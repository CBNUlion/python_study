# 객체와 클래스

## 6.1 객체란 무엇인가?

객체는 아래 두 가지를 포함한다.

- 데이터(변수, 속성)
- 코드(함수, 메서드)

객체는 어떤 구체적인 것의 유일한 인스턴스를 나타낸다. **파이썬의 모든 것은 객체다!**

## 6.2 클래스 선언하기: class

클래스는 박스를 만드는 툴에 비유할 수 있다.

> 예를 들면, String은 'cat'와 같은 문자열 객체를 만드는 내장된 클래스이다.

빈 클래스를 만들어보자

```python
class Person():
    pass
```

함수처럼 클래스 이름을 호출하여 클래스로부터 객체를 생성할 수 있다.

```python
someone = Person() # 객체 생성
```

Person()은 Person 클래스로부터 개별 객체를 생성하고, someone 변수에 할당했다.

```python
class Person():
    def __init__(self): # 객체 초기화 메서드 정의
        pass
```

**\_\_init\_\_ 메서드는 클래스의 정의로부터 객체를 초기화**하는 역할을 한다. **그리고 self 인자는 객체 자기 자신을 가리킨다.** 클래스에서 \_\_init\_\_을 정의할 때, **첫 번째 매개변수는 self여야 한다.**(꼭 인자명이 self일 필요는 없지만 관용적으로 self를 사용한다)

```python
class Person():
    def __init__(self, name):
        self.name = name
```

name 매개변수에 문자열을 전달하여 Person 클래스로부터 객체를 생성할 수 있다.

```python
hunter = Person('Elmer Fudd') # 객체 생성 및 초기화
```

코드가 동작하는 방식은

- Person 클래스의 정의를 찾고
- 새 객체를 메모리에 초기화(생성) 하고
- 객체의 \_\_init\_\_ 메소드를 호출한다. 새롭게 생성된 객체를 self에 전달하고 인자를 전달한다.
- 객체에 name 값을 저장한다
- 새로운 객체를 반환한다
- hunter에 이 객체를 연결한다

객체의 속성을 직접 읽고 쓸 수 있다.

```python
print("name is", hunter.name) # name is Elmer Fudd
```

hunter와 같은 객체를 생성할 때, 이것을 hunter.name이라고 여긴다! 모든 클래스가 \_\_init\_\_ 메서드를 사질 필요는 없다. **\_\_init\_\_ 메서드는 같은 클래스에서 생성된 다른 객체를 구분하기 위해 필요한 무언가를 수행한다!!!!!!!!**

## 6.3 상속

기존 클래스에서 일부를 추가하거나 변경하여 새 클래스를 생성한다. **상속을 이용하면 새로운 클래스는 기존 클래스를 복사하지 않고, 기존 클래스의 모든 코드를 쓸 수 있다.**

필요한 것만 추가 / 변경하여 새 클래스를 정의한다. **그리고 이것은 기존 클래스의 행동을 오버라이드(재정의) 한다.** 기존 클래스는 부모 | **슈퍼** | 베이스 클래스라고 부르고, 새 클래스는 자식 | **서브** | 파생된 클래스라고 부른다.

```python
class Car():
    pass

class Yugo(Car): # 슈퍼클래스로부터 상속
    pass
```

빈 클래스 Car를 정의했다. 그리고 Car의 서브클래스인 Yugo를 정의했다.

```python
give_me_a_car = Car()
give_me_a_yugo = Yugo()
```

각 클래스로부터 객체를 생성했다. **give_me_a_yugo 객체는 Yugo 클래스의 인스턴스지만, 또한 Car 클래스가 할 수 있는 어떤 것을 상속받는다.**

```python
class Car():
    def exclaim(self):
        print("I'm a Car!")

class Yugo(Car):
    pass

car = Car()
yugo = Yugo()
yugo.exclaim() # I'm a Car!
car.exclain() # I'm a Car!
```

Yugo 클래스는 아무것도 하지않고 슈퍼클래스로부터 상속 받았다. 때문에 exclaim 메소드를 사용할 수 있다.

## 6.4 메서드 오버라이드

새 클래스는 부모 클래스로부터 모든 것을 상속받는다. **부모 메소드를 대체 혹은 오버라이드할 수 있다.**

```python
class Car():
    def exclaim(self):
        print("I'm a Car!")

class Yugo(Car):
    def exclaim(self):
        print("I'm a Yugo!")

car = Car()
yugo = Yugo()

car.exclaim() # I'm a Car!
yugo.exclaim() # I'm a Yugo!
```

서브클래스에서 슈퍼클래스의 exclaim 메소드를 오버라이드(재정의) 했다. **init** 메소드를 포함한 모든 것들을 재정의할 수 있다!

```python
class Person():
    def __init__(self, name):
        self.name = name

class MDPerson(Person):
    def __init__(self, name):
        self.name = "Doctor " + name

class JDPerson(Person):
    def __init__(self, name):
        self.name = name + ", Esquire"

person = Person('Fudd')
doctor = MDPerson('Fudd')
lawyer = JDPerson('Fudd')

print(person.name) # Fudd
print(doctor.name) # Doctor Fudd
print(lawyer.name) # Fudd, Esquire
```

**init** 메소드도 재정의했다.

## 6.5 메서드 추가하기

서브클래스는 슈퍼클래스에 없는 메서드도 추가할 수 있다.

```python
class Car():
    def exclaim(self):
        print("I'm a Car!")

class Yugo(Car):
    def exclaim(self):
        print("I'm a Yugo!")

    def need_a_push(self):
        print("A little help here?")

car = Car()
yugo = Yugo()

yugo.need_a_push() # A little help here?
car.need_a_push() # 에러 발생
```

need_a_push 메소드는 서브클래스의 객체에서만 사용할 수 있다.

## 6.6 부모에게 도움 받기: super

서브 클래스에서 슈퍼 클래스의 메소드를 호출하는 방법이다.

```python
class Person():
    def __init__(self, name):
        self.name = name

class EmailPerson(Person):
    def __init__(self, name, email):
        super().__init__(name)
        self.email = email
```

**서브 클래스에서 \_\_init\_\_을 정의하면 더 이상 슈퍼 클래스의 \_\_init\_\_은 호출되지 않는다.** 따라서 명시적으로 슈퍼 클래스의 \_\_init\_\_을 호출해주어야 한다.

- super() 메소드는 슈퍼 클래스(Person)의 정의를 얻는다
- **init** 메소드는 Person.**init**() 메소드를 호출한다. 이 메소드는 self 인자를 슈퍼 클래스로 전달하는 역할을 한다. 그러므로 슈퍼 클래스에는 어떤 선택적 인자를 제공하기만 하면 된다. (지금의 경우 name을 제공한다)
- self.email = email은 새로운 코드이다

새로운 객체를 생성한다

```python
bob = EmailPerson('Bob Frapples', 'bob@naver.com')

bob.name # Bob Frapples
bob.email # bob@naver.com
```

왜 서브 클래스에서 다음과 같이 하지 않았을까?

```python
class EmailPerson(Person):
    def __init__(self, name, email):
        self.name = name
        self.email = email
```

**위의 코드로는 상속을 사용할 수 없다.** 슈퍼 클래스인 Person의 \_\_init\_\_이 변경되어도 서브 클래스에는 영향을 미치지 않기 때문에 불편하다. 즉, **슈퍼 클래스의 변경사항을 자동으로 반영하기 위해서 super() 메소드를 사용해서 상속받는다.**

## 6.7 자신: self

**파이썬은 적절한 객체의 속성과 메서드를 찾기 위해 self 인자를 사용한다.**

이전의 Car 클래스 예제를 보자

```python
car = Car()
car.exclaim() # I'm a Car!
```

다음과 같은 처리를 내부적으로 수행한다

- car 객체의 Car 클래스를 찾는다
- **car 객체를 Car 클래스의 exclaim 메소드의 self 매개변수에 전달한다.**

때문에 아래와 같이 해도 동작한다.

```python
Car.exclaim(car) # I'm a Car!
```

하지만 이렇게 사용할 이유는 없다!!

## 6.8 get / set 속성값과 프로퍼티

Java에서는 외부로부터 바로 접근할 수 없는 private 객체 속성을 지원한다. **이 private한 객체 속성의 값을 읽고 쓰기 위해 getter 메서드와 setter 메서드를 사용한다.**

하지만 Python에서는 모든 속성과 메서드는 public하기 때문에 getter나 setter 메서드가 필요없다. **만약 속성에 직접 접근하는 것이 부담스럽다면 getter와 setter를 작성해도 되지만 pythonic하게 프로퍼티(Property)를 사용하자.**

```python
class Duck():

    def __init__(self, input_name):
        self.hidden_name = input_name

    def get_name(self):
        print('inside the getter')
        return self.hidden_name

    def set_name(self, input_name):
        print('inside the setter')
        self.hidden_name = input_name

    name = property(get_name, set_name)

fowl = Duck('howard')
fowl.name
# inside the getter
# howard

fowl.name = 'daffy'
# inside the setter
# 그리고 daffy로 값이 변경된다

fowl.name
# inside the getter
# daffy
```

Duck 클래스를 정의하고 직접 접근하지 못하도록 getter와 setter를 만들었다. 하지만 프로퍼티가 아닌 각 메서드 직접 호출도 가능하다.

```python
fowl.get_name()
# inside the getter
# daffy

fowl.set_name('haha')
# inside the setter
```

프로퍼티를 정의하는 또 다른 방법은 데코레이터를 이용하는 것이다.

```python
class Duck():

    def __init__(self, input_name):
        self.hidden_name = input_name

    @property
    def name(self):
        print('inside the getter')
        return self.hidden_name

    @name.setter
    def name(self, input_name):
        print('inside the setter')
        self.hidden_name = input_name
```

getter와 setter 각 메서드에는 아래와 같은 서로 다른 데코레이터를 이용한다.

- getter 메서드 앞에는 @property
- setter 메서드 앞에는 @메서드\_이름.setter

**여전히 name을 속성처럼 접근할 수 있지만 get_name()과 set_name() 메서드는 존재하지 않기 때문에 메서드 직접 호출이 불가능하다.**

**또한 프로퍼티는 계산된 값을 참조할 수 있다.**

```python
class Circle():
    def __init__(self, radius):
        self.radius = radius

    @property
    def diameter(self):
        return 2 * self.radius

c = Circle(5)
c.radius # 5
c.diameter # 10

c.radius = 7 # radius의 값을 변경
c.radius # 7
c.diameter # 14
```

만약 속성에 대한 setter 프로퍼티를 명시하지 않았다면 외부로부터 이 속성을 설정할 수 없다. 즉, 읽기전용 속성이 되는 것이다.

```python
c.diameter = 10 # AttributeError: can't set attribute
```

직접 속성을 접근하는 것보다 프로퍼티를 통해서 접근하면 큰 이점이 있다. 만약 속성의 정의를 바꾸려면 모든 호출자를 수정할 필요 없이 클래스 정의에 있는 코드만 수정하면 된다.

## 6.9 private 네임 맹글링

파이썬은 클래스 정의 외부에서 볼 수 없도록 하는 속성에 대한 네이밍 컨벤션이 있다.

> 속성 앞에 \_\_(언더스코어 두 개)를 붙인다.

```python
class Duck():

    def __init__(self, input_name):
        self.__name = input_name

    @property
    def name(self):
        print('getter')
        return self.__name

    @name.setter
    def name(self, input_name):
        print('setter')
        self.__name = input_name

a = Duck('a')
a.name
# getter
# a

a.name = 'b'
# setter

a.__name
# AttributeError: 'Duck' object has no attribute '__name'
```

\_\_name 속성에 바로 접근 하려고하면 AttributeError 예외가 발생한다. 이 네이밍 컨벤션은 속성을 완벽히 private하게 만들지는 않지만, 파이썬은 이 속성이 우연히 외부 코드에서 발견할 수 없도록 이름을 맹글링(manggling)했다.

직접 접근하려면 클래스 이름을 이용해야 한다.

```python
a._Duck__name # 'b'
```

## 6.10 메서드 타입

어떤 데이터(속성)과 함수(메서드)는 클래스 자신의 일부고, 어떤 것은 클래스로부터 생성된 객체의 일부다.

**클래스 정의에서 메서드의 첫번째 인자가 self라면 이 메서드는 인스턴스 메서드이다.** 가장 일반적인 경우이며 파이썬은 이 메서드를 호출할 때 객체를 전달한다.

**클래스 메서드는 클래스 전체에 영향을 미친다.** 클래스에 대한 어떤 변화는 모든 객체에 영향을 미친다. **클래스 정의에서 함수에 @classmethod 데코레이터가 있다면 이것은 클래스 메서드이고, 이 메서드의 첫 번째 매개변수는 클래스 자기 자신이다.** 보통 매개변수를 cls로 쓴다.

```python
class A():
    count = 0

    def __init__(self):
        A.count += 1

    def exclaim(self):
        print("I'm an A!")

    @classmethod
    def kids(cls):
        print("A class has {} objects.".format(cls.count))

a = A()
b = A()
b.kids() # A class has 2 objects.
c = A()
b.kids() # A class has 3 objects.
c.kids() # A class has 3 objects.
```

클래스 정의에서 메서드의 세 번째 타입은 클래스나 객체에 영향을 미치지 못한다. 편의를 위해 존재하는 것이다. **정적 메서드는 @staticmethod 데코레이터를 사용하며, 첫 번째 매개변수로 self나 cls가 없다.**

```python
class A():
    @staticmethod
    def commercial():
        print("this A has been brought to you by Acme")

A.commercial() # this A has been brought to you by Acme
```

**static 메서드에 접근하기 위해서 클래스로부터 객체를 생성할 필요가 없다.** 바로 클래스를 통해서 메서드를 사용하면 된다.

## 6.11 덕 타이핑

파이썬은 다형성을 느슨하게 구현했다. **이것은 클래스에 상관없이 같은 동작을 다른 객체에 적용할 수 있다는 것을 의미한다.**

```python
class Quote():
    def __init__(self, person, words):
        self.person = person
        self.words = words

    def who(self):
        return self.person

    def says(self):
        return self.words + '.'

class QuestionQuote(Quote):
    def says(self):
        return self.words + '?'

class ExclamationQuote(Quote):
    def says(self):
        return self.words + '!'

hunter = Quote('Elmer Fudd', "I'm hunting wabbits")
print(hunter.who(), 'says:', hunter.says()) # Elmer Fudd says: I'm hunting wabbits.

hunted1 = QuestionQuote('Bugs Bunny', "What's up, doc")
print(hunter.who(), 'says:', hunted1.says()) # Elmer Fudd says: What's up, doc?

hunted2 = ExclamationQuote('Daffy Duck', "It's rabbit season")
print(hunted2.who(), 'says:', hunted2.says()) # Daffy Duck says: It's rabbit season!
```

위의 세 개의 서로 다른 says() 메서드는 세 클래스에 대해 서로 다른 동작을 제공한다. 이것이 **객체 지향 언어에서 전통적인 다형성의 특징이다.** 파이썬은 who()와 says() 메서드를 갖고 있는 모든 객체에서 이 메서드들을 실행할 수 있게 해준다.

```python
class BabblingBrook():
    def who(self):
        return 'Brook'

    def says(self):
        return 'Babble'

brook = BabblingBrook()
```

다양한 객체의 who()와 says() 메서드를 실행해보자. brook 객체는 다른 객체와 전혀 관계가 없다.

```python
def who_says(obj):
    print(obj.who(), 'says', obj.says())

who_says(hunter) # Elmer Fudd says I'm hunting wabbits.
who_says(hunted1) # Bugs Bunny says What's up, doc?
who_says(hunted2) # Daffy Duck says It's rabbit season!
who_says(brook) # Brook says Babble
```

이러한 행위를 **덕 타이핑**이라고 부른다. Quote 클래스와 BabblingBrook 클래스는 전혀 상관관계가 없지만 각 클래스의 객체를 호출하는 who_says() 함수에 의해 정상적으로 실행된다. 즉, 덕 타이핑이란 **실제 타입(클래스)은 상관하지 않고, 구현된 메서드로만 판단하는 방식**을 의미한다.

> **속성과 메소드 존재에 의해 객체의 적합성이 결정된다.**

> 파이썬 튜토리얼은 덕 타이핑을 아래와 같이 설명하고 있다.
>
> 객체의 타입을 다른 타입 객체와의 명시적인 관계를 비교하는 것이 아니라, 그 객체의 메서드나 속성들을 비교함으로써 판별하는 파이썬적인 프로그래밍 스타일이다. (“오리처럼 보이고, 오리처럼 운다면 오리임에 틀림없다.”) 특정 타입 대신 인터페이스를 강조함으로써, 잘 디자인된 코드는 다형적 대체를 허용함으로써 유연성을 향상시킬 수 있다. 덕 타이핑을 이용하면 type()이나 isinstance()를 이용한 테스트를 하지 않는다. 대신, 대개 hasattr() 테스트를 이용하거나, 혹은 EAFP (Easier to ask forgiveness than permission; 하고 나서 용서를 비는 것이 하기 전에 허락을 구하는 것보다 쉽다) 프로그래밍 기법을 이용한다.

## 6.12 특수 메서드

파이썬의 특수 메서드는 두 언더스코어(\_\_)로 시작하고 끝난다.

Word 클래스와 두 단어를 비교하는 equals() 메서드를 만들어 보자

```python
class Word():
    def __init__(self, text):
        self.text = text

    def equals(self, text2):
        return self.text.lower() == text2.text.lower()

a = Word('ha')
b = Word('HA')
c = Word('eh')

a.equals(b) # True
```

파이썬의 내장된 타입처럼 a == b와 같이 비교할수 있게 만들어보자

```python
class Word():
    def __init__(self, word):
        self.word = word

    def __eq__(self, word2):
        return self.word.lower() == word2.word.lower()

a = Word('ha')
b = Word('HA')
c = Word('eh')

a == b # True
a == c # False
```

\_\_eq\_\_()는 같은지 판별하는 파이썬의 특수 메서드이다.

파이썬의 특수 메서드는 아래와 같다.

- 비교 연산을 위한 특수 메서드

|                         |               |
| ----------------------- | ------------- |
| \_\_eq\_\_(self, other) | self == other |
| \_\_ne\_\_(self, other) | self != other |
| \_\_lt\_\_(self, other) | self < other  |
| \_\_gt\_\_(self, other) | self > other  |
| \_\_le\_\_(self, other) | self <= other |
| \_\_ge\_\_(self, other) | self >= other |

- 산술 연산을 위한 특수 메서드

|                               |                 |
| ----------------------------- | --------------- |
| \_\_add\_\_(self, other)      | self + other    |
| \_\_sub\_\_(self, other)      | self - other    |
| \_\_mul\_\_(self, other)      | self \* other   |
| \_\_floordiv\_\_(self, other) | self // other   |
| \_\_truediv\_\_(self, other)  | self / other    |
| \_\_mod\_\_(self, other)      | self % other    |
| \_\_pow\_\_(self, other)      | self \*\* other |

- 기타 특수 메서드

|                    |            |
| ------------------ | ---------- |
| \_\_str\_\_(self)  | str(self)  |
| \_\_repr\_\_(self) | repr(self) |
| \_\_len\_\_(self)  | len(self)  |

대화식 인터프리터는 변수의 결과를 출력하기 위해 **repr**() 함수를 사용한다. **str**() 또는 **repr**()을 정의하지 않으면 객체의 기본 문자열을 출력한다.

```python
class Word():
    def __init__(self, text):
        self.text = text

    def __eq__(self, text2):
        return self.text.lower() == text2.text.lower()

    def __str__(self):
        return self.text

    def __repr__(self):
        return "Word('" + self.text + "')"

a = Word('ha')
a # Word('ha')
print(a) # ha
```

## 6.13 컴포지션

서브 클래스가 슈퍼 클래스처럼 행동하고 싶을 때, 상속은 좋은 기술이다. 하지만 컴포지션 또는 어그리게이션의 사용이 더 적절한 경우도 있다.

```python
class Bill():
    def __init__(self, description):
        self.description = description

class Tail():
    def __init__(self, length):
        self.length = length

class Duck():
    def __init__(self, bill, tail):
        self.bill = bill
        self.tail = tail

    def about(self):
        print('This duck has a', self.bill.description, 'bill and a', self.tail.length, 'tail')

tail = Tail('wide orange')
bill = Bill('long')
duck = Duck(bill, tail)
duck.about() # This duck has a long bill and a wide orange tail
```

**다른 클래스의 일부 기능을 그대로 이용하고 싶으나, 전체 기능 상속은 피하고 싶을 때 사용한다.**

## 6.14 클래스와 객체, 그리고 모듈은 언제 사용할까?

- 비슷한 행동(메서드)을 하지만 내부 상태(속성)가 다른 개별 인스턴스가 필요할때 객체를 사용
- 클래스는 상속을 지원하지만, 모듈은 상속을 지원하지 않는다
- 어떤 한 가지 일만 수행한다면 모듈이 가장 좋은 선택(프로그램에서 파이썬 모듈이 참조된 획수에 상관없이 단 하나의 복사본만 불러옴)
- 여러 함수에 인자로 전달될 수 있는 여러 값을 포함한 여러 변수가 있다면, 클래스를 정의하는 것이 좋다.
- 딕셔너리, 리스트, 튜플은 모듈보다 더 작고, 간단하며, 빠르다. 그리고 일반적으로 모듈은 클래스보다 더 간단하다.

### 6.14.1 네임드 튜플

네임드 튜플은 튜플의 서브클래스이다. 이름(.name)과 위치([offset])로 값에 접근할 수 있다.

```python
from collections import namedtuple

Duck = namedtuple('Duck', 'bill tail')
duck = Duck('wide orange', 'long')
duck # Duck(bill='wide orange', tail='long')
duck.bill # 'wide orange'
duck.tail # 'long'
duck[1] # 'long'
```

네임드 튜플의 특징이다.

- 불별하는 객체처럼 행동한다
- 객체보다 공간 효율성과 시간 효율성이 더 좋다
- 딕셔너리 형식의 괄호대신 점 표기법으로 속성에 접근할 수 있다
- 네임드 튜플을 딕셔너리의 키처럼 쓸 수 있다
