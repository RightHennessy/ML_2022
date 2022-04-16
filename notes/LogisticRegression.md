# Logistic Regression

## 로지스틱 회귀

<br/>

[노션 보러가기](https://lavish-acorn-2f7.notion.site/Logistic-Regression-1350763634374745a0b9cb60d318e7aa)

<br/>

<details>
<summary> 궁금해요 ! </summary>
<div markdown="1">

<br/>    
    
✔ **선형회귀에서  CI vs PI**
    
**ŷ =  β * x̂ + ε**

confidence interval (신뢰 구간) : β의 추정 오차에 기인한 β의 신뢰도 범위 

prediction interval (예측 구간) : 잡음(ε)까지 고려하여 실제 데이터가 관측될 범위
    
<br/>    
    
✔ **sparse data (희소데이터) VS dense data (밀집 데이터)**
    
- sparse data : 차원/전체 공간에 비해 데이터가 있는 공간이 매우 협소한 데이터

- dense data :  차원/전체 공간에 비해 데이터가 있는 공간이 빽빽히 차있는 데이터

    → 이걸 행렬로 본다면 희소 행렬은 행렬값에 0이 많은 행렬, 밀집 행렬은 0이 거의 없는 행렬

</div>
</details>

<br/>    
    
### 로지스틱 함수 (Logistic Function)

S-커브 함수를 의미. = 시그모이드 함수

x값으로 어떤 값이든 받을 수 있지만, 출력결과 (y)는 항상 0에서 1사이가 된다.

![Untitled](https://user-images.githubusercontent.com/88828858/163663438-52e78e08-1942-4294-8e9a-765a946d3893.png)

<br/>

### 승산 (Odds)

임의의 사건 A가 발생하지 않을 확률 대비 일어날 확률의 비율

![Untitled 1](https://user-images.githubusercontent.com/88828858/163663429-77c61c2c-519d-43c6-8633-47c356919a01.png)

P(A)가 1에 가까울수록 승산은 커지고, P(A)가 0이라면 승산은 0

<br/>

### 이항 로지스틱 회귀

Y가 연속된 숫자가 아닌 범주형인 경우 사용불가 !

그림 1) Y 승산에 로그를 취하면 → 승산(좌측)의 범위 = 회귀식(우측)의 범위

그림 2) P(x) : x가 주어졌을 때 범주 1일 확률, 우변의 식을 a로 치환해 정리 → 로지스틱 함수

![그림 1](https://user-images.githubusercontent.com/88828858/163663430-edf98e97-9c1b-4e84-ab9f-93879ab35205.png) 
![그림 2](https://user-images.githubusercontent.com/88828858/163663432-a0d3273c-2cde-4980-a298-e74928d53fe6.png)

<br/>

### 이항 로지스틱 회귀의 결정 경계 (**decision boundry**)

이항 로지스틱 모델 : 범주 정보를 모르는 입력 벡터 x를 넣으면 범주 1에 속할 확률을 반환.

로지스틱모델의 결정경계 **:** βTx=0인 하이퍼플레인(hyperplane)

βTx<0 : 해당 데이터의 범주를 0으로 분류 , βTx>0 : 해당 데이터의 범주를 1로 분류 

![Untitled 4](https://user-images.githubusercontent.com/88828858/163663433-f16de6bf-c574-49ae-bca2-71a243dfea24.png)

![Untitled 5](https://user-images.githubusercontent.com/88828858/163663434-1048b99f-e910-4f3b-9f64-da4bc9ca002f.png)

<br/>

### 다항 로지스틱 회귀

세번째 범주에 속할 확률 = 1- 첫번째 범주에 속할 확률 - 2번째 범주에 속할 확률

![Untitled 6](https://user-images.githubusercontent.com/88828858/163663435-b69b2d0e-05b1-40f8-9ae4-0768edbbb274.png)

<br/>

### 다항 로지스틱 회귀와 소프트맥스

로그 승산으로 된 좌변을 로스 확률로 변경

![Untitled 7](https://user-images.githubusercontent.com/88828858/163663436-4f442471-8b02-4531-9ee0-bf60fa8ba62f.png)

c번째에 속할 확률을 기준으로 식을 정리

![Untitled 8](https://user-images.githubusercontent.com/88828858/163663437-65c8b9dd-5f9f-49f6-abaa-2ea30c06acd0.png)

전제 확률의 합 = 1

<br/>

## 💻실습해보기

<br/>

### Logistic Regression의 하이퍼 파라미터

![image](https://user-images.githubusercontent.com/88828858/163664092-f1c8b9bc-204e-4af2-b5ec-21b1c0dd803e.png)

<br/>

### Logistic Regression의 메소드

![image](https://user-images.githubusercontent.com/88828858/163664103-635b8185-efde-4f8e-8b39-dafecc7c74ae.png)

<br/>

```python
from sklearn.linear_model import LogisticRegression
logis = LogisticRegression( #다양한 파라미터 넣어보기 )
logis.fit(trainX, trainY)
testX_pred = logis.predict(testX)
```

- 참고자료
    
    [penalty](https://hanvenpark.wordpress.com/2016/10/15/logistic-regression%EC%9C%BC%EB%A1%9C-%EB%B3%B4%EB%8A%94-overfit/)
