# 객체와 클래스

## 6.1 객체란 무엇인가?

객체는 아래 두 가지를 포함한다.

* 데이터(변수, 속성)
* 코드(함수, 메서드)

객체는 어떤 구체적인 것의 유일한 인스턴스를 나타낸다. **파이썬의 모든 것은 객체다!**

## 6.2 클래스 선언하기: class

클래스는 박스를 만드는 툴에 비유할 수 있다. 

> 예를 들면, String은 'cat'와 같은 문자열 객체를 만드는 내장된 클래스이다.

빈 클래스를 만들어보자

~~~python
class Person():
    pass
~~~

함수처럼 클래스 이름을 호출하여 클래스로부터 객체를 생성할 수 있다.

~~~python
someone = Person() # 객체 생성
~~~

Person()은 Person 클래스로부터 개별 객체를 생성하고, someone 변수에 할당했다.

~~~python
class Person():
    def __init__(self): # 객체 초기화 메서드 정의
        pass
~~~

**\_\_init\_\_ 메서드는 클래스의 정의로부터 객체를 초기화**하는 역할을 한다. **그리고 self 인자는 객체 자기 자신을 가리킨다.** 클래스에서 \_\_init\_\_을 정의할 때, **첫 번째 매개변수는 self여야 한다.**(꼭 인자명이 self일 필요는 없지만 관용적으로 self를 사용한다)

~~~python
class Person():
    def __init__(self, name):
        self.name = name
~~~

name 매개변수에 문자열을 전달하여 Person 클래스로부터 객체를 생성할 수 있다.

~~~python
hunter = Person('Elmer Fudd') # 객체 생성 및 초기화
~~~

코드가 동작하는 방식은

* Person 클래스의 정의를 찾고
* 새 객체를 메모리에 초기화(생성) 하고
* 객체의 \_\_init\_\_ 메소드를 호출한다. 새롭게 생성된 객체를 self에 전달하고 인자를 전달한다.
* 객체에 name 값을 저장한다
* 새로운 객체를 반환한다
* hunter에 이 객체를 연결한다

객체의 속성을 직접 읽고 쓸 수 있다.

~~~python
print("name is", hunter.name) # name is Elmer Fudd
~~~

hunter와 같은 객체를 생성할 때, 이것을 hunter.name이라고 여긴다! 모든 클래스가 \_\_init\_\_ 메서드를 사질 필요는 없다. **\_\_init\_\_ 메서드는 같은 클래스에서 생성된 다른 객체를 구분하기 위해 필요한 무언가를 수행한다!!!!!!!!**

## 6.3 상속

기존 클래스에서 일부를 추가하거나 변경하여 새 클래스를 생성한다. **상속을 이용하면 새로운 클래스는 기존 클래스를 복사하지 않고, 기존 클래스의 모든 코드를 쓸 수 있다.**

필요한 것만 추가 / 변경하여 새 클래스를 정의한다. **그리고 이것은 기존 클래스의 행동을 오버라이드(재정의) 한다.** 기존 클래스는 부모 | **슈퍼** | 베이스 클래스라고 부르고, 새 클래스는 자식 | **서브** | 파생된 클래스라고 부른다. 

~~~python
class Car():
    pass

class Yugo(Car): # 슈퍼클래스로부터 상속
    pass
~~~

빈 클래스 Car를 정의했다. 그리고 Car의 서브클래스인 Yugo를 정의했다. 

~~~python
give_me_a_car = Car()
give_me_a_yugo = Yugo()
~~~

각 클래스로부터 객체를 생성했다. **give_me_a_yugo 객체는 Yugo 클래스의 인스턴스지만, 또한 Car 클래스가 할 수 있는 어떤 것을 상속받는다.** 

~~~python
class Car():
    def exclaim(self):
        print("I'm a Car!")

class Yugo(Car):
    pass

car = Car()
yugo = Yugo()
yugo.exclaim() # I'm a Car!
car.exclain() # I'm a Car!
~~~

Yugo 클래스는 아무것도 하지않고 슈퍼클래스로부터 상속 받았다. 때문에 exclaim 메소드를 사용할 수 있다.

## 6.4 메서드 오버라이드

새 클래스는 부모 클래스로부터 모든 것을 상속받는다. **부모 메소드를 대체 혹은 오버라이드할 수 있다.** 

~~~python
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
~~~

서브클래스에서 슈퍼클래스의 exclaim 메소드를 오버라이드(재정의) 했다. __init__ 메소드를 포함한 모든 것들을 재정의할 수 있다!

~~~python
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
~~~

__init__ 메소드도 재정의했다.

## 6.5 메서드 추가하기

서브클래스는 슈퍼클래스에 없는 메서드도 추가할 수 있다.

~~~python
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
~~~

need_a_push 메소드는 서브클래스의 객체에서만 사용할 수 있다. 

## 6.6 부모에게 도움 받기: super

서브 클래스에서 슈퍼 클래스의 메소드를 호출하는 방법이다. 

~~~python
class Person():
    def __init__(self, name):
        self.name = name

class EmailPerson(Person):
    def __init__(self, name, email):
        super().__init__(name)
        self.email = email
~~~

**서브 클래스에서 \_\_init\_\_을 정의하면 더 이상 슈퍼 클래스의 \_\_init\_\_은 호출되지 않는다.** 따라서 명시적으로 슈퍼 클래스의 \_\_init\_\_을 호출해주어야 한다.

* super() 메소드는 슈퍼 클래스(Person)의 정의를 얻는다
* __init__ 메소드는 Person.__init__() 메소드를 호출한다. 이 메소드는 self 인자를 슈퍼 클래스로 전달하는 역할을 한다. 그러므로 슈퍼 클래스에는 어떤 선택적 인자를 제공하기만 하면 된다. (지금의 경우 name을 제공한다)
* self.email = email은 새로운 코드이다

새로운 객체를 생성한다

~~~python
bob = EmailPerson('Bob Frapples', 'bob@naver.com')

bob.name # Bob Frapples
bob.email # bob@naver.com
~~~

왜 서브 클래스에서 다음과 같이 하지 않았을까?

~~~python
class EmailPerson(Person):
    def __init__(self, name, email):
        self.name = name
        self.email = email
~~~

**위의 코드로는 상속을 사용할 수 없다.** 슈퍼 클래스인 Person의 \_\_init\_\_이 변경되어도 서브 클래스에는 영향을 미치지 않기 때문에 불편하다. 즉, **슈퍼 클래스의 변경사항을 자동으로 반영하기 위해서 super() 메소드를 사용해서 상속받는다.**

## 6.7 자신: self

**파이썬은 적절한 객체의 속성과 메서드를 찾기 위해 self 인자를 사용한다.**

이전의 Car 클래스 예제를 보자

~~~python
car = Car()
car.exclaim() # I'm a Car!
~~~

다음과 같은 처리를 내부적으로 수행한다

* car 객체의 Car 클래스를 찾는다
* **car 객체를 Car 클래스의 exclaim 메소드의 self 매개변수에 전달한다.**

때문에 아래와 같이 해도 동작한다.

~~~python
Car.exclaim(car) # I'm a Car!
~~~

하지만 이렇게 사용할 이유는 없다!!