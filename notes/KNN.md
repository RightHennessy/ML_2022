# KNN : K-최근접 이웃

## K-Nearest Neighbors : K-최근접이웃

### 분류와 회귀

지도 학습의 대표적인 머신 러닝 방법

<br/>

✔ 분류

미리 정의된, 가능성 있는 여러 클래스 레이블 중 하나를 예측하는 것.

→ 이진 분류 (binary classification) : 두개의 클래스로 분류

→ 다중 분류 (multiclass classification) : 셋 이상의 클래스로 분류

<br/>

✔ 회귀

연속적인 숫자 또는 부동소수점수를 예측하는 것.

<br/>

### KNN의 개념

주변 k개의 자료의 클래스 중 가장 많은 클래스로 특정 자료를 분류하는 방식

Training-data 자체가 모형일 뿐 어떠한 추정방법도 모형도 없음

즉, 데이터의 분포를 표현하기 위한 파라미터를 추정하지 않음

매우 간단한 방법이나 performance는 떨어지지 않음

<br/>

✔ 게으른학습 또는 사례중심학습 (instance-based learing)

알고리즘은 훈련데이터에서 판별함수 (discriminative function)를 학습하는 대신 훈련 데이터 셋을 메모리에 저장하기 방법

<br/>

✔ 데이터의 차원이 증가 → 차원의 저주 문제 발생

KNN은 차원이 증가할 수록 성능 저하가 심하다.

데이터 차원이 증가할 수록 해당 공간의 크기가 기하급수적으로 증가하여 동일한 개수의 데이터의 밀도는 차원이 증가할수록 급속도로 희박해짐

<br/>

### KNN 거리 계산버

✔ Minkowski (민코프스키) 거리를 이용

m=1 : 맨하탄 거리

m=2 : 유클리디언 거리 (직선 거리)

![Untitled](https://user-images.githubusercontent.com/88828858/162591432-823e795a-bc22-4b2a-8559-321b2f3c319c.png)

![Untitled 1](https://user-images.githubusercontent.com/88828858/162591430-558c0244-eba1-443a-9ad1-fac86e6c9b5e.png)

<br/>

### KNN 분류 (classification)

✔ 근접치 k의 개수에 따른 Group 분류법

→ 다수결 방식 (Majority voting) : 이웃 범주 내에서 빈도가 가장 높은 범주 = 새 데이터의 범주

→ 가중 합 방식 (Weighted voting) : 가까운 이웃의 정보에 좀 더 가중치를 부여

 <br/>

### KNN 회귀 (regression)

✔ y 예측치 계산 법

k개의 정답(y)의 평균을 구한다.

→ 단순 회귀 : 가까운 이웃들의 단순한 평균

→ 가중 회귀 : 이웃이 얼마나 가까이에 있냐에 따라 가중치를 부여해 평균계산

<br/>

### KNN의 하이퍼 파라미터 K

✔ 탐색할 이웃 수 : k

k가 작을 경우 데이터의 지역적 특성을 지나치게 반영 → 과접합 (overfitting)

반대로 매우 클 경우 → 과한 정규화 (underfitting)

<br/>

### KNN의 장점과 단점

✔ 장점

학습 데이터 내의 노이즈의 영향을 크게 받지 않는다.

학습데이터 수가 많다면 꽤 효과적인 알고리즘이다.

마할라노비스 거리와 같이 데이터의 분산을 고려할 경우 매우 강건한 방법론

: 평균과의 거리가 표준 편차의 몇배인지 나타내는 값, 얼마나 이상한 값인지를 수치화하는 방법

<br/>

✔ 단점

최적 이웃의 수(k)와 어떤 거리 척도가 분석에 적합한지 불분명 

→ 각 데이터 특성에 맞게 연구자가 임의로 선정

best K는 데이터마다 다르기 때문에 탐욕적 방식 (Grid Search)으로 탐색 : 모든 경우를 시도

새로운 관측치와 각각의 학습 데이터 사이의 거리를 전부 측정 → 계산 시간이 오래 걸림

<br/>

## 💻실습해보기

- KNN 분류와 회귀의 차이점 ?
    
    분류는 라벨이 붙어 구분 가능 한것. 예를 들어 작물 분류처럼. 회귀는 자동차 가격 예측처럼 라벨 붙여 구분 불가능한 것 ~
    
<br/>
    

### KNN의 하이퍼 파라미터

![image](https://user-images.githubusercontent.com/88828858/162591629-93655590-827b-426e-bd47-9315fb86dd67.png)

<br/>

### KNN의 메소드

![image](https://user-images.githubusercontent.com/88828858/162591612-207b6824-695c-4f2c-a028-da725d760dfd.png)

<br/>

```python
# 학습
model.fit(X_train, y_train)
# 학습평가 -> 내가 풀었던 문제 다시 풀기 // 맞춘 비율
print(model.score(X_train, y_train))
# 실전평가 // 맞춘 비율 예)0.987364223..
print(model.score(X_test, y_test))
# 학습된 머신에 답이 없는 값 넣어 예측값 구하기
x_test_pred = model.predict(X_test)
# 예측값이 맞을 확률 구하기 // 배열로 결과값 알려줌
percent_x_pred = model.predict_proba(X_test)
```
