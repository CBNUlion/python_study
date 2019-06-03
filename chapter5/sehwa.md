# 5장 파이 포장하기 : 모듈, 패키지, 프로그램

> 데이터 타입 < 자료구조 < 함수 < 클래스 < 모듈 < 패키지 < 프로그램

## 5.1 스탠드얼론 프로그램

> OS으로부터 독립하여 자체적으로 실행이 가능한 프로그램
> 대화식 인터프리터 실행 대신 .py 파일을 만들고 터미널에서 실행한다. 


## 5.2 커맨드 라인 인자

> **sys.argv**
> 프로그램 실행 시 인자를 list()형식으로 반환해준다.
```python
import sys

if len(sys.argv) is 1:
  print("옵션을 주지 않고 이 스크립트를 실행하셨군요")


print("옵션 개수: %d" % (len(sys.argv) - 1))


print("\n< 옵션 목록 >")

for i in range(len(sys.argv)):
  print("sys.argv[%d] = '%s'" % (i, sys.argv[i]))
```

> <참고> 파이썬 argparse (커맨드라인 인자를 다루는 방법) : http://blog.naver.com/PostView.nhn?blogId=cjh226&logNo=220997049388&parentCategoryNo=&categoryNo=17&viewDate=&isShowPopularPosts=false&from=section 


## 5.3 모듈과 import문

> 프로그램이 길어짐에 따라, 유지를 위해 여러 개의 파일로 나눈다.
> 여러 프로그램에 썼던 편리한 함수의 정의를 복사하지 않고도 사용할 수 있다.
> --> 모듈
> import문을 통해 모듈의 코드를 참조한다.

### 5.3.1 모듈 임포트하기

> - 함수 밖에서 import : 임포트된 코드가 여러 장소에서 사용되는 경우
> - 함수 안에서 import : 임포트된 코드의 사용이 내부에 제한되는 경우

### 5.3.2 다른 이름으로 모듈 임포트하기

> as를 사용하여 다른 이름으로 임포트할 수 있다.
> **import [모듈] as [다른 이름]**

### 5.3.3 필요한 모듈만 임포트하기

> 모듈 전체 혹은 모듈의 필요한 부분만 임포트할 수 있다.
> **from [모듈] import [모듈의 함수]** 
> **from [모듈] import [모듈의 함수] as [다른 이름]**

### 5.3.4 모듈 검색 경로

> 모듈의 경로 출력
```python
import sys

for place in sys.path:
	print(place)

```

> 중복된 이름의 모듈이 있다면, 첫 번째 조건을 사용한다.
> <참고> https://docs.python.org/ko/3/tutorial/modules.html

## 5.4 패키지

> 패키지는 모듈을 디렉토리 형식으로 구조화한 것이다.
> <참고> https://offbyone.tistory.com/106


## 5.5 파이썬 표준 라이브러리

> <참고> 표준 라이브러리 : https://docs.python.org/ko/3/tutorial/stdlib.html

### 5.5.1 누락된 키 처리하기 : setdefault(), defaultdict()

> setdefault() : get()함수와 같은 역할, 키가 누락된 경우 항목을 할당할 수 있다.
> defaultdict() : setdefault()함수와 같은 역할, 함수의 인자를 누락된 키에 할당한다.

### 5.5.2 항목 세기 : Counter()

> **from collections import Counter**
> - most_common()을 이용해 모든 요소를 내림차순으로 반환한다.
> - '+' 와 '-' 연산자를 사용할 수 있다.
> - '&' 와 '|' 연산자를 사용할 수 있다.

### 5.5.3 키 정렬하기 : OrderedDict()

> **from collections import OrderedDict**
> **OrderedDict([('key1':'value1'), ('key2':'value2')])**

### 5.5.4 스택 + 큐 == 데크

> **from collections import deque**
>
>      =========================
>          |    |    |    |    |  ** 스택 **
>      =========================
>
>      =========================
>          |    |    |    |       ** 큐 **
>      =========================
>
>      =========================
>          |    |    |    |    #  ** 데크 **
>      =========================
>
> 사용할 수 있는 함수
> - append
> - appendleft
> - count
> - extend
> - extendleft
> - index
> - insert
> - maxlen
> - pop
> - popleft
> - remove

### 5.5.5 코드 구조 순회하기 : itertools

> - chain() : 순회 가능한 인자를 하나씩 반환한다.
> - cycle() : 인자를 무한으로 순환한다.
> - accumulate(,fun) : 축적된 값을 토대로 계산한다.
> - repeat() : 요소를 지정 개수만큼 반복한다.
>
> <참고> itertools : https://hamait.tistory.com/803

### 5.5.6 깔끔하게 출력하기 : pprint()

> 멋진 프린터 호호
> 가독성을 위해 요소들을 정렬하여 출력한다.

## 5.6 배터리 장착 : 다른 파이썬 코드 가져오기

> PyPi, github, readthedocs에서 오픈소스를 사용해보자.


