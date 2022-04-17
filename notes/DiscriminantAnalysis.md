# DA : Discriminant Analysis

## 판별 분석

<br/>

[노션 보러가기](https://lavish-acorn-2f7.notion.site/DA-Discriminant-Analysis-ad16c0013ae6469fa99f0e378eecadd2)

<br/>

### 판별 분석의 정의

두 개 이상의 모집단에서 추출된 표본들이 지니고 있는 정보(데이터의 분포)를 이용하여 이 표본들이 어느 모집단에서 추출된 것인지를 결정해 줄 수 있는 기준을 찾는 분석법

![Untitled 1](https://user-images.githubusercontent.com/88828858/163699508-0268de03-f661-4256-9df1-057a46df5332.png)

<br/>

✔ 용어 정리

모집단 : 연구자가 알고 싶어하는 대상, 집단 전체

표본 : 연구자가 측정 또는 관찰한 결과의 집단

<br/>

✔ 어떤 것이 좋은 기준인가

L1 같이 두 클래스가 같이 잘 구분되는 경우 좋은 기준.

L2는 축에 투영된 그래프로 클래스를 구분하기 불가능하다.  → 좋지 않은 기준

<br/>

### 판별 분석의 기초 개념

✔ 판별 변수 (Discriminant Variable)

어떤 집단에 속하는지 판별하기 위한 변수, 독립 변수 중 판별력이 높은 변수를 뜻함.

판별 변수를 선택 시 고려사항 : 판별 기여도, 다른 독립 변수들과의 상관관계 

👎 상관관계가 높은 두 독립 변수 선택 

👍 두 독립변수 중 하나를 판별 변수로 선택 후 그것과 상관관계가 저근 독립변수 선택

→ 상관관계가 적은 것이 좋다 !

<br/>

✔ 판별 함수 (Discriminant Function)

각 개체들이 소속 집단에 얼마나 잘 판별되는가에 대한 판별력을 측정

→ 새로운 대상을 어느 집단으로 분류할 것이냐를 예측하는데 주요 목적

(각 개체는 어느 집단에 속해 있는지 알려져 있어야 한다. - Supervised Learning)

<br/>

✔ 판별 점수 (Discriminant Score)

대상의 판별 변수들의 값을 판별 함수에 대입하여 구한 값

<br/>

✔ 표본의 크기 

전체 표본의 크기(N : 학습 데이터의 수)는 독립변수의 개수(D)보다 3배(최소 2배) 이상, N > 3D

종속 변수의 집단 각각의 표본의 최소크기가 독립변수의 개수보다 커야함, 가장작은 표본 크기 > D

<br/>

### 판별 분석의 단계

1) 케이스가 속한 집단을 구분하는데 기여할 수 있는 독립 변수 찾기

2) 집단을 구분하는 기준이 되는 독립 변수들의 선형 결합, 즉 판별 함수 도출

3) 도출된 판별 함수에 의해 (학습데이터) 분류의 정확도 분석

4) 판별 함수를 이용하여 새로운 케이스(테스트 데이터)가 속하는 클래스 예측
![Untitled 2](https://user-images.githubusercontent.com/88828858/163699510-478d37f8-dce1-4b1b-8fea-1aa656792239.png)

<br/>

### LDA : 선형 판별 분석

✔ 가정

각 클래스 집단은 정규분포(Normal Distribution) 형태의 확률분포를 가짐

각 클래스의 집단은 비슷한 행태의 공분산(Convariance) 구조를 가짐

※ 공분산 : 2개의 확률변수의 상관 정도를 나타내는 값

🔽 공분산 분포의 종류

![Untitled](https://user-images.githubusercontent.com/88828858/163699512-3301d92e-38cf-439a-b4de-eb1aa7998051.png)

🔽 이와 같이 클래스들의 공분산 구조가 비슷해야함

![이와 같이 클래스들의 공분산 구조가 비슷해야함](https://user-images.githubusercontent.com/88828858/163699515-57c17a41-94be-4cf3-bc4d-6c8631ff175f.png)

<br/>

✔ LDA는 판별과 차원 축소의 기능

2차원(두가지 독립변수)의 두가지 범주(주황, 파랑)를 갖는 데이터를 분류하는 문제에서 LDA는 먼저 하나의 차원에 projection을 하여 차원을 축소 시킴 

![Untitled](https://user-images.githubusercontent.com/88828858/163699518-e46caeaa-0a8a-405d-8fbf-32a3779e1ebd.png)

<br/>

✔ LDA의 결정 경계의 특징

Projection축(실선)에 직교하는 축 : 점선

이 정사영(projection)은 두 분포의 특징이 아래의 목표를 달성해야함

→ 각 클래스 집단의 평균의 차이가 큰 지점을 결정경계로 지정 : | μ₁ - μ₂ | 가 큰 지점

→ 각 클래스 집단의 분산이 작은 지점을 결정 경계로 지정 : σ² 이 작은 지점

![Untitled 6](https://user-images.githubusercontent.com/88828858/163699520-02b27def-3632-4fb0-b01a-3b0781d354a9.png)

→ 즉, 분산 대비 평균의 차이를 극대화 하는 결정 경계를 찾고자 함

tip) 사영 데이터의 분포에서 겹치는 영역(보라색 영역)이 작은 결정 경계를 선택하면 된다.

<br/>

✔ 장점

변수(x) 간 공분산 구조를 반영

공분산 구조 가정이 살짝 위반되더라도 비교적 robust하게 동작

<br/>

✔ 단점

가장 작은 그룹의 샘플 수가 설명 변수의 개수보다 많아야 한다.

정규분포 가정에 크게 벗어나는 경우 잘 동작하지 못한다.

범주 사이(y)에 공분산 구조가 많이 다른 경우를 반영하지 못함 → 이차판별 분석법 (QDA)로 해결

<br/>

### QDA : 이차 판별 분석

✔ 정의

K(범주의 수)와 관계없이 공통 공분산 구조에 대한 가정을 만족하지 못한 경우 사용

LDA에서 공통 공분산구조에 대한 가정을 제외한 것이라 생각하자 !

→ 즉, Y의 범주 별로 서로다른 공분산 구조를 가진 경우에 활용

<br/>

✔ LDA vs QDA

![Untitled 7](https://user-images.githubusercontent.com/88828858/163699521-e8de5855-110d-4f66-9e43-0ee535743b08.png)

1) 원형(파랑)과 대각(노랑, 초록)의 공분산 구조를 갖는다. 

→ LDA의 결정 경계는 선형으로 가정하고 있어 서로 다른 공분산 분류에 어려움이 있다. 

2) LDA도 변수의 제곱을 한 추가적인 변수들을 통해 보완해 비선형 분류가 가능하다. 

3) QDA는 서로 다른 공분산 데이터를 분류 가능하다. → 비선형 분류 가능

<br/>

✔ 특징

서로 다른 공분산 데이터 분류를 위해 샘플이 많이 필요하다. 

상대적 단점 : 설명변수의 개수가 많을수록, 추정해야하는 모수가 많아짐 → 즉, 연상량이 큼

<br/>

✔ 예시

![Untitled](https://user-images.githubusercontent.com/88828858/163699522-d8d88614-0d8d-4fba-b4b4-c837525cf2b3.png)

∑₂ 와 ∑₃ 는 완전 공분산으로 비슷한 구조를 가짐, ∑₁ 는 구형 공분산 구조를 가짐 → QDA 적용

<br/>

## 💻실습해보기

<br/>

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

<br/>

### LDA의 하이퍼 파라미터

![image](https://user-images.githubusercontent.com/88828858/163699673-b56f437b-3528-4ad7-a46a-c9e2f5a369bc.png)

<br/>

### QDA의 하이퍼 파라미터

![image](https://user-images.githubusercontent.com/88828858/163699678-e05a2635-a68a-4fed-acb3-07ec9dae9fdc.png)

<br/>

### LDA와 QDA의 공통 메소드

![image](https://user-images.githubusercontent.com/88828858/163699680-728c62fe-0c0f-4c6b-ad57-e78cf9c09187.png)

<br/>

### LDA에만 존재하는 메소드

❔ 뭐가 다르길래 LDA만 존재하는가

![image](https://user-images.githubusercontent.com/88828858/163699685-5371e762-a588-4460-a6d6-d9009f11afaf.png)
