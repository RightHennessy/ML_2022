# SVM

# Linear SVM : 선형 SVM


[노션 보러가기](https://www.notion.so/SVM-12787a940ec54262b37947c81b1c38d4)


### **SVM : Supprot Vector Machine**

패턴 인식, 자료분석을 위한 지도 학습 모델

분류와 회귀 문제에 사용 ( 주로 분류 문제 사용)

두 카테고리 중 어느 하나에 속한 데이터의 집합이 주어졌을 때, 주어진 데이터 집할을 바탕으로 하여 새로운 데이터가 어느 카테고리에 속할 지 판단하는 비-확률적 이진 선형 분류 모델

커널 트릭을 활용하여 비선형 분류 문제에도 사용 가능하다. 

</br>

### **학습 방향 : 마진(Margin)의 최대화**

경계 결계 (hyperplane)는 주변 데이터와의 거리가 최대가 되어야 함.

![Untitled](https://user-images.githubusercontent.com/88828858/182009846-9faea4d0-154e-4cd8-982a-2bf25dedd366.png)
![Untitled 1](https://user-images.githubusercontent.com/88828858/182009788-275dbd3e-c8c2-4ff1-9485-932d27e787ea.png)


</br>

### 용어

✔ 결정 경계 (Hyperplane) : 서로 다른 크래스를 완벽하게 분류하는 기준

✔ 서포트 벡터 (Support vector) : 결정 경계선에 가장 가까이에 있는 각 클래스의 데이터 

✔ 마진 (Margin) : 어떤 데이터도 포함하지 않는 영역, 서포트 벡터와 직교하는 직선과의 거리 

</br>

### 결정 경계 (Hyperplane)

데이터 임베딩 공간보다 1차원 낮은 부분공간

예) 2차원 데이터 공간의 결정 경계 : 직선

3차원 데이터 공간의 결정 경계 : 평면

4차원 이상 데이터 공간의 결정 경계 : 초평면

</br>

### 수학적 표현

![Untitled 2](https://user-images.githubusercontent.com/88828858/182009791-8c4dc816-540a-46cd-ba48-9ecc76c0111b.png)
![Untitled 3](https://user-images.githubusercontent.com/88828858/182009797-8078f0ab-dacb-4b89-ac79-e539b9b2e11b.png)
![Untitled 4](https://user-images.githubusercontent.com/88828858/182009798-2bd8beb9-0f2f-44f3-aa31-a9d29e1f2a84.png)

</br>

### Hard Margin SVM의 목적 함수

✔ 마진의 최대화 

![Untitled 5](https://user-images.githubusercontent.com/88828858/182009799-2bdb0ac6-c9f5-4966-8c6e-4c16166d2b4f.png)
![Untitled 6](https://user-images.githubusercontent.com/88828858/182009800-2bbbe88c-258e-487f-9bad-805dac4c572b.png)
![Untitled 7](https://user-images.githubusercontent.com/88828858/182009802-63b632ee-7e13-44c8-ab75-bb45626f403f.png)

</br>

### (W, b, α)가 Langrangian dual problem의 최적해가 되기 위한 조건

✔ KKT (Karush-Kuhn-Tucker) Conditions

![Untitled 8](https://user-images.githubusercontent.com/88828858/182009803-4947031b-af07-47a6-a815-7e900780f6d6.png)

</br>

### Hard margin SVM vs Soft Margin SVM

✔ Hard Margin SVM : 선형 분리 가능한 문제

✔ Soft Margin SVM : 선형 분리 불가능한 문제 - 학습데이터의 에러가 0이 되도록 완벽하게 나누는 것이 불가능 → 에러를 허용하자 !

⁖ suppor vector : 마진을 결정 

![Untitled 9](https://user-images.githubusercontent.com/88828858/182009804-d7c7ae2a-28a0-45c9-9d0b-9b80f3660a8b.png)
![Untitled 10](https://user-images.githubusercontent.com/88828858/182009805-5492dad5-a824-4ceb-9e6d-4a0fd541fe4d.png)

</br>

### Soft Margin SVM의 목적함수

: 에러(penalty term)을 허용하면서 Margin을 최대화 

✔ C를 통해 에러의 허용정도를 조절

 → C가 크면  학습 에러를 상대적으로 허용하지 않음 (Overfitting) → 마진이 작아짐

 → C가 작으면  학습 에러를 상대적으로 허용 (Underfitting) → 마진이 커짐

![Untitled 11](https://user-images.githubusercontent.com/88828858/182009807-2f1d31b2-8903-4f36-9c9b-9e6d4a4a9f4f.png)
![Untitled 12](https://user-images.githubusercontent.com/88828858/182009808-88e28f29-4f86-483b-bd12-5be2daf1e8ed.png)
![Untitled 13](https://user-images.githubusercontent.com/88828858/182009809-69bb4575-3ef9-42fc-a944-bd8a65700b73.png)


</br>

### Hard Margin과 Soft Margin

![Untitled 14](https://user-images.githubusercontent.com/88828858/182009810-41f0e686-437f-4305-9cbe-cc35d98f2094.png)

</br>

# Nonlinear SVM : 비선형 SVM

### 선형 SVM vs 비선형 SVM

✔ 선형 SVM : Hard margin SVM, Soft Margin SVM

✔ 비선형 SVM : Kernel SVM

![Untitled 15](https://user-images.githubusercontent.com/88828858/182009811-b45c1ecc-1c55-4e66-ae58-e462c51cbf5e.png)

</br>

### 비선형 SVM

데이터를 선형으로 분류하기 위해 차원을 높이는 방법을 사용

Feature Map(Φ) 을 통해 차원을 높임. 즉, x 대신 Φ(X)를 사용

커널 : Feature Map의 내적  Φ(X)•Φ(Y)

![Untitled 16](https://user-images.githubusercontent.com/88828858/182009812-4bc14109-4cef-4d6b-a844-eb7c314ada61.png)

</br>

### 비선형 SVM의 해법

SVM 모델을 Original Space가 아닌 Feature Space에서 학습 ( X → Φ(X) )

Transfer : Original space - Nonlinear decision boundary →  Feature space - linear decision boundary

고차원 Feature space에서는 분류가 더 쉬울 수 있음을 입증 

👇 고차원 Feature space를 효율적으로 계산할 수 있는 방법 

![Untitled 17](https://user-images.githubusercontent.com/88828858/182009813-5f7fb662-272c-4020-b9d1-020188445a9c.png)

</br>

### 비선형 SVM의 목적함수

![Untitled 18](https://user-images.githubusercontent.com/88828858/182009814-06587866-2ea2-4be6-ad6a-fbf3efcb3ac0.png)

</br>

### Kernel Mapping의 예

![Untitled 19](https://user-images.githubusercontent.com/88828858/182009815-a06318da-fbfc-415b-8056-4974ea0e9474.png)

✔ 커널 사용을 통해 명시적(explicitly)으로 Φ(X), Φ(Y)를 각각 계산하지 않고 암묵적(implicitly)으로     <Φ(X),Φ(Y)>를 바로 계산하여 연산 효율을 높일 수 있다.

![Untitled 20](https://user-images.githubusercontent.com/88828858/182009816-86ad92d5-838d-4e6c-a462-047784e9306f.png)

</br>

### Kernel Function의 예

![Untitled 21](https://user-images.githubusercontent.com/88828858/182009817-56ef790a-2d28-4a5f-b6df-38753809337e.png)

⁛ 아직 어떤 kernel의 성능이 더 우수하다 이런것은 없다. 

</br>

### 비선형 SVM의 예시

![Untitled 22](https://user-images.githubusercontent.com/88828858/182009818-8ab20c16-562b-4fd7-b659-3e75923a086c.png)

: 선형 분류가 불가능 하므로 Kernel 적용

: Low degree polynomial kernel function 사용 - K(x,y) = (xy+1)²

: Tuning parameter - C=100

</br>

### 비선형 SVM의 α 계산

![Untitled 23](https://user-images.githubusercontent.com/88828858/182009819-50751ec3-6b29-4e29-aa19-c07463a45ca4.png)

α₂, α₄, α₅ : hyperplane을 결정짓는 support vector

- α_i ≠ 0 → α_i>0, x_i → SV

- α_i = 0 → x_i ≠ SV 

</br>

### 비선형 SVM의 α 계산 → b 계산 → 모델 학습 완료

![Untitled 24](https://user-images.githubusercontent.com/88828858/182009820-37a06c90-a892-4722-ac8f-474b784a364d.png)


ἱ ∈ { α₂, α₄, α₅ }

f(x) 에 값 대입 후 → f(x) > 0 이면 1 class / f(x) < 0 이면 -1 class

</br>

### 비선형 SVM의 kernel 선정법

 SVM kernel을 결정하는 것은 어려운 문제이다. (정해진 기준이 없으므로 실험적으로 결정해야함.)

사용하는 kernel에 따라 feature space의 특징이 달라지기 때문에 데이터의 특성에 맞는 kernel을 결정하는 것은 중요하다. 

 → 일반적으로 RBF Kernel, Sigmoid Kernel, Low Degree Polynomial Kernel(4차미만) 등이 주로 사용.
 
 </br>

✔ 커널에 따른 분류 결과

![Untitled 25](https://user-images.githubusercontent.com/88828858/182009822-c0e2dae0-a8f7-4f03-a22d-583835c8fc21.png)

test error를 확인해 보면 오른쪽의 RBF가 test error가 작으므로 성능이 더 좋다. 

</br>

# SVM 다계층 분류 : Multi Classification

✔ 하나-나머지 방법 (One-vs-Rest)

: 이항 분류 값(hypothesis function)이 가장 큰 값을 그룹으로 할당 

  → 확률이 가장 높은 값으로 class 결정

  → 본인만 1, 나머지는 -1로 통일 ⇒ 분류기가 class의 수만큼 필요 !

✔ 하나-하나 방법 (One-vs-One)

: 주어진 특성 자료에 대해 가장 많이 할당된 그룹으로 할당 - voting 방식

  → nC₂ 개의 분류기가 필요 !

![Untitled 26](https://user-images.githubusercontent.com/88828858/182009823-b001f6cc-7e4e-4186-91ff-3e6fe8703163.png)

</br>

## 💻실습해보기

### 정리

**SVM 분류기**

 : 이진분류기, deep learning 이전 아주 널리 사용되던 기법

✔ 선형 SVM - Hard Margin SVM : 완전히 분류 가능

                      - Soft Margin SVM : error가 많은 경우 error를 허용

✔ 비선형 SVM : 차원을 높여서 해결,  X → Φ(X) ⇒ 커널을 도입

</br>

**parameter**

✔ C : Soft Margin SVM에서 사용 - 얼마나 error를 허용할 것인가?

✔ kernel : linear, poly, RBF, sigmoid

✔ ovo, ovr : 다중 분류기로 확장시킬 때 사용

</br>

### SVC와 SVR 추후 수정 예정.. 😥
