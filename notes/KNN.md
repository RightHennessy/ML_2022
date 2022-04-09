# KNN : K-최근접 이웃

## **K-Nearest Neighbors : K-최근접이웃**

### 분류와 회귀

지도 학습의 대표적인 머신 러닝 방법

✔ 분류

미리 정의된, 가능성 있는 여러 클래스 레이블 중 하나를 예측하는 것.

→ 이진 분류 (binary classification) : 두개의 클래스로 분류

→ 다중 분류 (multiclass classification) : 셋 이상의 클래스로 분류

✔ 회귀

연속적인 숫자 또는 부동소수점수를 예측하는 것.

### KNN의 개념

주변 k개의 자료의 클래스 중 가장 많은 클래스로 특정 자료를 분류하는 방식

Training-data 자체가 모형일 뿐 어떠한 추정방법도 모형도 없음

즉, 데이터의 분포를 표현하기 위한 파라미터를 추정하지 않음

매우 간단한 방법이나 performance는 떨어지지 않음

✔ 게으른학습 또는 사례중심학습 (instance-based learing)

알고리즘은 훈련데이터에서 판별함수 (discriminative function)를 학습하는 대신 훈련 데이터 셋을 메모리에 저장하기 방법

✔ 데이터의 차원이 증가 → 차원의 저주 문제 발생

KNN은 차원이 증가할 수록 성능 저하가 심하다.

데이터 차원이 증가할 수록 해당 공간의 크기가 기하급수적으로 증가하여 동일한 개수의 데이터의 밀도는 차원이 증가할수록 급속도로 희박해짐

### KNN 거리 계산버

✔ Minkowski (민코프스키) 거리를 이용

m=1 : 맨하탄 거리

m=2 : 유클리디언 거리 (직선 거리)

![Untitled](KNN%20K-%E1%84%8E%E1%85%AC%E1%84%80%E1%85%B3%207bf1b/Untitled.png)

![Untitled](KNN%20K-%E1%84%8E%E1%85%AC%E1%84%80%E1%85%B3%207bf1b/Untitled%201.png)

### KNN 분류 (classification)

✔ 근접치 k의 개수에 따른 Group 분류법

→ 다수결 방식 (Majority voting) : 이웃 범주 내에서 빈도가 가장 높은 범주 = 새 데이터의 범주

→ 가중 합 방식 (Weighted voting) : 가까운 이웃의 정보에 좀 더 가중치를 부여

 

### KNN 회귀 (regression)

✔ y 예측치 계산 법

k개의 정답(y)의 평균을 구한다.

→ 단순 회귀 : 가까운 이웃들의 단순한 평균

→ 가중 회귀 : 이웃이 얼마나 가까이에 있냐에 따라 가중치를 부여해 평균계산

### KNN의 하이퍼 파라미터 K

✔ 탐색할 이웃 수 : k

k가 작을 경우 데이터의 지역적 특성을 지나치게 반영 → 과접합 (overfitting)

반대로 매우 클 경우 → 과한 정규화 (underfitting)

### KNN의 장점과 단점

✔ 장점

학습 데이터 내의 노이즈의 영향을 크게 받지 않는다.

학습데이터 수가 많다면 꽤 효과적인 알고리즘이다.

마할라노비스 거리와 같이 데이터의 분산을 고려할 경우 매우 강건한 방법론

: 평균과의 거리가 표준 편차의 몇배인지 나타내는 값, 얼마나 이상한 값인지를 수치화하는 방법

✔ 단점

최적 이웃의 수(k)와 어떤 거리 척도가 분석에 적합한지 불분명 

→ 각 데이터 특성에 맞게 연구자가 임의로 선정

best K는 데이터마다 다르기 때문에 탐욕적 방식 (Grid Search)으로 탐색 : 모든 경우를 시도

새로운 관측치와 각각의 학습 데이터 사이의 거리를 전부 측정 → 계산 시간이 오래 걸림

## 💻실습해보기

- KNN 분류와 회귀의 차이점 ?
    
    분류는 라벨이 붙어 구분 가능 한것. 예를 들어 작물 분류처럼. 회귀는 자동차 가격 예측처럼 라벨 붙여 구분 불가능한 것 ~
    

### KNN의 하이퍼 파라미터

| parameter | info | default | kinds |
| --- | --- | --- | --- |
| ⭐ n_neighnors | 이웃의 갯수 | 5 | - |
| ⭐ weights | 거리의 가중치 | uiform |  uniform  거리에 따른 가중치 없음
 distance  가까운 이웃일수록 높은 가중치
 callable  사용자가 임의로 가중치를 부여 |
| algorithm | 가까운 이웃을 구하는데 사용되는 알고리즘 | auto |  auto   fit 메소드에서 전달된 값을 기반으로
           가장 적합한 알고리즘을 사용
 ball_tree  kd_tree의 비효율성 해소 대신 비쌈
                 매우 구조화/높은 차원 데이터에 굿
 kd_tree   비효율적인 brute 해소
                A-B멀고 B-C가 가깝다면 A-C는 멀다  
 brute   brute-force (=억지로)
             큰 샘플에서 비효율적 |
| leaf_size | ball_tree나 kd_tree에 
전달하는 leaf의 크기 | 30 |  추가설명   트리에서 몇 대 몇으로 뻗어 나갈지를 나타내는 값 
너무 작으면 → 가지 수가 많아짐
                         노이즈가 끼기 쉽고 속도 느림
너무 크면 → 너무 대충 분류해 예측 성능 저하 |
| ⭐ p | 거리를 구할 때 사용되는minkowski의 매개변수 | 2 |  l1 (p=1)   맨하탄 거리
 l2 (p=2)   유클리디언 거리 |
| metric | 미터법, 거리계산법 | minkowski | 다양한 metric이 궁금하다면 → 참고자료 |
| metric_params | metric의 추가 키워드 | none | - |
| n_jobs | 계산에 사용할 CPU (core)의 갯수를 지정 | none |  1   default(=none)인 경우 1개 사용 → 예외
 -1   사용가능한 모든 core 사용 |

### KNN의 메소드

| methods | info | parameter |
| --- | --- | --- |
| ⭐ fit(X, y) | train 데이터셋에 
학습시키는 과정 |  X   training data 
 y   target values : 답 모음집
→ 데이터에 답을 맞춰보며 추정기 생성 |
| get_params([deep]) | 추정기에 대한 모수를 
얻어오는 함수 | default=True |
| kneighbors(X, n_neighbors, return_distance]) | Find the K-neighbors of a point.
Returns indices of and distances to the neighbors of each point. ( 머라는겨.. =_= ) |  X   default=None (자동 전달)
      The query point or points.
 n_neighbors   default=None (자동 전달)
                        각 샘플에 요구되는 n.. 개수
 return_distance   default=True 
                            거리를 반환받을지 여부 |
| kneighbors_graph ([X, n_neighbors, mode]) | Compute the (weighted) graph of k-Neighbors for points in X. |  X   default=None (자동 전달)
      The query point or points.
 n_neighbors   default=None (자동 전달)
                        각 샘플들의 neighbor 수
 mode   default=connectivity
               : 0과 1로 표현된 인접행렬 반환
              + distance : 각 포인트들의 거리 |
| ⭐ predict(X) | train 데이터의 y 값들을 예측 |  X   test samples
 y   X값에 대한 y값들 |
| predict_proba(X) | 각 가능한 결과들에 대한 
확률을 예측 |  X   test samples |
| score(X, y[, sample_wight]) | 주어진 테스트 데이터 및 레이블에 대한 평균 정확도 도출 |  X   test samples
 y   X값에 대한 실제 y 정답들
 sample_weight   default=None |
| set_params(**params) | 추정기의 매개변수를 설정 |  **params   추정기의 매개변수 |

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