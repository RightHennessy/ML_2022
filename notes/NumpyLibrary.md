# Numpy 라이브러리

Numerical Python, 수치 데이터를 다루는 파이선 패키지

넘파이 배열 (ndarray) : 다차원 배열 자료구조. 벡터, 행렬 등 연산을 빠르게 계산

### 넘파이 라이브러리 불러오기

```python
import numpy as np
```

### np.array()

🔅 리스트, 튜플, 배열 → ndarray 생성

```python
# 1차원 배열 - 리스트로 만들기

vec = np.array([1,2,3,4,5])
print(vec)
```

[1 2 3 4 5]

```python
# 2차원 배열 - 리스트로 만들기

mat = np.array([[1,2,3], [4,5,6]])
print(mat)
```

[[1 2 3] [4 5 6]]

 

🔅 배열의 크기 확인하기

```python
# 축의 개수 출력 : ndim, 배열 크기 출력 : shape

vec.ndim
vec.shape
mat.ndim
mat.shape
```

1

(5, )

2

(2, 3)

### ndarray 초기화

🔅 ndarray를 만드는 다양한 방법

```python
# np.zeros() : 배열의 모든 원소에 0 삽입

zero_mat = np.zero((2,3))
print(zero_mat)

# np.ones() : 배열의 모든 원소에 1 삽입

one_mat = np.ones((2,3))
print(one_mat)

# np.full() : 배열의 모든 원소에 사용자 지정 값 삽입

same_mat = np.full((2,2), 7)
print(same_mat)

# np.random.random() : 임의의 값을 가지는 배열 생성 
# 시드 값을 고정해야 실행마다 같은 랜덤값 생성

random_mat = np.random.random((2,2)) 
```

[[0 0 0 ] [0 0 0]]

[[1 1 1 ] [1 1 1]]

[[7 7 ] [7 7]]

### np.arrange()

🔅 0부터 n-1 값을 가지는 배열 생성

```python
range_vec = np.arange(10)
print(range_vec)

# 배열 인터벌 지정 가능
n=2
range_n_step_vec = np.arange(1, 10, n)
print(range_n_step_vec)
```

[0 1 2 3 4 5 6 7 8 9]

[1 3 5 7 9]

### np.reshape()

🔅 내부  데이터 변경 없이 배열의 구조 변화

```python
reshape_mat = np.array(np.arange(30)).reshape((5,6))
print(reshape_mat)
```

[[ 0 1 2 3 4 5 ] 

 [ 6 7 8 9 10 11 ]

 [ 12 13 14 15 16 17 ]

 [ 18 19 20 21 22 23 ]

 [ 24 25 26 27 28 29] ] 

### Numpy 슬라이싱

```python
mat = np.array([[1, 2, 3], [4, 5, 6]])
print(mat)

# [행, 열]을 의미하며, 해당하는 행 또는 열을 슬라이싱하여 출력

slicing_mat = mat[0, :]
print(slicing_mat)

slicing_mat = mat[:, 1]
print(slicing_mat)
```

[[ 1 2 3 ]

 [ 4 5 6 ]]

[ 1 2 3 ]

[ 2 5]

### Numpy 정수 인덱싱

🔅 연속적이지 않은 원소로 배열을 만들 경우 슬라이싱 불가 → 인덱싱 사용

```python
mat = np.array([[1, 2], [4, 5], [7, 8]])
print(mat)
```

[[ 1 2 ]

 [ 4 5 ]

 [ 7 8 ]]

🔅 주의 : 행끼리, 열끼리 모아 값을 입력 받음

```python
# mat [[행, 행, 행], [열, 열, 열]]
# (2,1) 과 (0,1)을 불러오는 것이 아닌 (2,0), (1,1) 불러오는 것
indexing_mat = mat[[2, 1],[0, 1]]
print(indexing_mat)

# 이거는 (1,0), (1,1), (2,0) 을 불러서 저장
indexing_mat2 = mat[[1,1,2],[0,1,0]]
print(indexing_mat2)
```

[ 7 5 ]

[ 4 5 7 ]

### Numpy 연산

🔅 연산자 또는 함수 이용하여 배열 간 연산 수행 가능

```python
# 덧셈
result = x + y
result = np.add(x, y)

# 뺄셈
result = x - y
result = np.subtract(x, y)

# 곱셈
result = result * x
result = np.multiply(result, x)

# 나눗셈
result = result / x
result = np.divide(result, x)
```

🔅 행렬곱 (dot)

```python
mat1 = np.array([[1,2],[3,4]])
mat2 = np.array([[5,6],[7,8]])
dot_mat = np.dot(mat1, mat2)
print(dot_mat)
```

[[ 19 22 ]

 [ 43 50 ]]