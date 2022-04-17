# DA : Discriminant Analysis

## 판별 분석

### 판별 분석의 정의

두 개 이상의 모집단에서 추출된 표본들이 지니고 있는 정보(데이터의 분포)를 이용하여 이 표본들이 어느 모집단에서 추출된 것인지를 결정해 줄 수 있는 기준을 찾는 분석법

![Untitled](DA%20Discrim%20b9741/Untitled.png)

✔ 용어 정리

모집단 : 연구자가 알고 싶어하는 대상, 집단 전체

표본 : 연구자가 측정 또는 관찰한 결과의 집단

✔ 어떤 것이 좋은 기준인가

L1 같이 두 클래스가 같이 잘 구분되는 경우 좋은 기준.

L2는 축에 투영된 그래프로 클래스를 구분하기 불가능하다.  → 좋지 않은 기준

### 판별 분석의 기초 개념

✔ 판별 변수 (Discriminant Variable)

어떤 집단에 속하는지 판별하기 위한 변수, 독립 변수 중 판별력이 높은 변수를 뜻함.

판별 변수를 선택 시 고려사항 : 판별 기여도, 다른 독립 변수들과의 상관관계 

👎 상관관계가 높은 두 독립 변수 선택 

👍 두 독립변수 중 하나를 판별 변수로 선택 후 그것과 상관관계가 저근 독립변수 선택

→ 상관관계가 적은 것이 좋다 !

✔ 판별 함수 (Discriminant Function)

각 개체들이 소속 집단에 얼마나 잘 판별되는가에 대한 판별력을 측정

→ 새로운 대상을 어느 집단으로 분류할 것이냐를 예측하는데 주요 목적

(각 개체는 어느 집단에 속해 있는지 알려져 있어야 한다. - Supervised Learning)

✔ 판별 점수 (Discriminant Score)

대상의 판별 변수들의 값을 판별 함수에 대입하여 구한 값

✔ 표본의 크기 

전체 표본의 크기(N : 학습 데이터의 수)는 독립변수의 개수(D)보다 3배(최소 2배) 이상, N > 3D

종속 변수의 집단 각각의 표본의 최소크기가 독립변수의 개수보다 커야함, 가장작은 표본 크기 > D

### 판별 분석의 단계

1) 케이스가 속한 집단을 구분하는데 기여할 수 있는 독립 변수 찾기

2) 집단을 구분하는 기준이 되는 독립 변수들의 선형 결합, 즉 판별 함수 도출

3) 도출된 판별 함수에 의해 (학습데이터) 분류의 정확도 분석

4) 판별 함수를 이용하여 새로운 케이스(테스트 데이터)가 속하는 클래스 예측

![Untitled](DA%20Discrim%20b9741/Untitled%201.png)

### LDA : 선형 판별 분석

✔ 가정

각 클래스 집단은 정규분포(Normal Distribution) 형태의 확률분포를 가짐

각 클래스의 집단은 비슷한 행태의 공분산(Convariance) 구조를 가짐

※ 공분산 : 2개의 확률변수의 상관 정도를 나타내는 값

![공분산 분포의 종류](DA%20Discrim%20b9741/Untitled%202.png)

공분산 분포의 종류

![이와 같이 클래스들의 공분산 구조가 비슷해야함](DA%20Discrim%20b9741/Untitled%203.png)

이와 같이 클래스들의 공분산 구조가 비슷해야함

✔ LDA는 판별과 차원 축소의 기능

2차원(두가지 독립변수)의 두가지 범주(주황, 파랑)를 갖는 데이터를 분류하는 문제에서 LDA는 먼저 하나의 차원에 projection을 하여 차원을 축소 시킴 

![Untitled](DA%20Discrim%20b9741/Untitled%204.png)

✔ LDA의 결정 경계의 특징

Projection축(실선)에 직교하는 축 : 점선

이 정사영(projection)은 두 분포의 특징이 아래의 목표를 달성해야함

→ 각 클래스 집단의 평균의 차이가 큰 지점을 결정경계로 지정 : | μ₁ - μ₂ | 가 큰 지점

→ 각 클래스 집단의 분산이 작은 지점을 결정 경계로 지정 : σ² 이 작은 지점

![Untitled](DA%20Discrim%20b9741/Untitled%205.png)

→ 즉, 분산 대비 평균의 차이를 극대화 하는 결정 경계를 찾고자 함

tip) 사영 데이터의 분포에서 겹치는 영역(보라색 영역)이 작은 결정 경계를 선택하면 된다.

✔ 장점

변수(x) 간 공분산 구조를 반영

공분산 구조 가정이 살짝 위반되더라도 비교적 robust하게 동작

✔ 단점

가장 작은 그룹의 샘플 수가 설명 변수의 개수보다 많아야 한다.

정규분포 가정에 크게 벗어나는 경우 잘 동작하지 못한다.

범주 사이(y)에 공분산 구조가 많이 다른 경우를 반영하지 못함 → 이차판별 분석법 (QDA)로 해결

### QDA : 이차 판별 분석

✔ 정의

K(범주의 수)와 관계없이 공통 공분산 구조에 대한 가정을 만족하지 못한 경우 사용

LDA에서 공통 공분산구조에 대한 가정을 제외한 것이라 생각하자 !

→ 즉, Y의 범주 별로 서로다른 공분산 구조를 가진 경우에 활용

✔ LDA vs QDA

![Untitled](DA%20Discrim%20b9741/Untitled%206.png)

1) 원형(파랑)과 대각(노랑, 초록)의 공분산 구조를 갖는다. 

→ LDA의 결정 경계는 선형으로 가정하고 있어 서로 다른 공분산 분류에 어려움이 있다. 

2) LDA도 변수의 제곱을 한 추가적인 변수들을 통해 보완해 비선형 분류가 가능하다. 

3) QDA는 서로 다른 공분산 데이터를 분류 가능하다. → 비선형 분류 가능

✔ 특징

서로 다른 공분산 데이터 분류를 위해 샘플이 많이 필요하다. 

상대적 단점 : 설명변수의 개수가 많을수록, 추정해야하는 모수가 많아짐 → 즉, 연상량이 큼

✔ 예시

![Untitled](DA%20Discrim%20b9741/Untitled%207.png)

∑₂ 와 ∑₃ 는 완전 공분산으로 비슷한 구조를 가짐, ∑₁ 는 구형 공분산 구조를 가짐 → QDA 적용

## 💻실습해보기

### 그래프로 분포 확인하는 법

```python
from matplotlib import pyplot as plt
plt.xlabel('LD1')
plt.ylabel('LD2')
plt.scatter(
	x_lda[:,0],
	x_lda[:,1],
	c=y_train,
	cmap='rainbow',
	alpha=0.7,
	edgecolors='b'
)
```

### LDA의 하이퍼 파라미터

| parameter | info | default | kinds |
| --- | --- | --- | --- |
| ⭐ solver | 사용할 solver
 추가설명  lsqr 과 eigen : shrinkage 나 convariance _estimator와 함께 사용 가능 | svd |  svd  특이값 분해, 공분산 행렬을 계산하지 않으므로 대규모 데이터에 추천
 lsqr  최소제곱해 
 eigen  고유값 분해. |
| shrinkage | 수축 매개변수

 추가설명  convariance_estimator 사용하는 경우 None 사용 | None |  None  수축 없음
 auto  Ledoit-Wolf 기본형 기반 자동화
 float between 0 and 1  고정 수축 파라미터, 0과 1사이의 부동 소수점 |
| priors | 클래스 사전 확률, 기본적으로 클래스 비율은 훈련데이터에서 추론 | None | - |
| n_components | 차원 감소를 위한 구성 요소 수
<= min(n_classes - 1, n_features)
transform 메소드에만 영향있음 | None |  None  min(n_classes - 1, n_features)
 |
| store_convariance | True 인경우 solver가 svd 일때 가중 된 클래스 내 공분산 행렬을 명시적으로 계산  | False |  - |
| tol | solver = svd 경우에만 사용 | 1.0e-4 | - |
| convariance_estimator | lsqr과 eigen 에서만 작동
shrinkage와 함께 사용 불가능 | None | - |

### QDA의 하이퍼 파라미터

| parameter | info | default | kinds |
| --- | --- | --- | --- |
| priors | 클래스 사전 확률, 기본적으로 클래스 비율은 훈련데이터에서 추론 | None | - |
| ⭐ reg_param | S2에 의한클래스 별 공분산 정규화
S2 = (1 - reg_param) × S2
        + reg_param × np.eye(n_features) | 0.0 | - |
| store_convariance | True 일 때 클래스 내 공분산 행렬이 명시적으로 계산되어 self.convariance_에 저장 | False |  - |
| tol |  | 1.0e-4 | - |

### LDA와 QDA의 공통 메소드

| methods | info | parameter |
| --- | --- | --- |
| ⭐ fit(X, y) | train 데이터셋에 학습시키는 과정
→ 데이터에 답을 맞춰보며 추정기 생성 |  X   training data 
 y   target values : 답 모음집
 sample_weight  default=None
        개별 샘플에 할당된 가중치 배열 |
| get_params([deep]) | 추정기에 대한 모수를 얻어오는 함수 | default=True |
| ⭐ predict(X) | train 데이터의 y 값들을 예측 |  X   test samples
 y   X값에 대한 y값들 |
| decision_function(X) | 예측의 불확실성을 추정 |  X  신뢰도를 추측하고 싶은 데이터 |
| predict_proba(X) | 확률 추정치.
각 가능한 결과 (각 클래스) 들에 대한 확률을 예측 |  X   test samples |
| predict_log_proba(X) | 확률 추정치의 로그를 예측 |  X   test samples |
| score(X, y[, sample_wight]) | 주어진 테스트 데이터 및 레이블에 대한 평균 정확도 도출 |  X   test samples
 y   X값에 대한 실제 y 정답들
 sample_weight   default=None |
| set_params(**params) | 추정기의 매개변수를 설정 |  **params   추정기의 매개변수 |

### LDA에만 존재하는 메소드

❔ 뭐가 다르길래 LDA만 존재하는가

| methods | info | parameter |
| --- | --- | --- |
| transform(X) | 클래스 분할을 최대화 | - |
| fit_transform(X[,y]) | fit 후 transform(변환) | fit_transform(X, y=None, **fit_params) |