# Dimension Reduction : 차원 축소

머신러닝을 이용한 데이터 분석 과정 중 전처리에는 ‘정규화’, ‘차원축소’, ‘영상처리’가 존재한다. 

이번 장에서는 그 중 차원 축소에 대해 알아보고자 한다. 

# 차원 축소의 개요

### 차원의 저주 (Curse of dimensionality)

✔ 차원이 증가할 수록 동일 정보량을 표현하기 위해 필요한 데이터의 수는 지수적으로 증가한다.

→ 데이터 학습을 위해 차원이 증가하면서 학습 데이터의 수가 차원 수보다 적어져 모델의 성능 저하

→ 데이터 차원이 증가할 수록 개별 차원 내 학습할 데이터 수가 적어지는 (sparse) 현상 발생

⭐ 무조건 변수의 수가 증가한다고 해서 차원의 저주 문제가 있는 것은 아니며, 데이터의 수 보다 변수의 수가 많아지면 발생한다. 

✔ 일반적으로 intrinsic dimension은 original dimension보다 상대적으로 적다. 

✔ 차원이 높을수록 발생하는 문제 

: 데이터에 포함될 노이즈의 비율도 높아진다. → 성능의 감소로 이어짐

: 모델 학습과 추론의 계산 복잡도가 높아진다. 

: 동일한 성능을 얻기 위해 더 많은 데이터의 수가 필요하다. 

✔ 차원의 저주 해결방법

1) 도메인 지식을 이용 → 중요한 특성만을 사용한다. (차원을 높이지 않는다는 뜻)

2) 목적 함수에 Regularization term 추가

3) 차원 축소 기술을 전처리로 사용한다. ⭐ 바로 이 부분이 오늘 배울 내용 ~`

![Untitled](Dimension%20Reduction%20%E1%84%8E%E1%85%A1%E1%84%8B%E1%85%AF%E1%86%AB%20%E1%84%8E%E1%85%AE%E1%86%A8%E1%84%89%E1%85%A9%20271e9184a1024dcd9d7de7b6a36c12a2/Untitled.png)

위 사진을 통해 차원이 어느 정도 이상 증가하면 성능이 급감함을 알 수 있다.

### 차원 축소 개요

✔ 배경

이론적으로, 차원의 증가는 모델 성능을 향상 시킨다. (가정 : 모든 변수가 서로 독립일 경우)

실제로, 차원의 증가는 모델 성능의 저하를 가져온다. (가정과 달리, 모든 변수는 서로 상관관계가 있고, 노이즈가 존재하기 때문이다. )

✔ 목적

모델의 성능을 최대로 해주는 변수의 일부 셋을 찾는 것

✔ 효과 

 - 변수간 상관 관계 (correlation) 제거

 - 단순한 후처리 (post-processing)

 - 적절한 정보를 유지하면서 중복되거나 불필요한 변수를 제거

✔ 종류

 1) LDA : 지도 학습 기반 차원 축소

학습결과가 피드백 되어 Feature  Selection을 반복한다. 

X, Y가 존재 → 정답과 예측값 비교를 통해 error를 보정한다.  

![Untitled](Dimension%20Reduction%20%E1%84%8E%E1%85%A1%E1%84%8B%E1%85%AF%E1%86%AB%20%E1%84%8E%E1%85%AE%E1%86%A8%E1%84%89%E1%85%A9%20271e9184a1024dcd9d7de7b6a36c12a2/Untitled%201.png)

 2) PCA : 비지도 학습 기반 차원 축소 

지도학습 처럼 피드백을 통한 Feature Selection의 반복이 없다.  → X만 제공

![Untitled](Dimension%20Reduction%20%E1%84%8E%E1%85%A1%E1%84%8B%E1%85%AF%E1%86%AB%20%E1%84%8E%E1%85%AE%E1%86%A8%E1%84%89%E1%85%A9%20271e9184a1024dcd9d7de7b6a36c12a2/Untitled%202.png)

.

✔ 방법

1) 변수/피쳐 선택 : 유의미한 변수만 선택

 - 장점 : 선택한 변수 해석 용이

 - 단점 : 변수 간 상관관계 고려의 어려움 

2) 변수/피쳐 추출 : 예측 변수의 변환(변환함수가 필요)을 통해 새로운 변수 추추

 - 변수/피쳐 생성(Feature construction) 이라고도 함

 - 장점 : 변수간 상관관계 고려, 변수의 개수를 많이 줄일 수 있다. 

 - 단점 : 추출된 변수의 해석이 어렵다. 

 z = f(x₁, x₂, … , x₁₀₀) : 선형결합을 만드는 f 함수를 통해 새로운 변수 z를 추출한다. 

⭐ 종류 X 방법 = 2 X 2 = 4가지의 방법이 존재한다. ~

# 주성분 분석 : PCA

### 목적

차원을 줄이려는 비지도 학습 방법 중 한가지 

사영 후 데이터의 분산(variance)을 최대한 보존할 수 있는 기저를 찾아 차원을 줄이는 방법

![Untitled](Dimension%20Reduction%20%E1%84%8E%E1%85%A1%E1%84%8B%E1%85%AF%E1%86%AB%20%E1%84%8E%E1%85%AE%E1%86%A8%E1%84%89%E1%85%A9%20271e9184a1024dcd9d7de7b6a36c12a2/Untitled%203.png)

### 예시 : MNIST

![Untitled](Dimension%20Reduction%20%E1%84%8E%E1%85%A1%E1%84%8B%E1%85%AF%E1%86%AB%20%E1%84%8E%E1%85%AE%E1%86%A8%E1%84%89%E1%85%A9%20271e9184a1024dcd9d7de7b6a36c12a2/Untitled%204.png)

### 방법

데이터를 사영(projection) 시킬 경우 손실되는 정보의 양이 적은 쪽의 기저(축)를 선택

→ 분산이 큰 쪽을 선택 ~

![Untitled](Dimension%20Reduction%20%E1%84%8E%E1%85%A1%E1%84%8B%E1%85%AF%E1%86%AB%20%E1%84%8E%E1%85%AE%E1%86%A8%E1%84%89%E1%85%A9%20271e9184a1024dcd9d7de7b6a36c12a2/Untitled%205.png)

위의 경우 왼쪽 기저가 오른쪽 기저보다 원 데이터의 분산을 최대로 유지하므로 왼쪽을 선택

## PCA의 수리적 배경

### 주성분 분석 : 선형 결합

데이터(X) 사영 변환 후(Z)에도 분산이 보존하는 기저(a)을 찾는 것

![Untitled](Dimension%20Reduction%20%E1%84%8E%E1%85%A1%E1%84%8B%E1%85%AF%E1%86%AB%20%E1%84%8E%E1%85%AE%E1%86%A8%E1%84%89%E1%85%A9%20271e9184a1024dcd9d7de7b6a36c12a2/Untitled%206.png)

![Untitled](Dimension%20Reduction%20%E1%84%8E%E1%85%A1%E1%84%8B%E1%85%AF%E1%86%AB%20%E1%84%8E%E1%85%AE%E1%86%A8%E1%84%89%E1%85%A9%20271e9184a1024dcd9d7de7b6a36c12a2/Untitled%207.png)

P차원 data ——PCA——> P개의 축 ⇒ P개의 차원을 갖는 변수

### 공분산 (Covariance) : 변수의 상관 정도

X : 입력 데이터 (n 개의 데이터, d 개의 변수)

![Untitled](Dimension%20Reduction%20%E1%84%8E%E1%85%A1%E1%84%8B%E1%85%AF%E1%86%AB%20%E1%84%8E%E1%85%AE%E1%86%A8%E1%84%89%E1%85%A9%20271e9184a1024dcd9d7de7b6a36c12a2/Untitled%208.png)

데이터 셋의 전체 분산(Total variance)

→ tr[Conv(x)] = Conv(X)11+ Conv(X)22 + … + Conv(X)dd  (trace : 대각합..)

![Untitled](Dimension%20Reduction%20%E1%84%8E%E1%85%A1%E1%84%8B%E1%85%AF%E1%86%AB%20%E1%84%8E%E1%85%AE%E1%86%A8%E1%84%89%E1%85%A9%20271e9184a1024dcd9d7de7b6a36c12a2/Untitled%209.png)

Conv(A)는 대칭행렬이다..냠

1행에서 1열 : 1-1관계, 2열: 1-2관계, 3열: 1-3관계..를 뜻한다 ~

### 사영(Projection)

![Untitled](Dimension%20Reduction%20%E1%84%8E%E1%85%A1%E1%84%8B%E1%85%AF%E1%86%AB%20%E1%84%8E%E1%85%AE%E1%86%A8%E1%84%89%E1%85%A9%20271e9184a1024dcd9d7de7b6a36c12a2/Untitled%2010.png)

### 고유값(eigenvalue)과 고유벡터(eigenvector)

![Untitled](Dimension%20Reduction%20%E1%84%8E%E1%85%A1%E1%84%8B%E1%85%AF%E1%86%AB%20%E1%84%8E%E1%85%AE%E1%86%A8%E1%84%89%E1%85%A9%20271e9184a1024dcd9d7de7b6a36c12a2/Untitled%2011.png)

행렬 A 가 Non-singular (역행렬이 존재) 하다면, d개의 고유값과 고유벡터가 존재함

고유벡터는 서로 직교함(orthogonal)

tr(A) = λ₁ + λ₂ + … + λ_d

✔ 벡터에 행렬을 곱하는 것은 선형 변환의 의미를 갖는다. 

고유벡터는 변환에 의해 방향 변화가 발생하지 않음

고유벡터의 크기 변화는 λ 만큼

![Untitled](Dimension%20Reduction%20%E1%84%8E%E1%85%A1%E1%84%8B%E1%85%AF%E1%86%AB%20%E1%84%8E%E1%85%AE%E1%86%A8%E1%84%89%E1%85%A9%20271e9184a1024dcd9d7de7b6a36c12a2/Untitled%2012.png)

### 주성분 분석 알고리즘

1️⃣ **데이터 센터링 (data centering)** : 데이터 평균을 0으로 변경

![Untitled](Dimension%20Reduction%20%E1%84%8E%E1%85%A1%E1%84%8B%E1%85%AF%E1%86%AB%20%E1%84%8E%E1%85%AE%E1%86%A8%E1%84%89%E1%85%A9%20271e9184a1024dcd9d7de7b6a36c12a2/Untitled%2013.png)

2️⃣ **최적화 문제 정의** : X의 covariance, Cor(X) = S 구하기

데이터 X를 기저 벡터 W에 사영(projection)하면, 사용 후 분산은 다음과 같다.

![Untitled](Dimension%20Reduction%20%E1%84%8E%E1%85%A1%E1%84%8B%E1%85%AF%E1%86%AB%20%E1%84%8E%E1%85%AE%E1%86%A8%E1%84%89%E1%85%A9%20271e9184a1024dcd9d7de7b6a36c12a2/Untitled%2014.png)

![Untitled](Dimension%20Reduction%20%E1%84%8E%E1%85%A1%E1%84%8B%E1%85%AF%E1%86%AB%20%E1%84%8E%E1%85%AE%E1%86%A8%E1%84%89%E1%85%A9%20271e9184a1024dcd9d7de7b6a36c12a2/Untitled%2015.png)

![Untitled](Dimension%20Reduction%20%E1%84%8E%E1%85%A1%E1%84%8B%E1%85%AF%E1%86%AB%20%E1%84%8E%E1%85%AE%E1%86%A8%E1%84%89%E1%85%A9%20271e9184a1024dcd9d7de7b6a36c12a2/Untitled%2016.png)

S 는 X의 covariace matrix

❕ PCA의 목적은 사영 이후 분산 V를 최대화 하는 것이다

3️⃣ **최적화 문제 솔루션** : S의 eigen vector와 eigen value 구하기

라그랑지 멀티플라이어(Lagrangian multiplier) 적용

![Untitled](Dimension%20Reduction%20%E1%84%8E%E1%85%A1%E1%84%8B%E1%85%AF%E1%86%AB%20%E1%84%8E%E1%85%AE%E1%86%A8%E1%84%89%E1%85%A9%20271e9184a1024dcd9d7de7b6a36c12a2/Untitled%2017.png)

![Untitled](Dimension%20Reduction%20%E1%84%8E%E1%85%A1%E1%84%8B%E1%85%AF%E1%86%AB%20%E1%84%8E%E1%85%AE%E1%86%A8%E1%84%89%E1%85%A9%20271e9184a1024dcd9d7de7b6a36c12a2/Untitled%2018.png)

w : S의 eigen vector , λ : S의 eigen value

4️⃣ **주축 정렬** : eigen value에 해당하는 eigen vectors를 순서대로 정렬

![Untitled](Dimension%20Reduction%20%E1%84%8E%E1%85%A1%E1%84%8B%E1%85%AF%E1%86%AB%20%E1%84%8E%E1%85%AE%E1%86%A8%E1%84%89%E1%85%A9%20271e9184a1024dcd9d7de7b6a36c12a2/Untitled%2019.png)

위 식에 따르면 W₁ 에 사영된 데이터의 분산은 λ₁ 이다.

![Untitled](Dimension%20Reduction%20%E1%84%8E%E1%85%A1%E1%84%8B%E1%85%AF%E1%86%AB%20%E1%84%8E%E1%85%AE%E1%86%A8%E1%84%89%E1%85%A9%20271e9184a1024dcd9d7de7b6a36c12a2/Untitled%2020.png)

즉, 96%의 데이터를 첫번째 eigen value(즉, 주성분)으로 분류 가능하다. 

5️⃣ **PCA로 변환된 데이터**

![Untitled](Dimension%20Reduction%20%E1%84%8E%E1%85%A1%E1%84%8B%E1%85%AF%E1%86%AB%20%E1%84%8E%E1%85%AE%E1%86%A8%E1%84%89%E1%85%A9%20271e9184a1024dcd9d7de7b6a36c12a2/Untitled%2021.png)

6️⃣ **원데이터로 복원**

2D 데이터 → 1D PCA → 2D 데이터 복원 (reconstruction) : 물론 완벽 복원은 안된다..

![Untitled](Dimension%20Reduction%20%E1%84%8E%E1%85%A1%E1%84%8B%E1%85%AF%E1%86%AB%20%E1%84%8E%E1%85%AE%E1%86%A8%E1%84%89%E1%85%A9%20271e9184a1024dcd9d7de7b6a36c12a2/Untitled%2022.png)

### 주성분 분석 이슈

✔ 주성분 개수 선정법 : 몇개의 주성분을 사용해야할까?

 방법 1) 고유 값 감소율이 유의미하게 낮아지는 Elbow Point 에 해당한느 주성분 선택

 방법 2) 일정 수준 이상의 분산 비를 보존하는 최소의 주성분을 선택 (보통 70% 이상)

![Untitled](Dimension%20Reduction%20%E1%84%8E%E1%85%A1%E1%84%8B%E1%85%AF%E1%86%AB%20%E1%84%8E%E1%85%AE%E1%86%A8%E1%84%89%E1%85%A9%20271e9184a1024dcd9d7de7b6a36c12a2/Untitled%2023.png)

예시 )

![Untitled](Dimension%20Reduction%20%E1%84%8E%E1%85%A1%E1%84%8B%E1%85%AF%E1%86%AB%20%E1%84%8E%E1%85%AE%E1%86%A8%E1%84%89%E1%85%A9%20271e9184a1024dcd9d7de7b6a36c12a2/Untitled%2024.png)

전체 데이터 분산의 80%를 포함해야하는 경우 : PC1~PC5 선택 

전체 데이터 분산의 70%를 포함해야하는 경우 :  PC1~PC4 선택 

### 주성분 분석 한계

1) 데이터 분포가 단일 가우시안인 경우에만 적용 가능하다. 

![Untitled](Dimension%20Reduction%20%E1%84%8E%E1%85%A1%E1%84%8B%E1%85%AF%E1%86%AB%20%E1%84%8E%E1%85%AE%E1%86%A8%E1%84%89%E1%85%A9%20271e9184a1024dcd9d7de7b6a36c12a2/Untitled%2025.png)

2) 분류 문제를 위해 디자인되지 않음, 즉 분류 성능 향상을 보장하지 못함

![Untitled](Dimension%20Reduction%20%E1%84%8E%E1%85%A1%E1%84%8B%E1%85%AF%E1%86%AB%20%E1%84%8E%E1%85%AE%E1%86%A8%E1%84%89%E1%85%A9%20271e9184a1024dcd9d7de7b6a36c12a2/Untitled%2026.png)

### 기타 차원 축소

✔ 랜덤 PCA : Randomized PCA

자료의 크기 또는 특성변수의 크기가 매우 크면 주성분 W 를 구하기 위한 SVD 계산이 불가능하거나 시간이 많이 소요된다. → 이런 경우 Randomized PCA 가 유용

: QR 분해를 이용하여 행렬의 SVD를 수행한다.

✔ 커널 PCA : kernel PCA

PCA는 선형 변환이고 Kernelized PCA는 비선형 변환이다.

: SVM의 커널트릭을 PCA에서도 사용

: 특성 변수 x를 비선형 h(x)로 번환한 후 이에 대해 PCA를 하여 차원 축소를 하는 방법

![Untitled](Dimension%20Reduction%20%E1%84%8E%E1%85%A1%E1%84%8B%E1%85%AF%E1%86%AB%20%E1%84%8E%E1%85%AE%E1%86%A8%E1%84%89%E1%85%A9%20271e9184a1024dcd9d7de7b6a36c12a2/Untitled%2027.png)

## 💻실습해보기

? PCA 주축의 수 결정법

![Untitled](Dimension%20Reduction%20%E1%84%8E%E1%85%A1%E1%84%8B%E1%85%AF%E1%86%AB%20%E1%84%8E%E1%85%AE%E1%86%A8%E1%84%89%E1%85%A9%20271e9184a1024dcd9d7de7b6a36c12a2/Untitled%2028.png)