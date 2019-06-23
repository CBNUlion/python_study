# chapter 5 파이 포장하기 : 모듈, 패키지, 프로그램

## 5.1 스탠스얼론 프로그램(standalone)

- 대화식 인터프리터 말고 코드를 실행시키는 법
1. test.py 를 만든다
2. 안에 코드를 적는다
3. 터미널에 python tset.py를 적는다.
4. 결과값이 실행됨

## 5.2 커맨드 라인 인자

파이썬 파일 실행
```python
python 파일이름.py
```

## 5.3 모듈과 import문

- 모듈 (module) : 파이썬 코드의 파일
- import문을 다른 모듈 코드를 참조

### 5.3.1 모듈 임포트하기
- 모듈 임포트 : import문
- 모듈 : .py 확장자가 없는 파이썬 파일의 이름
- import 한 모듈이름.함수()
    - 네이밍 충돌을 피하기 위함
    - 만약 함수 이름만 쓰고 싶다면 그렇게 써도 되지만, 모듈 이름을 붙이는 것이 더 안전

### 5.3.2 다른 이름으로 모듈 임포트하기
- 앨리어스(alias) 사용

```python
import report as wr
# import # 원래 모듈 #as #지정하고 싶은 이름
```

### 5.3.3 필요한 모듈만 임포트하기

- 필요한 모듈을 임포드 : import
- 필요한 모듈에서 필요한 부분만 임포트 : import 모듈이름 from 필요한 부분

```python
from report import get_description as do_it
#from #모듈 #import #필요한함수 #as (엘리어스) #필요한 모듈에 지정하고 싶은 이름
```

### 5.3.4 모듈 검색 경로
- 디렉터리 이름의 리스트와 표준 sys모듈에 저장된 zip 아카이브 파일을 변수 **path** 로 사용한다.
```python
import sys
for place in sys.path:
    print(place)
```

## 5.4 패키지

- 하나의 디렉터리에 기능을 여러 개 나눠서 .py파일로 만드는 것
```python
from sources import one, two
#from #하나의 디렉터리 #import #one.py , two.py 임포트
```
- sources 디렉터리에 필요한 것
    - __init__.py 파일
        - 비워도 되지만 꼭 추가할 것
        - 그래야 파이썬이 패키지로 간주한다.
## 5.5 파이썬 표준 라이브러리
- 파이썬으로 원하는 기능이 있다면 표준 모듈에 있는지 먼저 확인하는 것이 좋음

### 5.5.1 누락된 키 처리하기 : setdefault(), defaultdict()

- 존재하지 않는 키로 딕셔너리에 접근하는 예외를 피할 수 있음
- 딕셔너리에 원하는 키가 없을 경우 새로 생성
- 있는 키가 들어가면 변화 없고 원래 값 그대로 있음
```python
taemi = {'one':1, 'two':2}
two = taemi.setdefault('two',100)   # 있는 값이므로
two
#2                  #변화 없이 2가 출력됨
```
- setdefault(), defaultdict() 차이
    - defaultdic()는 딕셔너리를 생성할 때 모든 새 키에 대한 기본값을 먼저 지정
```python
from collections import defaultdict
taemi_table = defaultdict(int) #정수0을 반환하는 함수 int
taemi_table['one'] = 1
taemi_table['two']
#0
taemi_table
defaultdict(<class 'int'>,{'two':0, 'one':1})
```
- 빈 기본값 반환 ( defaultdict 초기 설정시 )
    - int() : 0
    - list() : []
    - dict() : {}
    - 인자 입력하지 않을 경우 : None

- lambda로 인자의 기본 값을 만드는 함수를 정의할 수 있음
```python 
taemi = defaultdict(lambda : 'hey!')
taemi['Q']
#hey!           # 없는 인자
```

- 카운터 함수 만들어보기
```python
from collections import defaultdict
counter = defaultdict(int)      #0을 반환
for number in ['one', 'two', 'three', 'three']
    countet[number] +=1

for number, count in counter.items():
    print(number, count)

# one 1
# two 1
# three 2
```
만약 일반 dict를 만들었다면 분명 에러가 났을 것이다.<br>
새로운 항목 생성을 하지 못하므로<br>
그럴 땐 예외를 피하기 위한 조건문이 필요하다

### 5.5.2 항목세기 : Counter()
 표준 라이브러리에 항목을 셀 수 있는 여러가지 함수들이 존재
1. counter
 ```python
 >>>from collections import Counter
 >>> breakfast = ['spam', 'spam', 'eggs', 'spam']
 >>> breakfast_counter = Counter(breakfast) # 안에 리스트를 넣어줌
 >>> breakfast_counter
 # Counter({'spam':3, 'eggs:1'})

 ```
 2. most_common()
 - 모든 요소를 내림차순으로 반환
 - 숫자 입력 시 그 숫자만큼 상위 요소 반환
 ```python
 >>> breakfast_counter.most_common()         #제일 큰 값인 spam먼저 정렬
 [('spam',3), ('eggs',1)]
 >>> breakfast_counter.most_common(1)        # 가장 큰 값부터 하나의 값, 즉 spam만 출력
 [('spam',3)]
```
- 각 Count함수로 만들어진 counter인자는 +, -, &, |를 사용할 수 있다.
    - + : 각 항목의 합
    - \- : 각 항목의 차 
    - & : 공통되는 값
    - | : 전체값



### 5.5.3 키 정렬하기 : OrderedDict()
- 딕셔너리 키 순서는 에측 불가 ( 순서 x )
- OrderedDict()
    - 키의 추가 순서를 기억하고 이터레이터로부터 순서대로 키값을 반환
```python
>>> from collections import OrderedDict
>>> quotes = OrderedDict([
        ('Moe', 'A wise guy, huh?'),
        ('Larry', 'Ow!'),
        ('Curly', 'Nyuk nyuk!'),
        ])
>>>
>>> for stooge in quotes:
        print(stooge)

#Moe
#Larry
#Curly
```

### 5.5.4 스택 + 큐 == 데크
- 시퀀스의 양 끝으로부텉 항목을 추가하거나 삭제<br><br>
- popleft() : 왼쪽부터 항목 제거 후 항목 반환
- pop() : 오른쪽부터 항목 제거 후 항목 반환
<br><br>
```python
>>> def palindrome(word):
    from collections import deque
    dq = deque(word)
    while len(dq) > 1:
        if de.popleft() != dq.pop():
            return False
    return True

>>> palindrome('racecar')
#True
>>> palindrome('taemi')
#False
```
- 회전문 코드 더 간략하게 써보기 ( 번외 )
```python
>>> def anothor_palindrome(word):
    return word=word[::-1]
```

### 5.5.5 코드 구조 순회하기 : itertools
- itertools는 특수 목적의 이터레이터 함수를 포함
- for ... in 루프에서 이터레이터 함수 호출 시 함수는 한 번에 한 항목만 반환, 호출 상태 기억
<br>
1. chain()  : 순회 가능한 인자들을 하나씩 반환
```python
>>> import itertoos
>>> for item in itertoos.chain([1,2],['a','b']):
        print(item)
#1
#2
#a
#b
```
2. cycle() : 무한 이터레이터
```python
>>> import itertoos
>>> for item in itertoos.cycle([1,2]):
        print(item)
#1
#2
#1
#2
#...계속...
```

3. accomulate() : 축적 값 계산, 합계 계산
```python
>>> import itertoos
>>> for item in itertools.accumilate([1,2,3,4]):
        print(item)
    
#1
#3
#6
#10
```
4. accumulate() : 두번 째 인자를 함수로 전달하여 사용
```python
>>> import itertools
>>> def multiply(a,b):
        return a*b

>>> for item in itertools.accumulate([1,2,3,4], multuply):
        print(item)
#1
#2
#3
#6
#24
```
### 5.5.6 깔끔하게 출력하기 : pprint()
- 가독성을 위해 요소들을 정렬해서 출력
- 일반 print와는 다른 출력을 내보낸다

## 5.6 배터리 장착: 다른 파이썬 코드 가져오기
 원하는 모듈이 없거나 예상대로 동작하지 않을 때<br>

- PyPL
- github
- readthedocs
- activestate 사이트


### 

# 헷갈림
- 모듈 임포트를 이제까지 파일의 맨 위에 선언했는데 함수 안에 넣거나 필요한 곳 바로 윗코드에 모듈을 import해도 실행됨
- 지금까지 counter 함수는 숫자를 세주는 거였는데 python에서는 대부분 안에 있는 같으느 문자열, 변수 등이 몇개가 있는지 세어주는 함수가 많음

# Q
