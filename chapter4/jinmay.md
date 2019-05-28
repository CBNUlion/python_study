# 파이 크러스트: 코드 구조

## 4.1 코멘트 달기:

파이썬에서 주석은 **#**을 사용한다. 여러줄 주석은 없다.

## 4.2 라인 유지하기: \

한 라인에서 권장하는 최대 문자수는 80자이다. 한 줄에 코드를 다 넣을 수 없다면 가독성을 위해서 **백슬래시(\\)**를 사용해서 다음 라인에 계속 입력하는 것이 좋다.

```python
alphabet = 'abcdefg' + \
    'hijklmnop' + \
    'qrstuv'
```

파이썬 표현식이 여러 줄에 있는 경우에도 사용 가능하다.

```python
1 + 2 + \
    3

# 6을 리턴
```

## 4.3 비교하기: if, elif, else

다른 프로그래밍 언어와는 달리, 파이썬에서는 if문의 조건 테스트에서는 괄호가 필요 없다. **괄호 대신에 콜론(:)을 사용 하는 것에 유의하자.**

```python
if (a == 'a')
    pass # error
if a == 'a':
    pass # ok
if (a == 'a'):
    pass # ok
```

비교연산자는 True 혹은 False를 리턴하며 비교 연산자보다 우선순위가 낮다. 연산자 우선순위를 외우는 것보단 괄호를 사용함으로써 비교 순서를 명확히 해주는 것이 낫다.

```python
# 아래 두 코드는 같다
5 < x and x < 10
(5 < x and x < 10)
```

### 4.3.1 True와 False

아래의 값은 모두 False로 간주된다.

| 요소           | False |
| -------------- | ----- |
| null           | None  |
| 정수 0         | 0     |
| 부동소수점수 0 | 0.0   |
| 빈 문자열      | ''    |
| 빈 리스트      | []    |
| 빈 튜플        | ()    |
| 빈 딕셔너리    | {}    |
| 빈 셋          | set() |

## 4.4 반복하기: while

1부터 5까지 출력하는 예제이다.

```python
count = 1
while count <= 5:
    print(count)
    count += 1
```

### 4.4.1 중단하기: break

루프(반복)을 중단하기 위해서 break를 사용할 수 있다.

```python
while True:
    a = input('q means quit: ')
    if a == 'q':
        break
    print(a.capitalize())
```

만약 이중 루프로 구성되어 있다면 가장 안쪽에 있는 break는 하나의 루프만을 중단시킬 수 있다.

### 4.4.2 건너뛰기: continue

루프를 중단하는 건 아니지만 다음 루프로 건너뛸 수 있다. **루프의 종료가 아닌 다음 차례의 루프로 건너뛰는 것이다**

```python
a = 1
while a < 10:
    if a % 2 == 0:
        continue
    print(a)
    a += 1
```

위의 코드는 홀수를 출력할 것 같지만. 1을 출력한 뒤 무한루프를 돌게된다. continue 문을 실행하고 a값은 2가 되고 계속 continue를 실행하기 때문이다. **continue**는 **반복문의 나머지 부분을 보지 않고**, 루프의 처음으로 돌아가기 때문이다.

### 4.4.3 break 확인하기: else

while 루프를 실행하는데 break가 실행되지 않았다면 else가 실행된다.

> else를 그냥 루프의 break를 확인하는 용도라고 생각해도 좋다.

## 4.5 순회하기: for

이터레이터와 밀접한 연관을 가지고 있다.

### 4.5.4 여러 시퀀스 순회하기: zip()

순회를 하는 방법에는 for 반복문도 있지만 zip함수를 이용해서 여러 시퀀스를 병렬로 순회하는 것도 있다.

```python
a = [1, 2, 3, 4, 5]
b = ['a', 'b', 'c', 'd', 'e']

for num, char in zip(a, b):
    print("{} - {}".format(num, char))

# 1 - a
# 2 - b
# 3 - c
# 4 - d
# 5 - e
```

주의해야할 점으로는 **여러 시퀀스 중 가장 짧은 시퀀스가 완료되면 zip()은 멈추게 된다는 것**이다. 또한 zip()은 리스트나 튜플 자신을 리턴하지 않고 **하나로 반환될 수 있는 순회 가능한 값을 리턴한다.** 즉, zip()은 iterable을 받아서 iterator를 만드는 것이다!

```python
c = zip(a, b)
print(c) # <zip object at 0x109dc6308>
```

### 4.5.5 숫자 시퀀스 생성하기: range(start, stop, step)

range() 함수는 숫자 스트림을 반환한다. 메모리를 전부 사용하지 않고, 아주 큰 범위를 안전하게 생성할 수 있게 해준다. 사용법은 슬라이스와 비슷하다. **zip과 range는 순회 가능한 객체(iterator)를 반환한다.** 때문에 for 문에서 사용할 수 있는 것이다.

## 4.6 컴프리핸션

하나 이상의 이터레이터로부터 파이썬 자료구조를 만드는 간편한 방법이다.

### 4.6.1 리스트 컴프리헨션

**[표현식 for 변수 in 순회 가능한 객체]**

**[표현식 for 변수 in 순회 가능한 객체 if 조건]**

```python
number_list = [x for x in range(1, 11)]
# [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

간단한 조건식도 포함될 수 있다.

```python
odd_list = [x for x in range(1, 11) if x % 2 == 1]
# [1, 3, 5, 7, 9]
```

중첩도 가능하다

```python
rows = range(1, 7)
cols =range(1, 7)

[
    [x, y] for x in rows if x % 2 == 0 for y in cols if y % 2 ==1
]
```

### 4.6.2 딕셔너리 컴프리헨션

**{ 키*표현식: 값*표현식 for 표현식 in 순회 가능한 객체 }**

```python
word = 'letters'
letter_counts = {c: word.count(c) for c in word}
# {'l': 1, 'e': 2, 't': 2, 'r': 1, 's': 1}
```

### 4.6.3 셋 컴프리헨션

**{ 표현식 for 표현식 in 순회 가능한 객체 }**

### 4.6.3 제너레이터 컴프리헨션

**튜플은 컴프리헨션이 없다.** 소괄호를 통해 컴프리헨션을 만드려고 시도하면 제너레이터 객체가 생성된다.

```python
a = (num for num in range(1, 11))
# <generator object <genexpr> at 0x109c44f48>
```

**제너레이터는 이터레이터에 데이터를 제공하는 하나의 방법이다.** 때문에 제너레이터 객체를 바로 순회할 수 있다.

```python
num_list = (num for num in range(1, 5))
for a in num_list:
    print(a)
# 1
# 2
# 3
# 4
```

## 4.7 함수

```python
def func():
    pass
```

코드의 재사용설을 높힌다.

**함수로 전달된 값을 인자**라고 부르고 **함수를 호출하면 인자의 값은 함수 내의 매개변수**에 복사된다

```python
def pprint(something):
    print(something)

pprint('hello world') # hello world
```

**만약 함수가 명시적으로 return을 호출하지 앟으면 호출자는 리턴값으로 None을 얻는다**

```python
print(pprint('abc'))
# abc
# None
```

> None은 부울로 평가될때는 False 처럼 보이지만 부울값 False와는 다르다.
>
> ```python
> thing = None
> if thing:
>   print('a')
> else:
>   print('b')
> # b
> ```
>
> ```python
> if thing is None:
>   print('none')
> else:
>   print('b')
> # none
> ```

### 4.7.1 위치 인자

함수에 들어오는 값을 순서대로 상응하는 매개변수에 복사하는 **위치 인자**이다(positional arguments). 사용하기 편하지만 각 위치의 의미를 알아야 한다는 단점이 있다.

```python
def menu(a, b, c):
    print(a, b, c)
```

### 4.7.2 키워드 인자

매개변수에 상응하는 이름을 인자에 지정할 수 있다. **인자를 함수의 정의와 다른 순서로 지정할 수 있다.**

**위치 인자와 키워드 인자가 함께 사용된다면 위치 인자가 무조건 먼저 와야한다.**

### 4.7.3 기본 매개변수값 지정하기

매개변수에 기본값을 지정할 수 있다.

```python
# 주의하자: 위치 인자가 키워드 인자보다 먼저 와야한다
def menu(lunch, breakfast='bread'):
    return {
        'breakfast': breakfast,
        'lunch': lunch
    }

menu('haha', 'hihi')
# {'breakfast': 'hihi', 'lunch': 'haha'}
```

**기본 인자 값은 함수가 실행될 때 계산되지 않고, 함수를 정의할때 계산된다.**

```python
def buggy(arg, result=[]):
    result.append(arg)
    print(result)

buggy('a') # ['a']
buggy('b') # ['a', 'b']
```

함수를 호출할때마다 리스트를 초기화 하려면 아래와 같이 해야한다.

```python
def buggy(arg):
    result = []
    result.append(arg)
    print(result)

buggy('a') # ['a']
buggy('b') # ['b']
```

### 4.7.4 위치 인자 모으기 : \*

\*(애스터리스크)는 매개변수에서 위치 인자 변수들을 튜플로 묶어준다. \*를 사용할때 가변 인자의 이름으로 **args**를 사용할 필요는 없지만 **관용적으로 사용**한다.

```python
def pprint(*args):
    print(args)

pprint('a', 'b', 'c') # ('a', 'b', 'c')
```

### 4.7.5 키워드 인자 모으기: \*\*

두 개의 \*\*(에스터리스크)를 사용함으로써 키워드 인자를 딕셔너리로 묶을 수 있다. 마찬가지로 **가변 인자의 이름으로 kwargs를 관용적으로 사용한다.**

```python
def pprint(**kwargs):
    print(kwargs)

pprint(a=1, b=2, c=3) # {'a': 1, 'b': 2, 'c': 3}
```

**args와 kwargs를 섞어서 사용하려면 순서에 주의해야 한다!**

> args를 먼저 적는다!!

### 4.7.6 docstring

함수 몸체 시작 부분에 문자열을 포함시켜 함수 정의에 문서를 붙일 수 있다.

### 4.7.7 일등 시민: 함수

**파이썬의 모든 것은 객체(object)다!!** 파이썬의 함수는 일등 시민(first-class sitizen)이며 함수를 변수에 할당할 수 있고, 다른 함수에서 함수를 인자로 쓸 수 있으며, 함수에서 함수를 리턴할 수 있다
