# 실습 TIP

- 생각할 점
    
    하나의 열 내에서 문자열로 되어있는 데이터 값 → LabelEncoder로 숫자로 변경
    
    열끼리의 숫자 크기가 많이 다를 경우 → Scaler
    
    KNN → 1) 분류가 되는 경우 : classifier 사용     2) 연속적인 숫자의 값 : regressor 사용
    

- 자잘 코드
    
    `trainX.isnull().sum()`  isnull이 존재하는지 확인
    
</br>
    

### 기계학습의 일반적인 순서

1️⃣ 데이터셋 불러오기 

2️⃣ 데이터셋 카테고리의 실수화

3️⃣ 데이터 분할

4️⃣ (옵션) 입력데이터의 표준화

5️⃣ 모형 추정 혹은 사례중심학습

6️⃣ 결과 분석

</br>


### 1️⃣ 데이터셋 불러오기

✔ Iris 데이터 불러오기

```python
# seaborn 불러오기
import seaborn as sns
iris = sns.load_dataset('iris')
```

✔ Seaborn 라이브러리 

파이썬에서 데이터 시각화를 담당하는 모듈

유익한 통계 그래픽을 그리기 위한 고급 인터페이스를 제공

</br>


### 2️⃣ 데이터셋 카테고리의 실수화

머신이 이해가능한 실수로 변형시켜 주는 것

예 ) species : [’setosa’, ‘versicolor’, ‘virginica’] → [0, 1, 2]

DictVectorize 클래스 VS LabelEncoder 클래스 : One-hot encoding vs 범주형 라벨

3개 이상 multi label을 가진 data를 자동 변환 하는 경우 후자를 이용

```python
from sklearn.preprocessing import LabelEncoder
classle = LabelEncoder()
```

</br>


### 3️⃣ 데이터 분할

학습 데이터 (train) 과 시험 데이터 (test) 가 서로 겹치지 않도록 분할하는 것 

✔ 데이터 분할의 목적

학습데이터로 자료를 학습시키고 학습에 전혀 사용하지 않은 시험데이터에 적용하여 학습 결과의 일반화가 가능한지 알아보기 위함

→ 모델이 과적합 (overfitting)되었다면, validation 셋으로 검증 시 예측율이나 오차율이 떨어지는 형상이 나타난다.

```python
from sklearn.model_selection import train_test_split
x_train, x_test, y_train, y_test 
	= train_test_split(x, y, test_size=0.3, random_state=1, stratify=y)
```

`test_size`  테스트 셋 구성의 비율 → 전체 데이터 셋의 30%를 test (validation)셋으로

`shuffle`  split 하기 전 섞을 건지 여부. default = True, 보통의 경우 default값 사용

`stratify`  default = none, stratify 값을 target으로 지정해주면 각각의 class 비율을                                                  train / variation에 유지해 준다. → 옵션 미지정시 성능차이가 날 수 있다.

`random_state`  하이퍼 파라미터를 튜닝 시 이 값을 고정해두고 튜닝해야 매번 데이터셋이 변경되는 것을 방지 할 수 있다. 

</br>


### 4️⃣ (옵션) 입력데이터의 표준화

✔ 표준화

특정 자료의 측정 단위 (Scaling)에 영향을 받지 않도록 하는 과정

Standard Sclaer 클래스를 활용

시험 데이터의 표준화는 학습 데이터에서 구한 특성 변수의 평균과 표준편차를 이용 !

주의) 표준화로 인해 데이터의 분포인 통계적 특성이 깨지면 머신러닝의 학습저하가 생김

→ 표준화의 여부는 시험데이터의 정밀도(accuracy)를 정검하여 결정한다 !

```python
from sklearn.preprocessing import StandardScaler
sc = StandardScaler()
# 학습데이터(train)을 통해 특성 변수의 평균과 표준편차
sc.fit(train)
# 시험데이터(test)에 적용
test_std = sc.transform(test)
```

</br>


### 6️⃣ 결과 분석

분류문제는 회귀 분석과 달리 다양한 성능 평가 기준 (metric)이 필요하다

✔  혼합 행렬 (confusion matrix) 

타겟의 원래 클래스와 모형이 예측한 클래스가 일치하는지 갯수로 센 결과를 나타낸 표 

![Untitled](https://user-images.githubusercontent.com/88828858/182009473-54636dd2-6cdd-4487-bd5f-f871327b6530.png)



```python
from sklearn.metrics import confusion_metrics
conf = confusion_metrics(y_true=y_test, y_pred=y_test_pred)
```

✔ 정확도 점수 (accuracy score)

```python
from sklearn.metrics import accuracy_score
accuracy_score(y_true, y_pred)
# accuracy_score(y_true, y_pred, nomalize=False)
```

`nomalize`  default = True :  정확도를 비율 (소수점), False :  맞은 샘플의 개수로 표시
