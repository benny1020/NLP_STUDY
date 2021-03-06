https://wikidocs.net/21695

# 개요

- `언어모델`(`Languagel Model, LM`) 정의 - 언어라는 현상을 모델링하고자 단어 시퀀스(또는 문장)에 확률을 할당(assign)하는 모델. 즉, 가장 자연스러운 단어 시퀀스를 찾아내는 모델.
- 통계에 기반한 전통적인 언어 모델`Statistical Languagel Model, SLM` 우리가 실제 사용하는 자연어를 근사하기에는 많은 한계가 있고, 인공 신경망이 해결하면서 `SLM` 사용 빈도는 감소됨.
- 언어 모델 만드는 방법 - `통계` 또는 `인공 신경망`을 이용

### 언어모델 예시

- 이전 단어들이 주어졌을 때 다음 단어를 예측
- 주어진 양쪽의 단어들로부터 가운데 비어있는 단어를 예측

### 언어 모델링

- `언어 모델링(Language Modeling)` 주어진 단어들로부터 아직 모르는 단어를 예측하는 작업. 즉, 언어 모델이 이전 단어들로부터 다음 단어를 예측하는 일

## 단어 시퀀스의 확률 할당

### 기계 번역(Machine Translation)

언어 모델은 두 문장을 비교하여 좌측의 문장의 확률이 더 높다고 판단.

```python
P(나는 버스를 탔다) > P(나는 버스를 태운다)
```

### **오타 교정(Spell Correction)**

언어 모델은 두 문장을 비교하여 좌측의 문장의 확률이 더 높다고 판단

```python
선생님이 교실로 부리나케P(달려갔다) > P(잘려갔다)P(달려갔다) > P(잘려갔다)
```

### **음성 인식(Speech Recognition)**

언어 모델은 두 문장을 비교하여 우측의 문장의 확률이 더 높다고 판단.

```python
P(나는 메론을 먹는다) < P(나는 메론을 먹는다)
```

언어 모델은 위와 같이 확률을 통해 **보다 적절한 문장을 판단**

## 주어진 이전 단어들로부터 다음 단어 예측하기

- 조건부 확률로 표현

### **단어 시퀀스의 확률**

- 하나의 단어를 `w` , 단어 시퀀스을 대문자 `W` 라고 한다면, `n`개의 단어가 등장하는 단어 시퀀스 `W`의 확률

    $P(W) = P(w_1, w_2, w_3, w_4, w_5, ... ,w_n)$

### **다음 단어 등장 확률**

`n-1`개의 단어가 나열된 상태에서 `n`번째 단어의 확률. `|`의 기호는 `조건부 확률(conditional probability)`을 의미

$P(w_n | w_1, ..., w_{n-1})$

- 다섯번 째 단어의 확률: $P(W) = P(w_5 | w_1, w_2, w_3, w_4)$
- 전체 단어 시퀀스 `W`의 확률은 모든 단어가 예측되고 나서야 알 수 있으므로 단어 시퀀스의 확률은 다음과 같다.

    $P(W) = P(w_1, w_2, w_3, w_4, w_5, ... w_n) = \prod_{i=1}^{n}P(w_{n} | w_{1}, ... , w_{n-1})$

## 언어 모델의 간단한 직관

- 예시 - 비행기를 타려고 공항에 갔는데 지각을 하는 바람에 비행기를 [?]
    - 비행기를' 다음에 어떤 단어가 오게 될지 사람은 쉽게 '놓쳤다'라고 예상 가능
- 기계도 앞에 어떤 단어들이 나왔는지 고려하여 후보가 될 수 있는 여러 단어들에 대해서 확률을 예측해보고 가장 높은 확률을 가진 단어를 선택

## 검색 엔진에서의 언어 모델의 예

- 검색 엔진이 입력된 단어들의 나열에 대해서 다음 단어를 예측하는 언어 모델을 사용

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/36707813-fba5-43e7-8499-756cc2affad6/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/36707813-fba5-43e7-8499-756cc2affad6/Untitled.png)

---

# 통계적 언어 모델

- 통계적 언어 모델(`Statistical Language Model`), `SLM`

## 조건부 확률

### 확률 $P(A),P(B)$의 관계

- $p(B|A) = P(A,B)/P(A)$
- $p(A,B) = P(A)P(B|A)$

### 조건부 확률의 연쇄 법칙(chain rule)

$P(A,B,C,D) = P(A)P(B|A)P(C|A,B)P(D|A,B,C)$

### 조건부 확률의 일반화

$P(x_1, x_2, x_3 ... x_n) = P(x_1)P(x_2|x_1)P(x_3|x_1,x_2)...P(x_n|x_1 ... x_{n-1})$

## 문장에 대한 확률

- 문장 'An adorable little boy is spreading smiles'의 확률 `P(An adorable little boy is spreading smiles)`를 식으로 표현해보자.
- 문장의 확률 - 각 단어들이 이전 단어가 주어졌을 때 다음 단어로 등장할 확률의 곱

## 카운트 기반의 접근

## 카운트 기반 접근의 한계 - 희소 문제(Sparsity Problem)
- 충분한 데이터를 관측하지 못하여 정확히 모델링하지 못하는 문제

<math xmlns="http://www.w3.org/1998/Math/MathML" display="block">
  <mi>P</mi>
  <mtext>(is|An adorable little boy</mtext>
  <mo stretchy="false">)</mo>
  <mo>=</mo>
  <mfrac>
    <mrow>
      <mtext>count(An adorable little boy is</mtext>
      <mo stretchy="false">)</mo>
    </mrow>
    <mrow>
      <mtext>/ count(An adorable little boy&#xA0;</mtext>
      <mo stretchy="false">)</mo>
    </mrow>
  </mfrac>
</math>

---

# N-gram 언어 모델(N-gram Language Model)

## 코퍼스
- 대량의 텍스트 데이터

## 코퍼스에서 카운트하지 못하는 경우의 감소.
- P(is|An adorable little boy)≈ P(is|boy)
- P(is|An adorable little boy)≈ P(is|little boy)
- 즉, 앞에서는 An adorable little boy가 나왔을 때 is가 나올 확률을 구하기 위해서는 An adorable little boy가 나온 횟수와 An adorable little boy is가 나온 횟수를 카운트해야만 했지만, 이제는 단어의 확률을 구하고자 기준 단어의 앞 단어를 전부 포함해서 카운트하는 것이 아니라, 앞 단어 중 임의의 개수만 포함해서 카운트하여 근사하자는 것입니다.

## N-gram
- unigrams : an, adorable, little, boy, is, spreading, smiles 
- bigrams : an adorable, adorable little, little boy, boy is, is spreading, spreading smiles
- trigrams : an adorable little, adorable little boy, little boy is, boy is spreading, is spreading smiles
- 4-grams : an adorable little boy, adorable little boy is, little boy is spreading, boy is spreading smiles

## n-gram을 통한 언어모델에서는 다음에 나올 단어의 예측은 오직 n-1개의 단어에만 의존합니다.
- 'An adorable little boy is spreading' 4-gram을 이용한 언어모델을 통해 다음에 나올 단어를 예측할 때 n-1개 즉, 3개의 단어 ( boy is spreading )만 고려합니다
- 만약 갖고있는 코퍼스에서 boy is spreading가 1000번 등장했고 그 중 boy is spreading insults가 500번 boy is spreading smiles가 200번이라면 해당 모델은 확률적 선택에 따라 insults가 더 맞다고 판단합니다.

## N-gram Language Model의 한계
- n-gram은 뒤의 단어 몇 개만 보다 보니 의도하고 싶은 대로 문장을 끝맺음하지 못하는 경우가 생깁니다. 문장을 읽다 보면 앞 부분과 뒷부분의 문맥이 전혀 연결 안 되는 경우도 생길 수 있습니다.

## 희소 문제(Sparsity Problem)


### n을 선택하는 것은 trade-off 문제.
- n을 크게 선택하면 실제 훈련 코퍼스에서 해당 n-gram을 카운트할 수 있는 확률은 적어지므로 희소 문제는 점점 심각해집니다.
- n을 작게 선택하면 훈련 코퍼스에서 카운터는 잘 되겠지만 근사의 정확도는 현실의 확률분포와 멀어집니다.

### 적용 분야(Domain)에 맞는 코퍼스의 수집

## 인공 신경망을 이용한 언어 모델(Neural Network Based Language Model)

---

# 한국어에서의 언어 모델(Language Model for Korean Sentences)

- 영어나 기타 언어에 비해서 한국어는 언어 모델로 다음 단어를 예측하기가 훨씬 까다롭다.

## 한국어는 어순이 중요하지 않다.

- 이전 단어가 주어졌을때, 다음 단어가 나타날 확률을 구해야하는데 어떤 단어든 나타나도 된다.
- 예시) 아래 4개의 문장은 모두 의미 전달이 가능하며 주어인 `나는`을 생략해도 의미가 전달됨.

```python
① 나는 운동을 합니다 체육관에서.
② 나는 체육관에서 운동을 합니다.
③ 체육관에서 운동을 합니다.
④ 나는 운동을 체육관에서 합니다.
```

## 한국어는 교착어이다.

- 띄어쓰기 단위인 어절 단위로 `토큰화`를 할 경우에는 문장에서 발생가능한 단어의 수가 굉장히 늘어난다.
- 한국어는 `조사` 가 있기 때문에 `토큰화`를 통해 **접사나 조사 등의 분리** 작업이 굉장히 중요

## **한국어는 띄어쓰기가 제대로 지켜지지 않는다.**

- 한국어는 띄어쓰기를 제대로 하지 않아도 의미가 전달되며, 띄어쓰기 규칙 또한 상대적으로 까다로운 언어이다.
- 한국어 코퍼스는 띄어쓰기가 제대로 지켜지지 않는 경우가 많음.
- 토큰이 제대로 분리 되지 않는채 훈련 데이터로 사용된다면 언어 모델은 제대로 동작하지 않음!

---

# 펄플렉서티 (Perplexity) PPL
- 언어 모델을 평가하기 위한 내부 평가 지표

- PPL은 단어의 수로 정규화(normalization) 된 테스트 데이터에 대한 확률의 역수입니다. PPL을 최소화한다는 것은 문장의 확률을 최대화하는 것과 같습니다. 문장 W의 길이가 N이라고 하였을 때의 PPL은 다음과 같습니다.

- 이 언어 모델이 특정 시점에서 평균적으로 몇 개의 선택지를 가지고 고민하고 있는지를 의미합니다.
- PPL=10 -> 모든 시점마다 평균적으로 10개의 단어를 가지고 어떤 것이 정답인지 고민하고 있다.
- 즉, PPL이 더 낮은 언어 모델의 성능이 더 좋습니다.
- 테스트 데이터 상에서 높은 정확도를 보인다는 것이지, 사람이 직접 느끼기에 좋은 언어 모델이라는 것을 반드시 의미하진 않습니다.
- 언어 모델의 PPL은 테스트 데이터에 의존하므로 두 개 이상의 언어 모델을 비교할 때는 정량적으로 양이 많고, 또한 도메인에 알맞은 동일한 테스트 데이터를 사용해야 신뢰도가 높습니다.



# 조건부 확률
