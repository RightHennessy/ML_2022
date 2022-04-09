# Pandas 라이브러리

### 데이터프레임

🔅 열 (columns), 인덱스 (index), 값 (value)으로 구성

```python
import pandas as pd
```
<br/>
🔅 DataFrame ( values = 필수, index = 옵션, columns = 옵션 )

```python
values = [[1, 2, 3], [4, 5, 6], [7, 8, 9]] 
index = ['one', 'two', 'three']
columns = ['A', 'B', 'C']

df = pd.DataFrame(values, index=index, columns=columns)
df
```

|  | A | B | C |
| --- | --- | --- | --- |
| one | 1 | 2 | 3 |
| two  | 4 | 5 | 6 |
| three | 7 | 8 | 9 |

<br/>

```python

# DataFrame 옵션 생략하여 출력해보기

values = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
df = pd.DataFrame(values)
df
```

|  | 0 | 1 | 2 |
| --- | --- | --- | --- |
| 0 | 1 | 2 | 3 |
| 1  | 4 | 5 | 6 |
| 2 | 7 | 8 | 9 |

<br/>

🔅 리스트로 데이터 프레임 생성 

```python
data = [
    ['1000', 'Steve', 90.72], 
    ['1001', 'James', 78.09], 
    ['1002', 'Doyeon', 98.43], 
    ['1003', 'Jane', 64.19], 
    ['1004', 'Pilwoong', 81.30],
    ['1005', 'Tony', 99.14],
]

df = pd.DataFrame(data)
df
```

|  | 0 | 1 | 2 |
| --- | --- | --- | --- |
| 0 | 1000 | Steve | 90.72 |
| 1  | 1001 | James | 78.09 |
| 2 | 1002 | Doyeon | 98.43 |
| 3 | 1003 | Jane | 64.19 |
| 4 | 1004 | Pilwoong | 81.30 |
| 5 | 1005 | Tory | 99.14 |

<br/>

```python
# 열 이름 지정해주기

df = pd.DataFrame(data, columns=['학번', '이름', '점수'])
df
```

|  | 학번 | 이름 | 점수 |
| --- | --- | --- | --- |
| 0 | 1000 | Steve | 90.72 |
| 1  | 1001 | James | 78.09 |
| 2 | 1002 | Doyeon | 98.43 |
| 3 | 1003 | Jane | 64.19 |
| 4 | 1004 | Pilwoong | 81.30 |
| 5 | 1005 | Tory | 99.14 |

<br/>

🔅 딕셔너리로 데이터 프레임 생성하기

```python
# 딕셔너리로 판다스 생성하기
data = {
    '학번' : ['1000', '1001', '1002', '1003', '1004', '1005'],
    '이름' : [ 'Steve', 'James', 'Doyeon', 'Jane', 'Pilwoong', 'Tony'],
    '점수': [90.72, 78.09, 98.43, 64.19, 81.30, 99.14]
    }

df = pd.DataFrame(data)

# 만약 다시 판다스를 딕셔너리로 변경
df2dic = df.to_dict()
```

<br/>

🔅 데이터 프레임 조회

```python
# 앞 부분을 3개만 보기
df.head(3)

# 뒷 부분을 3개만 보기
df.tail(3)

# 학번에 해당하는 열 확인
# dtype 을 확인해보면 학번은 정수인것 처럼 보이지만 문자열 이다 !
df['학번']
```

<br/>

### 외부 데이터 읽기

```python
# 데이터프레임은 항상 인덱스가 자동으로 부여되기 때문에 저장할 때 index 저장을 제외해야함 !
# 그렇지 않으면 인덱스가 여러번 저장 ( index 의 default = True )

df.to_csv('example.csv', index=False)
```

<br/>

🔅 데이터프레임 삭제

```python
# drop( [삭제할 인덱스 명], axis) -> axis = 0 : 행, axis = 1 : 열

df_ = df.drop(["학번"], axis=1)

# 2개 동시 -> 반드시 [ ]로 묶어주기 !

df_ = df.drop(["학번", "이름"], axis=1)
```

<br/>

### 인덱스 조회 (row, 행 기준)

🔅  `loc`  인덱스 명을 이용하여 접근, `iloc`  인덱스 번호를 이용하여 접근

```python
# 숫자로 된 인덱스 명 -> 숫자로 접근 가능
df.loc[1]
df.iloc[1]
```

학번     1001
이름    James
점수    78.09
Name: 1, dtype: object

```python
# 슬라이싱
df.loc[0:1]
```

|  | 학번 | 이름 | 점수 |
| --- | --- | --- | --- |
| 0 | 100 | Steve | 90.72 |
| 1  | 1001 | James | 78.09 |

<br/>

🔅 kolumn, 열 기준 익덱스 데이터 조회

```python
df.loc[0:5], ['학번']]
```

|  | 학번 |
| --- | --- |
| 0 | 1000 |
| 1  | 1001 |
| 2 | 1002 |
| 3 | 1003 |
| 4 | 1004 |
| 5 | 1005 |

<br/>

```python
df.iloc[0:5, 0]
```

0    1000
1    1001
2    1002
3    1003
4    1004
Name: 학번, dtype: object

<br/>

```python
df.iloc[0:5, 0:0]
```

|  |
| --- |
| 0 |
| 1  |
| 2 |
| 3 |
| 4 |

<br/>

🔅 `at` 값만 반환

```python
df.at[0, '학번']
```

‘1000’

<br/>

### 조건식

`AND(&)`  `OR(|)`  `isin()`

```python
# 점수가 80 이상인지 True False로 표기
df['점수']>80
```

0     True
1    False
2     True
3    False
4     True
5     True
Name: 점수, dtype: bool

<br/>

```python
# f['점수']>80 : Ture 인경우만 -> df에 다시 넣어줌
df[df['점수']>80]
```

|  | 학번 | 이름 | 점수 |
| --- | --- | --- | --- |
| 0 | 1000 | Steve | 90.72 |
| 2 | 1002 | Doyeon | 98.43 |
| 4 | 1004 | Pilwoong | 81.30 |
| 5 | 1005 | Tory | 99.14 |

<br/>
<br/>

# 프로파일링

### EDA(Exploratory Data Analysis, 탐색적 데이터 분석)

좋은 머신러닝 결과를 얻기 위해서는 데이터의 성격을 파악하는 과정이 선행되어야 한다. 

데이터 내 값의 분포, 변수 간의 관계, Null 값과 같은 결측값(missing values) 존재 유무 등의 데이터를 파악하는 과정을 EDA라 한다.

<br/>

### 프로파일링

방대한 양의 데이터를 가진 데이터 프레임을 단 한줄의 명령으로 탐색하는 패키지

<br/>

```python
# 판다스 프로파일링 설치
! pip install -U pandas-profiling

import pandas as pd
import pandas_profiling

# 프로파일링에 사용할 데이터를 가져오는 법
! wger [주소]
data = pd.read_csv('spam.csv')

# 프로파일링 시작 
data.profile_report()
```

<br/>

### 분석하기

![pansdas-1](https://user-images.githubusercontent.com/88828858/162556717-0412b298-1c23-416b-a478-56a1b0df8817.png)

Missing cells : 결측값

<br/>

![pansdas-2](https://user-images.githubusercontent.com/88828858/162556727-781522be-74e0-4ea2-bcdc-5263ea412809.png)

Unanamed : 99% 이상이 missing 으로 예상

<br/>

![pansdas-3](https://user-images.githubusercontent.com/88828858/162556739-a7b7723f-44ce-46e5-beb6-a67332ed80d3.png)

variable에서 missing 된 값은 있는지, 몇개의 종류로 나눠졌는지 확인 가능

<br/>

![pansdas-4](https://user-images.githubusercontent.com/88828858/162556744-c8fb637c-87b0-4552-a823-992a8d451b51.png)

Toggle details → Categories
