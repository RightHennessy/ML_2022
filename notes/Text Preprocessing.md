# 텍스트 전처리 Text Preprocessing

# 토큰화 Tokenization

자연어 처리에서 크롤링 등으로 얻어낸 코퍼스 데이터가 필요에 맞게 전처리되지 않은 상태

→ 해당 데이터를 사용하고자하는 용도에 맞게 토큰화 & 정제 & 정규화 과정이 필요

토큰화 : 주어진 코퍼스(corpus)에서 토큰(token)이라 불리는 단위로 나누는 작업

### 단어 토큰화 ****(Word Tokenization)****

토큰의 기준을 단어(word)로 하는 경우

예시 ) 구두점(punctuation)과 같은 문자는 제외시키는 간단한 단어 토큰화 작업. 
구두점 : 마침표(.), 컴마(,), 물음표(?), 세미콜론(;), 느낌표(!) 등과 같은 기호.

입력: Time is an illusion. Lunchtime double so!

출력 : "Time", "is", "an", "illustion", "Lunchtime", "double", "so”

보통 토큰화 작업은 단순히 구두점이나 특수문자를 전부 제거하는 정제(cleaning) 작업을 수행하는 것만으로 해결되지 않는다. 띄어쓰기 단위로 자르면 사실상 단어 토큰이 구분되는 영어와 달리, 한국어는 띄어쓰기만으로는 단어 토큰을 구분하기 어려운 경우가 있다

### 토큰화 중 생기는 선택의 순간

예시 ) 영어권 언어에서 아포스트로피(')가 들어가있는 단어는 어떻게 토큰으로 분류해야 하는가

Don't be fooled by the dark sounding name, Mr. Jone's Orphanage is as cheery as cheery goes for a pastry shop. → “Don’t”, “Jone’s”

NLTK는 영어 코퍼스를 토큰화하기 위한 도구들을 제공

```python
from nltk.tokenize import word_tokenize
from nltk.tokenize import WordPunctTokenizer
from tensorflow.keras.preprocessing.text import text_to_word_sequence

print('단어 토큰화1 :',word_tokenize("Don't be fooled by the dark sounding name, Mr. Jone's Orphanage is as cheery as cheery goes for a pastry shop."))
print('단어 토큰화2 :',WordPunctTokenizer().tokenize("Don't be fooled by the dark sounding name, Mr. Jone's Orphanage is as cheery as cheery goes for a pastry shop."))
print('단어 토큰화3 :',text_to_word_sequence("Don't be fooled by the dark sounding name, Mr. Jone's Orphanage is as cheery as cheery goes for a pastry shop."))
```

단어 토큰화1 : ['Do', "n't", 'be', 'fooled', 'by', 'the', 'dark', 'sounding', 'name', ',', 'Mr.', 'Jone', "'s", 'Orphanage', 'is', 'as', 'cheery', 'as', 'cheery', 'goes', 'for', 'a', 'pastry', 'shop', '.']

→ `word_tokenize` ’s 의 경우에만 제대로 분리

단어 토큰화2 : ['Don', "'", 't', 'be', 'fooled', 'by', 'the', 'dark', 'sounding', 'name', ',', 'Mr', '.', 'Jone', "'", 's', 'Orphanage', 'is', 'as', 'cheery', 'as', 'cheery', 'goes', 'for', 'a', 'pastry', 'shop', '.']

→ `WordPunctTokenizer().tokenize` don’t 와 Jone’s 모두 제대로 분리 

단어 토큰화3 : ["don't", 'be', 'fooled', 'by', 'the', 'dark', 'sounding', 'name', 'mr', "jone's", 'orphanage', 'is', 'as', 'cheery', 'as', 'cheery', 'goes', 'for', 'a', 'pastry', 'shop']

→ `text_to_word_sequence` 모든 알파벳을 소문자로 변경, 아포스트로피를 제외한 구두점 제거

### 토큰화에서 고려해야할 상황

1) 구두점이나 특수 문자를 단순히 제외하면 안된다.  예시) Ph.D, $, 01/02/22

2) 줄임말과 단어 내 띄어쓰기가 존재하는 경우

### 문장 토큰화

단순히 ? . ! 구분하면 안된다. 마침표는 문장의 끝이 아니라도 등장할 수 있기 때문. 

사용하는 코퍼스가 어떤 국적의 언어인지, 해당 코퍼스 내에서 특수문자들이 어떻게 사용되고 있는지 따라 직접 규칙을 정의해서 사용가능하다. 

한국어의 경우에는 문장토큰화 도구로 KSS(Korean Sentence Splitter) 추천

### 한국어에서의 토큰화의 어려움

1) 교착어의 특성

한국어는 어절이 독립적인 단어로 구성되는 것이 아니라 조사 등의 무언가가 붙어있는 경우가 많아서 이를 전부 분리해줘야 한다.

→ 한국어에서 영어에서의 단어 토큰화와 유사한 형태를 얻으려면 어절 토큰화가 아니라 형태소 토큰화를 수행해야한다.

형태소 : 뜻을 가진 가장 작은 말의 단위 

- 자립 형태소 : 접사, 어미, 조사와 상관없이 자립하여 사용할 수 있는 형태소. 그 자체로 단어가 된다. 체언(명사, 대명사, 수사), 수식언(관형사, 부사, 감탄사)

- 의존 형태소 : 다른 형태소와 결합하여 사용되는 형태소. 접사 어미, 조사, 어간을 뜻함

2) 한국어는 띄어쓰기가 영어보다 잘 지켜지지 않는다. 

### 품사 태깅 (Part-of-speech tagging)

단어 표기는 같지만 품사에 따라서 단어의 의미가 달라지기도 한다. 

예) 못 - 고정하는 물건 / 못한다와 같은 동작동사

### 한국어 토큰화

한국어 자연어 처리를 위해서 KoNLPy(코엔엘파이)라는 파이썬 패키지를 사용할 수 있다. KoNLPy를 통해서 사용할 수 있는 형태소 분석기로 Okt(Open Korea Text), 메캅(Mecab), 코모란(Komoran), 한나눔(Hannanum), 꼬꼬마(Kkma)가 있다.

```python
// 여기서는 Okt와 꼬꼬마 두개의 형태소 분석기를 사용하여 토큰화를 수행

from konlpy.tag import Okt
from konlpy.tag import Kkma

okt = Okt()
kkma = Kkma()

print('OKT 형태소 분석 :',okt.morphs("열심히 코딩한 당신, 연휴에는 여행을 가봐요"))
print('OKT 품사 태깅 :',okt.pos("열심히 코딩한 당신, 연휴에는 여행을 가봐요"))
print('OKT 명사 추출 :',okt.nouns("열심히 코딩한 당신, 연휴에는 여행을 가봐요"))

print('꼬꼬마 형태소 분석 :',kkma.morphs("열심히 코딩한 당신, 연휴에는 여행을 가봐요"))
print('꼬꼬마 품사 태깅 :',kkma.pos("열심히 코딩한 당신, 연휴에는 여행을 가봐요"))
print('꼬꼬마 명사 추출 :',kkma.nouns("열심히 코딩한 당신, 연휴에는 여행을 가봐요"))
```

OKT ****형태소 분석 : ['열심히', '코딩', '한', '당신', ',', '연휴', '에는', '여행', '을', '가봐요']

OKT ****품사 태깅 : [('열심히', 'Adverb'), ('코딩', 'Noun'), ('한', 'Josa'), ('당신', 'Noun'), (',', 'Punctuation'), ('연휴', 'Noun'), ('에는', 'Josa'), ('여행', 'Noun'), ('을', 'Josa'), ('가봐요', 'Verb')]

OKT ****명사 추출 : ['코딩', '당신', '연휴', '여행']

꼬꼬마 형태소 분석 : ['열심히', '코딩', '하', 'ㄴ', '당신', ',', '연휴', '에', '는', '여행', '을', '가보', '아요']
꼬꼬마 품사 태깅 : [('열심히', 'MAG'), ('코딩', 'NNG'), ('하', 'XSV'), ('ㄴ', 'ETD'), ('당신', 'NP'), (',', 'SP'), ('연휴', 'NNG'), ('에', 'JKM'), ('는', 'JX'), ('여행', 'NNG'), ('을', 'JKO'), ('가보', 'VV'), ('아요', 'EFN')]
꼬꼬마 명사 추출 : ['코딩', '당신', '연휴', '여행']

`morphs`  형태소 추출

`pos`  품사 태깅

`nouns`  명사 추출

참고자료 : [한국어 형태소 분석기 성능 비교](https://iostream.tistory.com/144)

# 정제(Cleaning)과 정규화(Normalization)

토큰화 작업 전, 후에 텍스트 데이터를 용도에 맞게 정제 및 정규화 과정을 거친다. 

정제 : 갖고 있는 코퍼스로부터 노이즈 데이터를 제거

정규화 : 표현 방법이 다른 단어들을 통합시켜 같은 단어로 만든다. 

1) 규칙에 기반한 표기가 다른 단어들의 통합 

예] US - USA, uh-huh - uhhuh

2) 대, 소문자 통합

3) 불필요한 단어의 제거 - 불용어 제거, 등장 빈도가 적은 단어 등

4) 정규 표현식 (Regular Expression)

# 어간 추출과 표제어 추출

정규화 기법 중 코퍼스에 있는 단어의 개수를 줄일 수 있는 기법

하나의 단어로 일반화시킬 수 있아면 하나의 단어로 일반화 시켜서 문서 내의 단어수를 줄인다. 이러한 방법들은 BoW(Bag of Words)표현을 사용하는 자연어 처리 문제에서 자주 사용된다. 

### 표제어 추출 (Lemmatization)

표제어 : 기본 사전형 단어

예] be - am, are, is

표제어 추출을 하는 가장 섬세한 방법은 단어의 형태학적 파싱을 먼저 진행하는 것.

형태학 : 형태소로부터 단어들을 만들어가는 학문

형태학적 파싱 : 형태소의 종류 - 어간, 접사 를 분리하는 작업

1) 어간 (stem) : 단어의 의미를 담고 있는 단어의 핵심 부분

2) 접사 (affix) : 단어에 추가적인 의미를 주는 부분

```python
from nltk.stem import WordNetLemmatizer

lemmatizer = WordNetLemmatizer()

words = ['policy', 'doing', 'organization', 'have', 'going', 'love', 'lives', 'fly', 'dies', 'watched', 'has', 'starting']

print('표제어 추출 전 :',words)
print('표제어 추출 후 :',[lemmatizer.lemmatize(word) for word in words])
```

표제어 추출 전 : ['policy', 'doing', 'organization', 'have', 'going', 'love', 'lives', 'fly', 'dies', 'watched', 'has', 'starting']
표제어 추출 후 : ['policy', 'doing', 'organization', 'have', 'going', 'love', 'life', 'fly', 'dy', 'watched', 'ha', 'starting']

### 어간 추출 (Stemming)

어간을 추출하는 작업, 행태학적 분석을 단순화한 버전으로 볼 수 있다. 

### 어간추출과 표제어 추출의 차이

**Stemming** am → am, the going → the go, having → hav

**Lemmatization** am → be, the going → the going, having → have

### 한국어서의 어간 추출

5언 9품

| 언 | 품 |
| --- | --- |
| 체언 | 명사, 대명사, 수사 |
| 수식언 | 관형사, 부사 |
| 관계언 | 조사 |
| 독립언 | 감탄사 |
| 용언 | 동사, 형용사 |

1) 활용 (conjugation)

-어간(stem) : 용언을 활용할 때, 원칙적으로 모양이 변하지 않는 부분, 확용에서 어미에서 선행하는 부분

-어미(ending) : 용언의 어간 뒤에 붙어서 활용하면서 변하는 부분

→ 규칙 활용, 불규칙 확용

2) 규칙 활용

어간이 어미를 취할 떄 어간의 모습이 일정한 경우 예] 잡+다

이 경우에는 어간의 모습이 어미가 붙기 전과 붙은 후가 같으므로, 규칙 기반으로 어미를 단순히 분리해주면 어간 추출이 된다.

3) 불규칙 활용

어간이 어미를 취할 때 어간의 모습이 바뀌거나 취하는 어미가 특수한 어미일 경우

예] 푸르+어 → 푸르러

 [다양한 불규칙 활용의 예](https://namu.wiki/w/한국어/불규칙%20활용)

# 불용어 (Stopword)

데이터에서 유의미한 단어 토큰만을 선별하기 위해서 큰 의미가 없는 단어 토큰을 제거하는 작업이 필요. 

불용어 : 문장에서 자주 등장하지만, 실제 의미 분석을 하는 데 거의 기여가 없는 단어

### NLKT에서 불용어 확인하기

```python
stop_words_list = stopwords.words('english')
print('불용어 개수 :', len(stop_words_list))
print('불용어 10개 출력 :',stop_words_list[:10])
```

불용어 개수 : 179
불용어 10개 출력 : ['i', 'me', 'my', 'myself', 'we', 'our', 'ours', 'ourselves', 'you', "you're"]

### NKLT를 통해서 불용어 제거하기

```python
example = "Family is not an important thing. It's everything."
stop_words = set(stopwords.words('english')) 

word_tokens = word_tokenize(example)

result = []
for word in word_tokens: 
    if word not in stop_words: 
        result.append(word) 

print('불용어 제거 전 :',word_tokens) 
print('불용어 제거 후 :',result)
```

불용어 제거 전 : ['Family', 'is', 'not', 'an', 'important', 'thing', '.', 'It', "'s", 'everything', '.']
불용어 제거 후 : ['Family', 'important', 'thing', '.', 'It', "'s", 'everything', '.']

### 한국어에서 불용어 제거하기

한국어에서 불용어를 제거하는 방법으로는 간단하게는 **토큰화 후에 조사, 접속사 등을 제거하는 방법**이 있다. 하지만 불용어를 제거하려고 하다보면 조사나 접속사와 같은 단어들뿐만 아니라 명사, 형용사와 같은 단어들 중에서 불용어로서 제거하고 싶은 단어들이 생긴다. 결국에는 사용자가 직접 불용어 사전을 만들게 되는 경우가 많다.

보편적으로 선택할 수 있는 한국어 불용어 [리스트1](https://www.ranks.nl/stopwords/korean), [리스트2](https://bab2min.tistory.com/544) - 절대적인 기준은 아님

# 정규 표현식 (Regular Expression)

### 정규 표현식 문법과 모듈 함수

파이썬에서는 정규 표현식 모듈 re을 지원한다. 이를 이용해 특정 규칙이 있는 텍스트 데이터를 빠르게 정제할 수 있다.

1) 정규 표현식 문법

| 특수문자 | 설명 | 예시 |
| --- | --- | --- |
| . | 한 개의 임의의 문자를 나타낸다. 
(줄바꿈 문자인 \n는 제외) | a.c
→ abc, avc, a5c, a!c etc... |
| ? | 앞의 문자가 존재할 수도 있고, 존재하지 않을 수도 있다. (문자가 0개 또는 1개) | ab?c
→ a[b]c, a[ ]c |
| * | 앞의 문자가 무한개로 존재할 수도, 존재하지 않을 수도 있다. (문자가 0개 이상) | ab*c
→ ac, abc, abbc, abbc etc..  |
| + | 앞의 문자가 최소 한 개 이상 존재한다. (문자가 1개 이상) |  |
| ^ | 뒤의 문자열로 문자열이 시작된다. |  |
| $ | 앞의 문자열로 문자열이 끝난다. |  |
| {숫자} | 숫자만큼 반복 |  |
| {숫자1, 숫자2} | 숫자1 이상 숫자2 이하만큼 반복한다. → ?, *, +로 대체 가능. |  |
| {숫자,} | 숫자 이상만큼 반복 |  |
| [] | 대괄호 안의 문자들 중 한 개의 문자와 매치합니다. 
[amk]라고 한다면 a 또는 m 또는 k 중 하나라도 존재하면 매치를 의미. 
[a-z]와 같이 범위 지정 가능. 
[a-zA-Z]는 알파벳 전체를 의미하는 범위 문자열에 알파벳이 존재하면 매치 |  |
| [^문자] | 해당 문자를 제외한 문자를 매치한다. |  |
| | | AlB와 같이 쓰이며 A 또는 B를 의미 |  |

| 문자규칙 | 설명 |
| --- | --- |
| \ | 역 슬래쉬 문자 자체를 의미 |
| \d | 모든 숫자를 의미.  == [0-9]. |
| \D | 숫자를 제외한 모든 문자를 의미. == [^0-9] |
| \s | 공백을 의미  == [ \t\n\r\f\v] |
| \S | 공백을 제외한 문자를 의미 == [^ \t\n\r\f\v] |
| \w | 문자 또는 숫자를 의미 == [a-zA-Z0-9] |
| \W | 문자 또는 숫자가 아닌 문자를 의미.  == [^a-zA-Z0-9] |

### 정규표현식 모듈 함수

| 모듈 함수 | 설명 |
| --- | --- |
| re.complie() | 정규표현식을 컴파일하는 함수. 즉, 파이썬에게 전해주는 역할. 
찾고자 하는 패턴이 빈번한 경우에는 미리 컴파일해놓고 사용하는 것이 좋다. |
| re.search() | 문자열 전체에 대해서 정규표현식과 매치되는지 검색 |
| re.match() | 문자열의 처음이 정규표현식과 매치되는지 검색 |
| re.split() | 정규 표현식을 기준으로 문자열을 분리하여 리스트로 반환한다. |
| re.findall() | 문자열에서 정규 표현식과 매치되는 모든 경우의 문자열을 찾아서 리스트로 리턴합니다. 만약, 매치되는 문자열이 없다면 빈 리스트가 리턴된다. |
| re.finditer | 문자열에서 정규 표현식과 매치되는 모든 경우의 문자열에 대한 이터레이터 객체를 리턴한다 |
| re.sub() | 문자열에서 정규 표현식과 일치하는 부분에 대해서 다른 문자열로 대체한다. |