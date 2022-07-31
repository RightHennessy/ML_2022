# 기말고사

## 데이터 전처리

**데이터 전처리 과정**

1. 데이터 실수화
2. 불완전한 데이터 제거
3. 잡음 섞인 데이터 제거 예)과도하게 큰 나이 200살 가격 -100원
4. 모순된 데이터 제거 예) 남자 주민번호 2
5. 불균형 데이터 해결

**데이터 전처리의 주요 기법**

1. 데이터 실수화
2. 데이터 정제
3. 데이터 통합
4. 데이터 축소 : 데이터 수 줄이기 Sampling, 데이터 차원 축소
5. 데이터 변환 : 정규화, 로그, 평균값, 구간화
6. 데이터 균형

**범주형 자료의 실수화**

1. one-hot encoding
2. dictVectorizer
3. gmlthgodfuf → COO형식에 비해 CRS형식이 적은 메모리, 빠른 연산

**텍스트 자료의 실수화**

TF-IDF(Term Frequency~) : 자주등장하여 분석에 의미를 갖지 못하는 단어의 중요도 낮춤

countVectorize : 단어의 출현 횟수를 이용한 데이터 실수화

**데이터 변환**

정규화(Normalization)가 표준화(Standardization)보다 유용하다. 

예외) 테이터 특성이 bell-shape이거나 이상치가 있는 경우 표준화가 유용

**데이터 불균형**

머신러닝의 목적이 분류일때,  특정 클래스의 관측치가 다른 클래스에 비해 매우 낮게 나타나면 → 이러한 자료가 불균형 자료이다.

해소기법 2가지

- 과소표집(undersampling)  - NEARMISS
    
     → 다수클래스의 표본을 임의로 학습데이터로부터 제거
    
- 과대표집(oversampling) : 주로 사용된다 - SMOTE, ADASYN
    
     → 소수 클래스의 표본을 복제하여 이를 학습데이터에 추가
    

불균형 자료에 강인한 특성을 보이는 모델 : 의사결정 나무, 앙상블

 

## SVM

**정의**

패턴 인식, 자료 분석을 위한 지도학습 모델

분류와 회귀문제에 사용 - 주로 분류

비-확률적 이진 선형 분류류 모델

커널트릭을 활용해 비선형 분류 문제에도 사용 가능

학습 방향 : 마진의 최대화

- 결정경계 : 서로 다른 클래스를 완벽하게 분류하는 기준
- 서포트 벡터 : 결정 경계선에 가장 가까이에 있는 각 클래스의 데이터
- 마진 : 어떤 데이터도 포함하지 않는 영역

**SVM 분류기**

- Hard Margin SVM : 선형분리 가능
- Soft Margin SVM : 에러 허용하고 선형으로 분리한다.
- Kernel SVM : 비선형 분리 가능 → 차원을 높이는 방법 사용
    
     종류 : Linear, Polynomial, Sigmoid, Gaussian, RBF
    
- 다계층 분류 : One-vs-Rest(확률이 가장 높은 것) : n
    
                          One-vs-One(voting) : nC2
    

![Untitled](%E1%84%80%E1%85%B5%E1%84%86%E1%85%A1%E1%86%AF%E1%84%80%E1%85%A9%E1%84%89%E1%85%A1%20b84ae7a0fee9478493034a12984fda29/Untitled.png)

## 군집화 : Clustring

**개념**

유사한 속성을 갖는 데이터를 묶어 전체 데이터를 몇개의 군집으로 나누는 것

- 동일한 군집에 소속된 데이터 : 서로 유사할 수록
- 상이한 군집에 소속된 데이터 : 서로 다를 수록

**분류 vs 군집화**

지도학습 vs 비지도 학습

**고려사항**

유사도 측성 시 어떤 거리 측도 사용?

어떤 군집화 알고리즘?

어떻게 최적의 군집수 결정?

어떻게 군집화 결과 평가?

**알고리즘**

1. 계층적 군집화 - 덴드로그램
    
    min max, avg, avg 사이의 평균, ward
    
2. 분리형 군집화
    
    k-means : k 평균 군집화 - 사전에 군집의 수 k 가 정해져야 알고리즘 수행
    
    k개의 중심 임의생성 → 생성된 중심 기준 모든 데이터 군집 할당 
    
    → 각 군집의 중심 계산 → 중심이 변하지 않을때까지 반복
    
    단점) 서로다른 크기, 밀도의 군집을 잘 못찾는다, 지역적 패턴이 존재하는 군집 판별하기 어려움
    
    K값 선정법) Elbow Point, SSE : 군집 내 거리 최소화(만족), 군집 간 거리 최대화(불만족)
    
3. 분포 기반 군집화
    
    DBSCAN : 높은 밀도 → 그룹.  낮은 밀도 → 잡음 
    
    데이터의 e-neighborhood가  M개 이상의 데이터를 포함하는가
    
    핵심자료, 주변자료, 잡음자료
    
    임의데이터 군집1부여 → 임의 데이터의e-NN을 구하고 M보다 작으면 잡음을 부여 → M보다 크면 e-NN 모두 군집 1부여, M보다 큰 것이 없을 떄까지 반복 → 군집 2에대해 동일 반복
    
    e : 너무 작으면 데이터가 잡음, 너무 크면 군집개수가 적음
    

## 차원축소

모든 변수가 서로 독립이라는 가정 하에, 차원의 증가는 모델 성능을 향상

→ 실제로는 모델 성능 저하, 모든 변수는 서로 관계가 있기 때문 ㅋㅋ

**효과**

1. 변수간 상관관계 제거
2. 단순한 후처리
3. 적절한 정보유지하면서 중복되거나 불필요한 변수제거
4. 시각화

**PCA : 주성분 부석**

비지도 학습, 분산을 최대한 보존, 선형

**PCA 알고리즘**

데이터 센터링 : 데이터 평균 =0

→ 최적화 문제 정의

→ 최적화 문제 솔루션

→ 주축 정렬

→ PCA로 변환된 데이터

→ 원데이터로 변환

**PCA 한계**

단일 가우시안인 경우에만 적용 가능

분류 성능 ㅎ향상 보장 못함

## 교차검증

홀드아웃 교차 검증은 좋은 것이 아님!

**과적합 문제**

**과대적합** 너무 일반화

→ 학습데이터 추가 수집

→ 모델 제약 늘리기 : 규제 늘리기

→ 학습 데이터 잡음 줄이기

**과소적합** 너무 단순

→ 파라미터 더 많은 모델 선택

→ 모델 제약 줄이기 : 규약 줄이기

→ 과적합 이전까지 충분히 학습

## 앙상블

여러 분류기를 하나로 연결하여 개별 분류기보다 더 좋은 일반화 성능을 달성하는 것

- 여러 분류 알고리즘 : voting : 동일한 학습 데이터
- 하나의 분류 알고리즘 :
    
    배깅: 알고리즘 수행마다 서로 다른 학습데이터 - 부트스트랩 사용(복원추출) - 랜덤포레스트
    
    부스팅:잘못분류된 데이터 50%재학습에 사용또는 가중치 - adaboost
    

![Untitled](%E1%84%80%E1%85%B5%E1%84%86%E1%85%A1%E1%86%AF%E1%84%80%E1%85%A9%E1%84%89%E1%85%A1%20b84ae7a0fee9478493034a12984fda29/Untitled%201.png)