# Logistic Regression

## 로지스틱 회귀

- 궁금해요 !
    
    ✔ **선형회귀에서  CI vs PI**
    **ŷ =  β * x̂ + ε**
    confidence interval (신뢰 구간) : β의 추정 오차에 기인한 β의 신뢰도 범위 
    prediction interval (예측 구간) : 잡음(ε)까지 고려하여 실제 데이터가 관측될 범위
    
    ✔ **sparse data (희소데이터) VS dense data (밀집 데이터)**
    
    - sparse data : 차원/전체 공간에 비해 데이터가 있는 공간이 매우 협소한 데이터
    
    - dense data :  차원/전체 공간에 비해 데이터가 있는 공간이 빽빽히 차있는 데이터
    
    → 이걸 행렬로 본다면 희소 행렬은 행렬값에 0이 많은 행렬, 밀집 행렬은 0이 거의 없는 행렬
    

### 로지스틱 함수 (Logistic Function)

S-커브 함수를 의미. = 시그모이드 함수

x값으로 어떤 값이든 받을 수 있지만, 출력결과 (y)는 항상 0에서 1사이가 된다.

![Untitled](Logistic%20R%2099eed/Untitled.png)

### 승산 (Odds)

임의의 사건 A가 발생하지 않을 확률 대비 일어날 확률의 비율

![Untitled](Logistic%20R%2099eed/Untitled%201.png)

P(A)가 1에 가까울수록 승산은 커지고, P(A)가 0이라면 승산은 0

### 이항 로지스틱 회귀

Y가 연속된 숫자가 아닌 범주형인 경우 사용불가 !

그림 1) Y 승산에 로그를 취하면 → 승산(좌측)의 범위 = 회귀식(우측)의 범위

그림 2) P(x) : x가 주어졌을 때 범주 1일 확률, 우변의 식을 a로 치환해 정리 → 로지스틱 함수

![그림 1](Logistic%20R%2099eed/Untitled%202.png)

그림 1

![그림 2](Logistic%20R%2099eed/Untitled%203.png)

그림 2

### 이항 로지스틱 회귀의 결정 경계 (**decision boundry**)

이항 로지스틱 모델 : 범주 정보를 모르는 입력 벡터 x를 넣으면 범주 1에 속할 확률을 반환.

로지스틱모델의 결정경계 **:** βTx=0인 하이퍼플레인(hyperplane)

βTx<0 : 해당 데이터의 범주를 0으로 분류 , βTx>0 : 해당 데이터의 범주를 1로 분류 

![Untitled](Logistic%20R%2099eed/Untitled%204.png)

![Untitled](Logistic%20R%2099eed/Untitled%205.png)

### 다항 로지스틱 회귀

세번째 범주에 속할 확률 = 1- 첫번째 범주에 속할 확률 - 2번째 범주에 속할 확률

![Untitled](Logistic%20R%2099eed/Untitled%206.png)

### 다항 로지스틱 회귀와 소프트맥스

로그 승산으로 된 좌변을 로스 확률로 변경

![c번째에 속할 확률을 기준으로 식을 정리](Logistic%20R%2099eed/Untitled%207.png)

c번째에 속할 확률을 기준으로 식을 정리

![전제 확률의 합 = 1](Logistic%20R%2099eed/Untitled%208.png)

전제 확률의 합 = 1

## 💻실습해보기

### Logistic Regression의 하이퍼 파라미터

| parameter | info | default | kinds |
| --- | --- | --- | --- |
| ⭐ penalty | 규제에 사용된 기준
overfit을 극복하는 방법
큰 계수에 penalty를 주어 약화시킴 | l2 |  none  페날티 없음
 l2  제곱의 합
 l1  절댓값의 합
      0이 많은 데이터 (sparse)에 적합
 elasticnet   l1 + l2 |
| dual | Dual Fomulation 인지 
Primal Fomulation 인지 결정
 | False |  False  when n_samples > n_features
           Dual : 이중공식
           → iblinear + l2 경우에만 가능
 True  Primal : 초기공식 |
| tol | 중지 기준에 대한 허용 오차값 | 1e-4 | - |
| ⭐ C | 규제 강도 (람다) 의 역수 
규제화의 정도를 조절
* 람다 : 모델의 복잡도를 컨트롤 | 1.0 |  추가설명  작은 값 → 강한 규제
규제강도가 커질 수록 추정된 계수들의 절대값이 작아짐 → 모델 단순화 |
| fit_intercept | 의사 결정 함수에 상수 (절편)를 
추가할 지 여부 결정 | True |  True   
 False   |
| intercept_scaling | 정규화 효과 정도 | 1 |  추가설명  solver=’liblinear’ & fit_intercept =’True’ 인 경우에만 유용 |
| ⭐ class_weight | 데이터에 직접 가중치를 성정하여 학습의 강도를 다르게 할수 있음. | None | - |
| random_state | 난수 시드 설정 | None |  추가설명  solver = ‘sag’, ‘saga’, ‘liblinear’ 인 경우 데이터를 섞음 |
| ⭐ solver | 최적화 문제에 사용하는 알고리즘

 추가설명  sag와 saga는 피쳐스가 대략 비슷한 스케일을 가진 경우에만 빠른 수렴을 한다. | lbfgs |  newton-cg  멀티클래스의 분류모델
                    에 사용 [ l2, none ]
 lbfgs  멀티클래스 분류모델에 사용
           현재까지 가장 좋은 성능
           [ l2, none ]
 liblinear  작은 데이터셋에 적합
                one vs rest에 한정, [ l1, l2 ]
 sag  확률적 경사 하강법을 사용
         → 대용량 데이터셋에서 빠름
          [ l2, none ]
 saga  sag와 동일
          [ l1, l2, elasticnet, none ] |
| max_iter | 문제를 해결하는데 걸리는 최대 반복 횟수 (무한루프를 방지 하는 것) | 100 |  - |
| multi_class | 다중 분류 (3개 이상) 시 설정 값 | auto |  auto  
 ovr  one vs rest 방식
        데이터가 많아지면 시간 걸림
 multinomial  softmax 방식 (better) |
| verbose | 동작 과정에 대한 출력 메시지 | 0 |  추가설명  solver= ‘liblinear’, ‘lbfgs’의                
                 경우에만 사용 가능  |
| warm_start | 이전 호출에 사용했던 솔루션으로 초기화 할 것인지의 여부 | False |  True  
 False  이전 솔루션 삭제
 추가설명  solver==’liblinear’ : 무쓸모 |
| n_jobs | 병렬처리 시 사용할 CPU 코어의 수  | None |  None  = 1, 예외
 -1  using all proces
 추가설명  muliclass = ‘ovr’ 에서 사용
solver = ‘liblinear’ 경우 파라미터 무시 |
| l1_ratio | l1의 규제 비율
penalty=’elasticnet’경우에만 사용 | None |  0  penalty = ‘l2’
 1  penalty = ‘l1’
 0 < < 1  combination of l1 and l2 |

### Logistic Regression의 메소드

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
| densify() | Convert coefficient matrix (계수행렬) to dense array format.
Converts 계수행렬의 원소들을 (back) to a numpy.ndarray. | - |
| sparsify() | 계수행렬을 희소형식으로 변환
Converts 계수행렬의 원소들 to 
a scipy.spaese matrix |  |

```python
from sklearn.linear_model import LogisticRegression
logis = LogisticRegression( #다양한 파라미터 넣어보기 )
logis.fit(trainX, trainY)
testX_pred = logis.predict(testX)
```

- 참고자료
    
    [penalty](https://hanvenpark.wordpress.com/2016/10/15/logistic-regression%EC%9C%BC%EB%A1%9C-%EB%B3%B4%EB%8A%94-overfit/)