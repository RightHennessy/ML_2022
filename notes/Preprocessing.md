# Preprocessing : 데이터 전처리

### 데이터 전처리 과정

1) 데이터 실수화: 컴퓨터가 이해할 수 있는 값으로의 변환

2) 불완전한 데이터 제거: NULL, NA, NAN 값의 제거

3) 잡음 섞인 데이터 제거

: 가격 데이터에 있는 (-) 값 제거 - 가격이 -100원인 경우
: 연령 데이터 중 과도하게 큰 값 제거 - 나이 값으로 200, 300, 400 등의 값이 존재하는 경우

4) 모순된 데이터 제거 : 남성 데이터 중 주민번호가 ‘2’로 시작하는 경우

5) 불균형 데이터 해결 : 과소표집(undersampling), 과대표집(oversampling)

### 데이터 전처리의 주요 기법

1️⃣ 데이터 실수화 (Data Vectorization)

범주형 자료, 텍스트 자료, 이미지 자료 등을 실수로 구성된 형태로 전환하는 것

2️⃣ 데이터 정제 (Data Cleaning)

없는 데이터는 채우고, 잡음 데이터는 제거하고, 모순 데이터를 올바른 데이터로 교정하는 것

3️⃣ 데이터 통합 (Data Integration)

여러 개의 데이터 파일을 하나로 합치는 과정

4️⃣ 데이터 축소 (Data Reduction)

데이터가 과도하게 큰 경우, 분석 및 학습에 시간이 오래 걸리고 비효율적이기 때문에 데이터의 수를 줄이거나(Sampling), 데이터 차원을 축소하는 작업

5️⃣ 데이터 변환 (Data Transformation)

데이터를 정규화 하거나, 로그를 씌우거나, 평균값을 계산하여 사용하거나, 사람 나이 등을 10대, 20대, 30대 등으로 구간 화 하는 작업

6️⃣ 데이터 균형 (Data Balancing)

특정 클래스의 관측치가 다른 클래스에 비해 매우 낮을 경우 샘플링을 통해
클래스 비율을 맞추는 작업

### 1️⃣ 데이터 실수화

✔ 자료의 유형

연속형 자료 (Continuous data), 범주형 자료 (Categorical data), 텍스트 자료 (Text data)

**범주형 자료의 실수화** 

✔ One-hot encoding 을 이용한 데이터 실수화

![Untitled](Preprocessing%20%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%84%90%E1%85%A5%20%E1%84%8C%E1%85%A5%E1%86%AB%E1%84%8E%E1%85%A5%E1%84%85%E1%85%B5%20cfdb705028624e4ab6d62c815e655c1d/Untitled.png)

✔ Scikit-learn의 `DictVectorizer` 함수

범주형 자료의 실수화 하는 함수

Input argument : 디폴트 옵션 Sparse=True → 눈으로 확인하기 위해서는 False로 설정

```python
# 범주형 자료의 수량화 
x = [{'city':'seoul', 'temp':10.0}, {'city':'Dubai', 'temp':33.5}, {'city':'LA', 'temp':20.0}]
x

from sklearn.feature_extraction import DictVectorizer
vec = DictVectorizer(sparse=False)
vec.fit_transform(x)
```

[ {'city':'seoul', 'temp':10.0}, 
  {'city':'Dubai', 'temp':33.5}, 
  {'city':'LA', 'temp':20.0} ]

array( [ [ 0. , 0. , 1. , 10. ],
            [1. , 0. , 0. , 33.5 ],
            [ 0. , 1. , 0. , 20. ] ] )

✔ 희소행렬(Sparse Matrix)

행렬의 값이 대부분 0인 경우를 가리키는 경우

 → 불필요한 0 값으로 인해 메모리 낭비가 심하고 행렬의 크기가 커서 연산시 시간도 많이 소모

 → COO표현식과 CSR표현식을 통해 문제 해결 가능

👉 CSR 표현식 (Compressed Sparse Row)

 : COO형식에 비해 메모리가 적게 들고 빠른 연산이 가능함

```python
velc = DictVectorizer(sparse=True)  #메모리를 줄이기 위해 
x1 = vecl.fit_transform(x)
x1
```

<3x4 sparse matrix of type ‘<class ‘numpy.float64’>’ with 6 stored elements in Compressed Sparse Row format>

**텍스트 자료의 실수화** 

✔ 단어의 출현 횟수를 이용한 데이터 실수화

![Untitled](Preprocessing%20%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%84%90%E1%85%A5%20%E1%84%8C%E1%85%A5%E1%86%AB%E1%84%8E%E1%85%A5%E1%84%85%E1%85%B5%20cfdb705028624e4ab6d62c815e655c1d/Untitled%201.png)

```python
# 텍스트 자료의 수량화 
text = ['떴다 떴다 비행기 날아라 날아라',
				'높이 높이 날아라 우리 비행기',
			  '내가 만든 비행기 날아라 날아라',
			  '멀리 멀리 날아라 우리 비행기']
text
```

[ '떴다 떴다 비행기 날아라 날아라',
  ‘높이 높이 날아라 우리 비행기’,
  ‘내가 만든 비행기 날아라 날아라’,
  ‘멀리 멀리 날아라 우리 비행기’]

```python
from sklearn.feature_extraction.text import CountVectorizer
vec2 = CountVectorizer()
t = vec2.fit_transform(text).toarray() #sparse=True를 풀고 text를 수량화 배열 자료로 변환

import pandas as pd
t1 = pd.DataFrame(t, columns=vec2.get_feature_means())
t1
```

![Untitled](Preprocessing%20%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%84%90%E1%85%A5%20%E1%84%8C%E1%85%A5%E1%86%AB%E1%84%8E%E1%85%A5%E1%84%85%E1%85%B5%20cfdb705028624e4ab6d62c815e655c1d/Untitled%202.png)

BUT 출현 횟수가 정보의 양과 비례하는 것은 아니다. → TF-IDF 기법을 이용

TF-IDF(Term Frequency Inverse Document Frequency)

 : 자주 등장하여 분석에 의미를 갖지 못하는 단어의 중요도를 낮추는 기법 (예) The, a 등의 관사

→ 가중치 재계산, 높은 빈도에 낮은 가중치, 낮은 빈도에 높은 가중치

```python
from sklearn.feature_extraction.text import TfidVectorizer
tfid = TfidVectorizer()
x2 = tfid.fit_transform(text).toarray()
x3 = pd.DataFrame(x2, columns = tfid.get_feature_names())
x3
```

![Untitled](Preprocessing%20%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%84%90%E1%85%A5%20%E1%84%8C%E1%85%A5%E1%86%AB%E1%84%8E%E1%85%A5%E1%84%85%E1%85%B5%20cfdb705028624e4ab6d62c815e655c1d/Untitled%203.png)

### 2️⃣ 데이터 정제

✔ 결측 데이터 채우기

결측 데이터 : np.nan, npNaN, None

→ 평균(mean), 중위수(median), 최빈수(most frequent value)로 대처하는 기법 사용

```python
# 결측자료 대체
x_miss = np.array([[1,2,3,None], [5,np.NAN,7,8], [None,10,11,12], [13,np.nan,15,16]])

from sklearn.impute import SimpleImputer
im = Imputer(strategy='mean') # 열(세로기준)의 평균값으로 null 값 대체
im.git_transfer(x_miss)
```

`impruter()`  입력 인자로 평균, 중위수, 최빈수 선택 가능하다. 

### 3️⃣ 데이터 통합

여러개의 데이터 파일을 하나로 합치는 과정 : pandas의 `merge()`  사용

`.dtypes` 나 `.unique()`  로 자료 타입을 확인해 보자 !

### 5️⃣ 데이터 변환

✔ 필요성

머신러닝은 데이터가 가진 특성(Feature)들을 비교하여 데이터 패턴을 찾는다.

→ 데이터가 가진 특성 간 스케일 차이가 심하면 패턴을 찾는데 문제가 발생함

✔ 방법

1) 표준화 : Standardization

![Untitled](Preprocessing%20%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%84%90%E1%85%A5%20%E1%84%8C%E1%85%A5%E1%86%AB%E1%84%8E%E1%85%A5%E1%84%85%E1%85%B5%20cfdb705028624e4ab6d62c815e655c1d/Untitled%204.png)

2) 정규화 : Nomarlization

![Untitled](Preprocessing%20%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%84%90%E1%85%A5%20%E1%84%8C%E1%85%A5%E1%86%AB%E1%84%8E%E1%85%A5%E1%84%85%E1%85%B5%20cfdb705028624e4ab6d62c815e655c1d/Untitled%205.png)

⭐ 정규화가 표준화보다 유용하다. 
     단, 데이터 특성이 bell-shape 이거나 이상치가있을 경우에는 표준화가 유용함

### 6️⃣데이터 균형

✔ 데이터 불균형이란?

머신러닝의 목적이 분류 일 때, 특정 클래스의 관측치가 다른 클래스에 비해 매우 낮게 나타나면 이러한 자료를 불균형자료라고 한다.

![Untitled](Preprocessing%20%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%84%90%E1%85%A5%20%E1%84%8C%E1%85%A5%E1%86%AB%E1%84%8E%E1%85%A5%E1%84%85%E1%85%B5%20cfdb705028624e4ab6d62c815e655c1d/Untitled%206.png)

✔데이터 불균형 해소 기법

좌 : 과대표집(oversampling), 우 : 과소표집(undersampling)

→ 일반적으로 과소표집보다 과대표집이 통계적으로 유용하다.

→ 의사결정나무(decision tree)와 앙상블(ensemble)은 상대적으로 불균형자료에 강인한 특성을 보임

✔ 과소표집(undersampling)

다수클래스의 표본을 임으로 학습데이터로부터 제거하는 것

✔ 과대표집(oversampling)

소수클래스의 표본을 복제하여 이를 학습데이터에 추가하는 것

대표적인 방법론 : SMOTE(Synthetic minority oversampling technique)
                             ADASYN(adaptive synthetic sampling method)

```python
import imblearn.over_sampling import SMOTE, ADASYN

sm = SMOTE(random_state=42)
X_res, y_res = sm.fit_transform(X, y)

ada = ADASYN(random_state=0)
X_syn, y_syn = ada.fit_transform(X, y)

import imblearn.under_sampling import NearMiss
undersample = NearMiss(version=3, n_neighbors_ver3=3)
X_Under, y_Under = undersample.fit_transform(X, y)
```

![Untitled](Preprocessing%20%E1%84%83%E1%85%A6%E1%84%8B%E1%85%B5%E1%84%90%E1%85%A5%20%E1%84%8C%E1%85%A5%E1%86%AB%E1%84%8E%E1%85%A5%E1%84%85%E1%85%B5%20cfdb705028624e4ab6d62c815e655c1d/Untitled%207.png)