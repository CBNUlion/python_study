# chapter 4 파이 크러스트: 코드구조

파이썬은 구조를 정의하는데 **공백**을 사용한다.

## 4.1 코멘트 달기 : #

- 코멘트는 인터프리터에 의해 무시되는 텍스트의 한 부분이다.
- 파이썬은 여러라인을 처리하는 주석이 없다. 따라서 명시적으로 각 라인에 #을 붙여야한다.
- 해시(hash)가 문자열 안에 있다면 코멘트가 아닌 평범한 문자로 돌아가게 된다

## 4.2 라인 유지하기 : \

## 4.3 비교하기 : if, elif, else

- if, else : 참(True)인지 거짓(False)인지 확인하는 *선언문*이다

- 조건을 사용할 때에는 ()를 쓰지 않는다
- 조건문을 작성하려면 : 를 사용한다

- 비교 연산자와 부울연산자 
- ( 부울 연산자는 비교 연산자보다 우선순위가 낮다.)
    - 비교 연산자 : ==, !=, <, <=, >, >=, in
    - 부울 연산자 : and, or, not

### 4.3.1 True 와 False

- False로 간주되는 값들
```python
요소               False

null               NONE
정수0                0
부동소수점수0         0
빈 문자열            ' '
빈 리스트             []
빈 튜플               ()
빈 딕셔너리           {}
빈 셋                set()
```

## 4.4 반복하기 : while

- 파이썬에서 가장 간단한 루핑 매커니즘

### 4.4.1 중단하기 : break

- 루프문을 중간에 빠져나옴

### 4.4.2 건너뛰기 : continue

- 반복문을 중단하진 않되, 다음 루프로 뛰어 넘고 싶을 때

### 4.4.3 break 확인하기 : else

## 4.5 순회하기 : for

- 파이썬에서 **이터레이터(iterator)**는 유용
    - 자료 구조의 크기와 구현 방식에 상관 없이 자료구조를 순회할 수 있도록 해줌
    - 바로 생성되는 데이터도 순회 가능
    - 데이터가 메모리에 맞지 않더라도 데이터 **스트림**을 처리할 수 있도록 허용
- 순회 가능한 객체 : 문자열, 리스트, 튜플, 딕셔너리, 셋 등
- 딕셔너리는 키를 반환
    - 값을 반환하고 싶다면 values() 함수를 사용
        - ex. for value in taemi.values()
    - 키와 값을 반환하고 싶다면 items()함수를 사용
        - ex. for item in taemi.items()
    - 키는 card에, 값은 contents에 할당하고 싶다면?
        - ex. for card, contents in taemi.items()
### 4.5.1 중단하기 : break
### 4.5.2 건너뛰기 : continue
### 4.5.3 break 확인하기 : else

### 4.5.4 여러 시퀀스 순회하기 : zip()

- zip() 함수를 사용해서 여러 시퀀스를 병렬로 순회할 수 있다
    - for day, fruit, drink, dessert in zip(days, fruits, drinks, desserts)
    - 이렇게 사용하게 되면 for 문 한번에 zip안에 있는 자료구조들을 한번에 하나씩 꺼내온다.
    - 여러 시퀀스 중 가장 짧은 시퀀스가 완료되면 zip()은 멈춘다.
- zip() 함수 이용하기
    - 두개의 튜플을 만들기 위해 zip을 사용한다
        - zip()에 의해 반환되는 값은 튜플이나 리스트가 자신이 아니라 하나로 반환될 수 있는 순회 가능한 값
```python

    list(zip(튜플, 튜플))  # [(,),(,),(,)]
    dict(zip(튜플, 튜플)) # {'':'','':'','':''}
```
### 4.5.5 숫자 시퀀스 생성하기 : range()

- 리스트나 튜플 같은 자료구조를 생성하여 저장하지 않더라도 특정 범위 내에서 숫자 스트림 반환
    - 컴퓨터의 메모리를 전부 사용하지 않고, 프로그램의 충돌 없이 아주 큰 범위 생성가능
- 사용법
    - 슬라이스 사용법과 비슷
    - range(start, stop, step)
        - start : defalt = 0
        - stop : 필수 값
        - step : detalt = 1
- 순회 가능한 객체를 반환
    - range()나 zip()같은 함수는 순회 가능한 객체를 반환한다

### 4.5.6 기타 이터레이터

- 8장 
    - 파일에 대한 순회 ( iteration )
- 6장 
    - 직접 정의한 객체를 순회가 가능하도록 설정

## 4.6 컴프리핸션(conprehention, 함축)

- 파이썬 자료구조를 만드는 방법
    - 하나 이상의 이터레이터
    - 비교적 간편한 구문으로 반복문과 조건 테스트 결합 가능

### 4.6.1 리스트 컴프리헨션

- 일반적 표현
    - [표현식 for 항목 in 순회 가능한 객체]
        - [number for number in range(1,6)] ==> [1,2,3,4,5]
        - [number-1 for number in range(1,6)] ==> [0,1,2,3,4]
- 조건문이 있는 표현
    - [표현식 for 항목 in 순회 가능한 객체 if 조건]
        - [number for number in range(1,6) if number %2 == 1] ==> [1,3,5]
- 중첩루프가 있는 표현
    - [(row, col) for row in rows for col in cols]
        - rows가 더 큰 루프, cols는 rows안의 루프
        - 튜플 언패킹도 가능
```python

cells = [(row, col) for row in rows for col in cols]
for row, col in cells:
    print(row, col)

```

### 4.6.2 딕셔너리 컴프리헨션

- {키_표현식 : 값_표현식 for 표현식 in 순회 가능한 객체}
    - if테스트 가능
    - 다중 for문 가능
ex1.
```python 
name = 'taemi'
name_counts = {taemi : name.count(taemi) for taemi in name}
name_counts
#{'t':1, 'a':1, 'e':1, 'm':1, 'i':1}
```
ex2.
```python
name ='taemi'
taemi_counts = {taemi:name.count(taemi) for taemi in set(name)}
# {'t': 1, 'e': 1, 'a': 1, 'i': 1, 'm': 1}
```

- ex1, ex2를 비교해봤을 때 출력이 다른 것을 확인할 수 있다 
    - (name에 들어있는 문자열이 반복되면 더 잘 확인할 수 있다)
    - 이는 set(name)을 순회하는 것과 문자열 name을 순회하는 서로 다르게 문자를 반환하기 때문이다.

### 4.6.3 셋 컴프리헨션

- 형식
    - {표현식 for 표현식 in 순회 가능한 객체}
        - if 테스트 가능
        - 다중 for절 가능

### 4.6.4 제너레이터 컴프리헨션

- **튜플은 컴프리헨션이 없다.**
- 튜플 안에 컴프리헨션을 사용하면 예외는 나오지 않음
- 제너레이터 객체를 반환한다
    - 제너레이터 객체는 한번만 순환 가능하다
        - 제너레이터 객체는 한번 순환하면 빈 값을 출력한다
        - 제너레이터 객체는 바로 순회 가능하다
- 리스트 컴프리헨션처럼 쓰고 싶다면 
    - 제너레이터 객체에 list() 호출을 랩핑해서 변경시키면 됨

## 4.7 함수

- 함수 정의
    - def 와 함수이름, 괄호, (매개변수), :
- 함수가 명시적으로 return을 호출하지 않으면 None을 얻음
    - None과 False는 다르다

### 4.7.1 위치 인자 (positional arguments)

파이썬은 다른 언어에 비해 함수의 인자를 유연하고 독특하게 처리한다.

### 4.7.2 키워드 인자

- 위치인자의 혼동을 피하기 위해 사용
- 매개 변수에 상응하는 이름을 인자에 지정할 수 있다.
    - 다른 순서로 정의해도 무관
ex. 함수이름(인자이름 = '값')
- 위치 인자와 키워드 인자를 혼동해서 쓸 수 있다.
    - 위치 인자와 키워드 인자로 함수를 호출한다면 위치 인자가 먼저 와야한다.

### 4.7.3 기본 매개변수값 지정하기

- 기본 매개 변수 값 지정
    - 호출자가 인자를 제공하지 않음 : 기본 매개변수 값 들어감
    - 호출자가 인자를 제공 : 입력한 인자 사용
```python

def taemi(first = "park", second = "taemi"):
    print(first, second)
taemi() # park taemi
taemi('taemi', 'park') #taemi park
```

### 4.7.4 위치 인자 모으기 : *

- **포인터 아님**
- 매개변수에서 위치 인자 변수들을 튜플로 묶는다.
```python 
def print_args(*args):
    print('positional argument tuple: ', args)
```
- 이처럼 사용할 때는 그냥 args라고 쓰면 됨
- 인자가 들어가지 않으면 빈 튜플 생성
- *를 사용할 때 가변 인자의 이름으로 args를 사용할 필요는 없음
    - 관용적으로 args를 쓸 뿐

### 4.7.5 키워드 인자 모으기 : **

- 딕셔너리로 묶음
- 인자의 이름 : 키
- 키에 대응하는 딕셔너리 값 : 값
```python
def print_kwarge(kwargs):
    print(kwargs)

print_kwargs(first = "park", second = "taemi")
#{'first': 'park', 'second':'taemi'}
```

- 위치 매개변수와 *args, **kwargs를 섞어서 사용하려면
    - 순서대로 배치해야 함

### 4.7.6 docstring

함수의 몸체 시작 부분에 문자열을 포함시켜 함수 정의에 문서(documentation)를 붙일 수 있다.
이것이 함수의 **docstring**이다.

- 사용 
    - 함수 내에 문자열을 포함시킴
        - 길어도 가능, 즉  '', "", ''' ''', 전부 가능
- 출력
    - help() 함수로 호출
        - help(taemi)
- 서식 없이 출력
    - print(taemi.__doc__)
```python
def taemi():
    'return taemi'
    return taemi

help(taemi)

#Help on function taemi in module __main__:
#
#taemi()
# return taemi

print(taemi.__doc__)
# return taemi
```

### 4.7.7 일등 시민 : 함수
 
모든 파이썬은 객체이다. 

- 객체 : 숫자, 문자열, 튜플, 리스트, 딕셔너리, **함수**
- **함수를 변수에 할당 가능**
    - **다른 함수에서 이를 인자로 쓸 수 있음**
```python
def answer():
    print(42)

def run_something(func):
    func()

run_something(answer) # 42
```
- **answer()**를 전달하는 것이 아니라 **answer**로 전달하는 것
- 괄호가 없으면 함수도 다른 모든 객체와 마찬가지로 간주

```python
def taemi ():
    return taemi
type(taemi) #<class 'function'>
type(taemi()) # <class 'function'>
```

- func : 실행할 함수
- arg1 : func 함수의 첫 번째 인자
- arg2 : func 함수의 두 번째 인자
사용 :
def run_something_with_args(func, arg1, arg2):
    func(arg1, arg2)


*args와 **kwargs인자와 결합 가능
```python
def aum_args(*arg):
    return sum(args)
```

### 4.7.8 내부 함수

- 함수 안에 함수
- 루프나 코드 중복을 피하기 위해 또 다른 함수 내에 어떤 복잡한 작업을 한 번 이상할 때 유용

### 7.4.9 클로져(closure)

- 내부함수는 **클로져**처럼 행동 가능
    - 특징 
        - 내부에 있는 함수는 인자를 취하지 않고, 외부 함수의 변수를 직접 사용
        - return 즉 반환을 할 때, 이름을 호출하지 않고 반환
- 다른 함수에 의해 동적 생성 ( 함수 안에 함수 정의 )
- 바깥 함수로부터 생성된 변수값을 변경, 저장 가능
```python
def knights2(saying):
    def inner2():
        return "say: '%s'" % saying
    return inner2
```

### 4.7.10 익명함수 : lambda()

- 파이썬의 람다함수는 단일문으로 표현되는 익명함수
- 사용 
```python
edit_story(stairs, lambda word: word.capitalize() + '!')
```

함수의 두번 째 인자, 구성을 보면
< lambda 인수 : 함수 내용 > 으로 구성이 되어 있다.

## 4.8 제너레이터 (generator)

- 파이썬의 시퀀스를 생성하는 객체
- 전체 시퀀스를 한 번에 메모리를 생성하고 정렬할 필요 없음
- 잠재적으로 아주 큰 시퀀스 순회 가능
- 이터레이터에 대한 소스로 자주 사용된다.
- 제너레이터 중 하나인 range() 함수를 사용
    - range() : 일련의 정수 생성
    - sum(range(1, 101))
        - 순회 할 때마다 마지막으로 호출 된 항목을 기억하고 다음 값을 반환
- 일반 함수와 다른 점 : 일반함수는 이전 호출에 대한 메모리가 없고, 항상 같은 상태로 첫째 라인부터 수행
- 잠재적으로 큰 시퀀스를 생성, 제너레이터 컴프리헨션에 대한 코드가 아주 긴 경우 사용
- 일반 함수지만 return문으로 값을 반환하지 않음
    - 대신 **yield**문으로 값을 반환
```python

def my_range(first = 0, last = 10, step = 1):
    number = first
    while number < last :
        yield number
        number += step

my_range
#<function my_range at 0x10193e268>

#제너레이터 반환 객체
ranger = my_range(1,5)
ranger
#<generator object my_range at 0x101a0a168>
```
- 함수 실행
    - 함수 뜸 
- 함수에서 반환되는 객체를 받아서 실행
    - generator 뜸
    - generator 객체 순회 가능

## 4.9 데커레이터 ( decorator)

- 하나의 함수를 취해서 또다른 함수를 반환
- 실제 받는 함수로부터 그 함수 코드를 실행하지 않음
    - 하지만 받은 함수를 호출하여 결과 뿐만 아니라 새로운 함수를 얻음
- 수동으로 데커레이터 할당
    - 데커레이터 함수를 만들어서 안에 넣어줌
- 편하게 데커레이터 할당
    - 함수에 @데커레이터_이름 추가
- 함수는 여러개의 데커레이터를 가질 수 있음
    - 대신 실행 순서에 유의
        - 가장 가까운 데커레이터가 먼저 실행되고 그 위에 데커레이터 실행


## 4.10 네임스페이스와 스코프

- 각 함수는 자신의 네임스페이스 정의
- 함수에서 전역 변수의 값을 얻어 바꾸려고 하면 에러
    - 전역변수는 전역변수의 네임스페이스를 가지고 있기 때문
    - 메인 프로그램은 전역 네임스페이스를 정의
    - 전역과 지역에 같은 변수를 사용하고 싶다면
        - id라는 네임스페이스를 이용
        - return 해줄 때 id(변수이름)을 보내준다 그럼 충돌이 없어서 오류가 나지 않는다
- global
    - 전역 변수의 네임스페이스
- local
    - 지역 변수의 네임스페이스
    - 함수 내가 아니면 힘 x

### 4.10.1 이름에 _와 __사용

- 두 언어스코어 (__)는 변수 선언 시 금지


## 4.11 에러 처리하기 : try, except

- try안에 구문에서 문제가 있으면 except로 가서 예외를 잡아준다
- except에 조건이 있어도 되고 없어도 됨.
    - 조건이 없으면 try문에서 생기는 예외를 전부 받게 됨
    - 조건 있으면 : except 예외타입 as 이름
    
## 4.12 예외 만들기

- 모든 예외는 파이썬 표준 라이브러리에 미리 정의되어 있음
    - 필요한 예외처리 선택해서 사용
    - 예외 타입 정의 가능
        - class이용
        

# 헷갈리는 것
- zip()함수를 사용한 for문
    - zip안에 여러 시퀀스 중 가장 짧은 시퀀스가 완료되면 zip()은 멈추는 것
- 4.6 컴프리헨션에서 
    - 리스트와 튜플은 컴플리헨션 가능
    - **튜플은 컴플리헨션 불가**
        - 튜플을 컴플리헨션처럼 쓴다면 제너레이터 객체 반환
        - 제너레이터 객체는 한번 순회가능
        - 순회가 끝나면 빈 값을 출력
        - 리스트 컴플리헨션처럼 쓰고 싶다면 list((i for i in ice))이런 식으로 랩핑
- 4.4.7 에서 함수를 변수에 할당할 수 있고 이를 다시 인자로 사용할 수 있는 것
- 4.4.7 에서 함수를 함수에 전달할 때 answer()이 아닌 answer의 형태로 전달하는 것
- 클로저는 다른 함수에 의해 동적 생성이 된다.


# Q

- 117p에 튜플에서 키와 값을 모두 반환하기 위해서 ... 
    - ==> 여기부터 '튜플<->딕셔너리'오타 아닌가..?

# 스터디 후
- else 한 번 더 찾아보기 
- 제너레이터 이터레이터 차이점 다시 알아보기

# 두번 째 공부

## zip() 함수 이용

### zip() 함수 최대길이에 맞춰 사용하기

- import하기 
    - from itertools import zip_longest
- 사용법
    - itertools.zip_longest(*terable, fillvalue=None)

```python
x = [1,2,3]
y = [1,2,3,4]
zipped = zip_longest(x, y, fillvalue = 0)
print(list(zipped))

#결과
#[(1, 4), (2, 5), (3, 6), (0, 7)]
```

## 이터레이터와 제너레이터

[관련 블로그](https://mingrammer.com/translation-iterators-vs-generators/)

### 컨테이너(Container)
- 원소들을 가지고 있는 데이터구조
- 멤버쉽 테스트 지원
- 메모리에 상주 ( 보통 모든 원소값을 메모리에 가지고 있음)
- 컨테이너 종류
    - **list**, deque, ...
    - **set**, frozonset, ...
    - **dict**, defaultdict, OderedDict, Counter, ...
    - **tuple**, namedtuple, ...
    - **str**
- 특정한 원소를 포함하고 있는지 판단 가능
    - 딕셔너리는 키 값으로 판단
```python
#여기서 assert는 뒤의 조건이 True가 아니면 AssertError를 발생
>>> assert 1 in [1,2,3]
>>> assert 1 in {1:'part', 2:'taemi'}
>>> assert 4 not in {1:'part', 2:'taemi'}
>>> assert 'p' in 'park'
>>> assert 'park' in 'parktaemi' #문자열은 부분 문자열 모두 "포함"
```
- 마지막예제
    - 문자열은 모든 부분문자열들의 리터럴 복사본을 메모리에 저장하고 있지는 않음
- 컨테이너로 원소를 생성하는 기능은 이를 컨테이너가 아니라 이터레이터로 만듦
- 이터레이블하지 않은 컨테이너 : Bloom filter
    - 특정 원소를 포함하고 있는지 판단가능
    - 각각의 개별 원소 반환 x

### 이터레이블(Iterable)
- 컨테이너
    - 컨테이터가 유한할 경우 이터레이블은 무한한 데이터 소스 나타내기 가능
- 이외에, 파일열기, 소켓 열기 등등..
- 반드시 데이터 구조일 필요 x
    - 이터레이터를 반한할 수 있는 객체면 가능
- **이터레이블이 iter()로 반환한 것이 이터레이터**
- 이터레이블로 for문을 돌리게 되면 iter를 실행시키는데 필요한 GET_ITER를 호출

### 이터레이터(Iterator)
- next()를 호출할 때 다음 값을 생성해내는 상태를 가진 헬퍼 객체
- next()를 가진 모든 객체는 이터레이터

```python
# itertools의 모든 함수는 이터레이터를 반환
>>> from itertools import count
>>> counter = count (start=13)
>>> next(counter)
13
>>> next(counter)
14
```
- 클래스 안에 iter()와 next()가 둘 다 있으면?

### 제너레이터(Generator)
- 특별한 종류의 이터레이터
- 모든 제너레이터는 이터레이터
- 값을 그 때 그 때 생성
- yield 사용
- 값을 넘길 때 객체화 해서 넘김
- 일반 함수는 진입점이 하나라고 하면 제너레이터는 진입점이 여러개
    - 원하는 시점에 데이터를 넘겨 받을 수 있다.
```python
>>> def fib():
...     prev, curr = 0, 1
...     while True:
...         yield curr
...         prev, curr = curr, prev + curr
...
>>> f = fib() #여기서 fib()안 쪽 내용은 아직 실행되지 않음
>>> list(islice(f, 0, 10)) # 호출 시 실행, islice는 f인스턴스에서 next를 호출
[1, 1, 2, 3, 5, 8, 13, 21, 34, 55]

# yield는 하나 값을 반환하며 함수 실행은 거기서 멈춤
#islice가 list에 값을 하나 저장하고 다시 f에게 다음값을 요청
# 이때 f는 yield 밑에 코드부터 실행 
# 다음 yield를 만나 다음 curr값을 반환

#### 제너레이터의 타입
```
[예제](https://winterj.me/Python-Generator/)
```python
>>> def generator():
...     yield 1
...     yield 'string'
...     yield True

>>> gen = generator()
>>> gen
<generator object generator at 0x10a47c678>
>>> next(gen)
1
>>> next(gen)
'string'
>>> next(gen)
True
>>> next(gen)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
StopIteration

```
1. 제너레이터 함수 (function)
    - 몸체에 yield 키워드가 나타나는 모든 함수
2. 제너레이터 표현 (expressions)
3. 리스트 컴프리헨션(list comprehension)과 동일한 제너레이터
    - 튜플을 리스트컴프리헨션의 형태로 사용하면 제너레이터가 된다.

```python
>>> number = [1,2,3,4,5]
>>> [x*x for x in number]
[1, 4, 9, 16, 25]
>>> {x*x for x in  number}
{1, 4, 9, 16, 25}
>>> (x*x for x in number)
<generator object <genexpr> at 0x0000027424643F10>
```
```python
>>> gen = (x*x for x in number)
>>> next(gen)
1
>>> list(gen)
[4,9,16,25]         #이걸 게으른 행동이라고 부른다
```
## 데코레이터 ( decorator )
[참고](https://bluese05.tistory.com/30)

- 함수 앞에 @붙여서 써진 것
- 대상 함수를 wrapping하고, 이 wrapping된 함수의 앞뒤에 추가적으로 꾸며질 구문 들을 정의해서 손쉽게 재사용
##### 어떨 때 사용하는지?
- 메인 구문이 있고, 부가적인 구문을 추가하고 싶을 때
- 그리고 이 부가적인 구문을 반복해서 사용하고 싶은 경우
##### 사용하면 좋은 점은?
- main함수에 대한 가독성이 좋아짐
- 같은 패턴을 100번 해야한다고 할 때 main에 직접 코드를 넣는 것보다 간결하고 간편하다.
##### 사용법
- 함수내에서 사용하고 싶으면?
```python
import datetime

def datetime_decorator(func): #decorator역할을 하는 함수 데커레이터가 적용될 함수를 인자로 받는다
        def decorated():        #원하는 작업 
                print datetime.datetime.now()
                func()
                print datetime.datetime.now()
        return decorated

@datetime_decorator         # 데코레이터 선언
def main_function_1():
        print "MAIN FUNCTION 1 START"

#출처: https://bluese05.tistory.com/30 [ㅍㅍㅋㄷ]
```
- class내에서 사용하고 싶으면?
```python
import datetime

class DatetimeDecorator:
        def __init__(self, f):
                self.func = f

        def __call__(self, *args, **kwargs): #call함수로 decorator형식 정의
                print datetime.datetime.now()
                self.func(*args, **kwargs)
                print datetime.datetime.now()

class MainClass:
        @DatetimeDecorator
        def main_function_1():
                print "MAIN FUNCTION 1 START"

#출처: https://bluese05.tistory.com/30 [ㅍㅍㅋㄷ]
```
## 컴프리헨션

- [컴프리헨션에서 표현식을 2개 이상 쓰지 말기](https://excelsior-cjh.tistory.com/132)
- 리스트 컴프리헨션은 다중 루프와 루프 레벨별 다중 조건을 지원
- 표현식 두 개가 넘는 컴프리헨션은 이해가 어려우므로 피해야한다.

## 추가 
- rendering 
    - rendering은 renderer engine이 함
    - render은 html로 입력 받아 해석해서 모니터로 출력

## Q
- 컨테이너가 이터레이블하면 왜 무한한 데이터 소스를 나타낼 수 있는지
