#객체와 클레스

## 6.1 객체란 무엇인가?
 파이썬의 모든 것은 객체

## 6.2 클래스 선언하기 : class
```python
>>> class Person():
        def __init__(self, name): # 객체 초기화 함수, self인자는 객체 자신을 가리킨다.
            self.name = name
```
-  클래스 실행순서
1. Person 클래스 정의를 찾는다
2. 새 객체를 메모리에 **초기화** ( 생성 )한다
3. 객체의 __init__메서드를 호출, 새롭게 생성된 객체를 self에 전달, 인자를 name에 전달
4. 객체에 name값 저장
5. 새로운 객체 반환
6. hunter에 이 객체를 연결

__init__ 메서드를 모든 클래스 정의에서 가질 필요는 없다.<br>
다만, 같은 클래스에서 생성된 다른 객체를 구별하기 위해서는 사용해야 한다.

## 6.3 상속

- 기존 클래스를 수정하지 않고 기능을 추가하고 싶을 때
- **오버라이드 ( overide )**
- 기존클래스 : 부모클래스, 슈퍼 클래스, 베이스클래스
- 새 클래스 : 자식클래스, 서브클래스, 파생된 클래스
```python
>>> class Person():
    pass
>>> class taemi(Person)
```

## 6.4 메서드 오버라이드

- 부모와 자식 클래스 내부에 같은 이름의 함수가 존재한다면 자식 클래스 내부에 함수가 실행된다
( 자식 클래스로 객체를 만들어 실행할 시)

## 6.5 메서드 추가하기
- 자식 클래스가 부모 클래스에 없는 기능을 추가하는 것 

## 6.6 부모에게 도움받기 : super

```python
>>> class Person():
    def __init__(self, name):
        self.name = name

>>> class EmailPerson():
    def __init__(self, name, email):
        super().__init__(name):         #부모 클래스의 기능을 가져온다
        self.email = email

#super클래스를 보면 self인자가 없다.

```
물론 직접 정의해도 괜찮지만 부모 클래스에서 변경사항이 있을 때 자동변경이 되려면 super를 써야한다.

## 6.7 자신 : self
클래스 안에 함수에 self인자 빼먹지 말 것.<br>
self 인자를 빼게 되면 클래스 객체를 만들었을 때 그 객체로부터 함수를 호출할 수 없다.


## 6.8 get/set 속성값과 프로퍼티
- 외부에서 직접 접근하지 못하도록 getter(get_name()), setter(set_name())메서드를 정의한다.
- 데커레이터 이용
    - getter 메서드 앞에 @propert
    - setter 메서드 앞에 @name.setter

## 6.9 private 네임 맹글링
- 속성 이름 앞에 두 언더스코어(__)를 붙이면 외부에서 볼 수 없는 속성이 된다.
    - 외부에서 접근이 불가능
    - 외부에서 setname 같은 형식으로 이름 지정은 가능하지만 직접 부르기 ( ex. taemi.__name)는 불가

## 6.10 메서드 타입
- 인스턴스 메서드 ( instance method )
    - 첫번 째 매개변수 self
    - 메서드를 호출할 때 객체를 전달
- 클래스 메서드 ( class method )
    - 클래스 전체에 영향
    - 매개변수 : cls
        - 앞 인스턴스 메서드에서는 객체 자신 가리키기 위해 self를 적었지만, 클래서 메서드에서는 자신의 클래스를 가리키기 위해 cls를 썼다.
    - @classmethod

```python
>>> class A():
    def __init__(self):
        a.count += 1
    @classmethod
    def kids(cls):
        print("a has", cls.count, "little objects.)

>>> easy_a = A()
>>> breezy_a = A()
>>> wheez_a = A()
>>> A.kids()
a has 3 little objects
```
## 6.11 덕타이핑
- 다형성 : 클래스에 상관없이 같은 동작을 다른 객체에 적용가능
- 기존 클래스와 상관 없는 클래스가 생성이 되었는데, 이것이 기존 클래스의 기능과 같다면 이것은 기존 클래스라고 할 수 있다.
- 오래처럼 꽥꽥거리고 걷는다면, 이것은 오리다.

## 6.12 특수 메서드
- 우리가 사용하는 일반적인 연산자처럼 사용할 수 있도록 하는 것
- 두 언어스코어(__)로 시작하고 끝난다.
```python
>>> class word():
        def __init__(self, text):
            self.text = text
        def __eq__(self, word2):
            return self.text.lower() == word2.text.lower()

>>> first = word('ha')
>>> second = word('HA')
>>> third = word('eh')
>>> first == second
True
>>> first == third
False
```
여기서 __eq__() 는 같은지 아닌지 판별하는 파이썬의 특수 메서드<br>

- 비교 연산
| __eq__(self, other) | self == other |
| __ne__(self, other) | self != other |
| __lt__(self, other) | self < other  |
| __gt__(self, other) | self > other  |
| __le__(self, other) | self <= other |
| __ge__(self, other) | self >= other |

- 산술 연산
| __add__(self, other)      | self + other  |
| __sub__(self, other)      | self - other  |
| __mul__(self, other)      | self * other  |
| __floordiv__(self, other) | self // other |
| __truediv__(self, other)  | self / other  |
| __mod__(self, other)      | self % other  |
| __pow__(self, other)      | self ** other |

- 기타메서드
| __str__(self) | str(self)  |
| __repr__(self)| repr(self) |
| __len__(self) | len(self)  |

- __Str__() 과 __repr__() 메서드를 추가하여 클래스 만들어보기
```python
>> class Word():
        def __init_(self, text):
            self.text = text
        def __eq__(self, word2):
            return self.text.lower() == word2.text.lower()
        def __str__(self):
            return self.text
        def __repr__(self):
            return "Word(' " + self.text + " ')"
>>> first = Wrod('ha')
>>> first #__repr__ 호출
# Word("ha")
>>> print(first) # __str__호출
# ha
```

## 6.13 컴포지션

- **컴포지션** 또는 **어그리게이션** 
- X has a Y
- 쓰는 방식이 익숙하지 않음
```python
>>> class Bill():
        def __init(self, description):
            self.length = length

>>> class Tail():
        def __init__(self, length):
            self.length = length
>>> class Duck():
        def __init(self, bill, tail):
            self.bill = bill
            self.tail = tail
        def about(self):
            print('this duck has a', self.bill.decription, 'bill and a', self.tail.length, 'tail')
>>> tail = Tail('long')
>>> bill = Bill('wide orange')
>>> duck = Duck(bill, tail)
>>> duck.about()
```
- 위에서 사용한 것 같이 클레스 안에 클레스를 넣어서 내부 변수를 건들일 수 있는 것

## 6.14 클래스와 객체, 그리고 모듈은 언제 사용할까?
- [참고: 클래스와 모듈](https://seongjaemoon.github.io/python/2018/04/06/python-course3.html)

### 6.14.1 네임드 튜플
- 네임드튜플 : 튜플의 서브 클래스
- 이름 (.name)과 위치 ([offset])로 값에 접근할 수 있다.
- 모듈로 불러와야 함
```python
>>>from collections import namedtuple

>>>Duck = namedtuple('Duck','bill tail')         #띄어쓰기로 구분
>>> duck = Duck('wide orange','long')           # bill에 wide orange , 그리고 tail에 long이 들어감
>>> duck                                        #반환하면
Duck (bill = 'wide orange', tail = 'long')      # Duck이라는 네임드튜플 안에 bill과 tail값이 정의되어 있다.
>>> duck.bill                                   # 이름으로 접근 가능
'wide orange'
>>> duck.tail
'long'
```
- 딕셔너리로 네임드 튜플을 만들 수 있음
```python
>>> parts = {'bill':'wide orange', 'tail':'long'}
>>> duck2 = Duck(**parts)                    # **parts는 키워드 인자, 키와 값을 추출해서 Duck에게 인자로 전달
>>> duck2
#Duck(bill = 'wide orange', tail = 'long')      # 바뀌었음
```
- 네임드 튜플의 특징
    - **불변하는 객체**처럼 행동
    - 객체보다 공간 효율성과 시간 효율성이 더 좋다
    - 딕셔러니 형식의 괄호 ([]), 대신, 점(.) 표기법으로 속성에 접근
    - 네임드 튜플으르 딕셔너리의 키처럼 쓸 수 있다.


# 헷갈리는 거
- 아직 독립적으로 네임드튜플을 잘 쓰진 못할 것 같음
