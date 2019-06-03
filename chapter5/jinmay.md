# 파이 포장하기: 모듈, 패키지, 프로그램

## 5.2 커맨드 라인 인자

~~~python
# vi test1.py
import sys
print('args': sys.argv)

python test1.py 1, 2, 3, 4, 5
# args:  ['test1.py', '1', '2', '3', '4', '5']
~~~

## 5.3 모듈과 import문

import 문을 사용하여 다른 모듈의 코드를 참조할 수 있다. 임포트한 모듈의 코드와 변수를 프로그램에서 사용할 수 있다

### 5.3.1 모듈 임포트하기

import 문을 사용해서 모듈을 임포트할 수 있다. 모듈이란 .py 확장자가 없는 파이썬 파일이 이름이다.

~~~python
# 메인 프로그램
# vi weatherman.py
import report

description = report.get_description()
print("Weather description: ", description)

# 모듈
# vi report.py
def get_description():
    return '오늘은 화창합니다'
~~~

위의 두 파일은 같은 디렉토리에 저장한다. weahterman.py를 실행하면 메인 프로그램은 report 모듈에 접근해서 get_description() 함수를 실행한다. 그 결과 description 변수에 저장이 되며 출력이 된다.

~~~python
python weatherman.py
# Weather description:  오늘은 화창합니다
~~~

### 5.3.2 다른 이름으로 모듈 임포트하기

alias를 이용해서 모듈 이름을 바꿔서 임포트 할 수 있다.

~~~python
import report as wr
description = wr.get_description() # report.get_description()와 같다
~~~

### 5.3.3 필요한 모듈만 임포트하기

지금까지는 모듈의 모든 부분을 임포트했다. 하지만 필요한 부분만 임포트도 가능하다.

~~~python
from report import get_description
description = get_description()
print("Weather description: ", description)
~~~

alias를 사용하면 아래와 같이 쓸 수 있다.

~~~python
from report import get_description as do_it
description = do_it() # get_description의 이름이 do_it으로 변했다
~~~

### 5.3.4 모듈 검색 경로

파이썬은 임포트할 파일을 디렉터리 이름의 리스트와 표준 sys 모듈에 저장되어 있는 ZIP 아카이브 파일을 변수 path로 사용한다. 

~~~python
import sys
for place in sys.path:
    print(place)
~~~

모듈을 찾는 경로리스트가 출력이 된다. 만약 중복된 이름의 모듈이 있다면 처음으로 만난 경로를 사용한다. 즉, 우리가 random 모듈을 정의하고, 이 모듈이 파이선 표준 라이브러리를 찾기 전의 경로에 있다면 표준 라이브러리의 random을 절대로 접근하지 못하게 된다.

## 5.4 패키지

패키지를 만들어보자

~~~python
# 메인 프로그램
# vi boxes/weather.py
from sources import daily, weekly

print("Daily: ", daily.forecast())
print("Weekly: ", weekly.forcast())

# vi boxes/sources/daily.py
def forcast():
    return 'like yesterday'

# vi boxes/sources/weekly.py
def forecast():
    return 'I do not know...TT'
~~~

중요한 점으로는 sources 폴더에 \_\_init\_\_.py 파일을 만들어 주어야 한다. **파일의 내용은 비워도 되지만, 파이썬은 이 파일을 포함하는 디렉토리를 패키지로 간주한다!!**

## 5.5 파이썬 표준 라이브러리

파이썬의 장점 중 하나는 배터리 포함(batteries included)이라는 철학으로 유용한 작업을 처리 하는 많은 표준 라이브러리 모듈이 있다는 것이다. 

### 5.5.1 누락된 키 처리하기: sedefault(), defaultdict()

존재하지 않는 키로 dict에 접근하면 예외가 발생한다. 설정된 기본값을 반환하는 get() 함수를 사용하면 이 예외를 피할 수 있다. 또한 setdefault() 함수는 get() 함수와 같지만 키가 없는 경우 새로 딕셔너리에 항목을 할당할 수 있다.

존재하는 키에 접근한다면 값이 변경되고, 키가 존재하지 않는다면 새로은 항목이 할당된다. 

~~~python
test = {
    'a': 1,
    'b': 2
}
test.setdefault('c', 3)
test # {'a': 1, 'b': 2, 'c': 3}
~~~

defaultdict() 함수는 새 키에 대한 기본값을 먼저 지정한다.

~~~python
from collections import defaultdict
test_dict = defaultdict(int) # 새 키에 대한 기본값이 0 으로 지정된다

test_dict['a'] = 'first'
test_dict['b']
test_dict # defaultdict(int, {'a': 'first', 'b': 0})

test_dict['c']
test_dict # defaultdict(int, {'a': 'first', 'b': 0, 'c': 0})
~~~

defaultdict()의 인자는 값을 누락된 키에 할당하여 반환한다. 명시적으로 값을 넣어 주어도 되지만 함수도 가능하다.

~~~python
from collections import defaultdict

def default_value():
    return 'DEFAULT'

test_dict = defaultdict(default_value)
test_dict['a'] = 1234
test_dict['b']
test_dict # defaultdict(<function __main__.default_value()>, {'a': 1234, 'b': 'DEFAULT'})
~~~

인자를 입력하지 않으면 새로운 키의 초기값이 None으로 설정된다. 

~~~python
from collections import defaultdict
food_counter = defaultdict(int)
# food_counter = {} -> KeyError 발생
for food in ['spam' ,'spam' ,'eggs', 'spam']:
    food_counter[food] += 1

for food, count in food_counter.items():
    print(food, count)
~~~

만약 food_counter 딕셔너리가 defaultdict형 dict가 아닌 일반적인 dict 였다면 KeyError가 발생했을 것이다. 값이 초기화 되어 있지 않은 항목에 +1 연산을 하기 때문이다. 

### 5.5.2 항목 세기: Counter()

~~~python
from collections import Counter
breakfast = ['spam' ,'spam' ,'eggs', 'spam']
breakfast_counter = Counter(breakfast)
breakfast_counter # Counter({'spam': 3, 'eggs': 1})

# most_common() 함수
breakfast_counter.most_common() # [('spam', 3), ('eggs', 1)]

# 숫자를 입력하는 경우 그 숫자만큼 상위 요소를 반환
breakfast_counter.most_common(1) # [('spam', 3)]
~~~

리스트처럼 처럼 +과 - 연산도 지원한다

### 5.5.3 키 정렬하기: OrderedDict()

기본 딕셔너리는 순서를 보장하지 않기 때문에 사용할때마다 항목의 순서가 바뀔 수 있다. 딕셔너리의 항목을 정렬하고 싶다면 OrderedDict을 써야한다

OrderedDict은 키의 추가 순서를 기억하고, 이터레이터로부터 순서대로 키 갓을 반환한다.

~~~python
from collections import OrderedDict
test = OrderedDict([
    ('a', 1),
    ('b', 2),
    ('c', 3)
])

for x in test:
    print(x)
~~~

### 5.5.4 스택 + 큐 == 데크(deque)

데크는 스택과 큐의 기능을 모두 가진 큐이다. pop()과 leftpop()이 있다.

~~~python
def palindrome(word):
    from collections import deque
    dq = deque(word)
    while len(dq) > 1:
        if dq.popleft() != dq.pop():
            return False
    return True

palindrome('a') # True
palindrome('fsdafe') # False
palindrome('racecar') # True
~~~

### 5.5.5 코드 구조 순회하기: itertools

itertools는 특수 목적의 이터레이터 함수를 포함하고 있다. 

~~~python
import itertools

# chain
for item in itertools.chain([1, 2], ('a', 'b')):
    print(item)

# 1
# 2
# a
# b

# cycle
for item in itertools.cycle(('a', 'b')):
    print(item)

# a
# b
# 무한 출력

# accumulate - 축적된 값 계산
for item in itertools.accumulate([1, 2, 3, 4]):
    print(item)

# accumulate - 함수를 전달해서 사용 가능
def multiply(a, b):
    return a * b

for item in itertools.accumulate([1, 2, 3, 4], multiply):
    print(item)

# 1
# 2
# 6
# 24
~~~

### 5.5.6 깔끔하게 출력하기: pprint()

가독성을 높혀준다.