# 6장 객체와 클래스

## 6.1 객체란 무엇인가?

객체 = 데이터(변수, 속성 ) + 코드(함수, 메서드)

객체 : 명사  /  각각의 사물
메서드 : 동사 / 사물간 상호작용


## 6.2 클래스 선언하기 : class

클래스 = 박스를 만드는 툴

파이썬에는 표준 데이터 타입을 생성하는 많은 내장 클래스가 있다.

```python
class Person():
	def __init__(self, name): # self는 Person이며, 클래스 한정 전역변수
		self.name = name

hunter = Person('sehwa')
# Person('sehwa') 또한 하나의 객체

```

** Person('sehwa')이 객체이면, 메모리 낭비가 있지 않을까? **

** --> 일시적으로 메모리를 차지하지만, hunter에 값 반환 후 사라진다. ** 


## 6.3 상속

####상속

- 기존 클래스에서 일부를 추가하거나 변경하여 새로운 클래스를 생성
- 코드를 재사용하는 아주 좋은 방법
- 기존 클래스를 복사하지 않고, 기존 클래스의 모든 것을 사용할 수 있음


## 6.4 매서드 오버라이드

####오버라이드

- 부모 클래스를 상속 받은 후
- 부모 클래스의 메서드를 대체 혹은 오버라이드 할 수 있다


## 6.5 매서드 추가하기

- 자식 클래스는 부모 클래스에 없는 메서드를 추가할 수 있다.

```python
class Car():
    def exclaim(self):
        print("I'm a Car!")

class Yugo(Car):
    def exclaim(self):
        print("I'm a Yugo!")

    def needapush(self):
        print("A little help here?")

givemeacar = Car()
givemeayugo = Yugo()

```
Yugo는 needapush 매서드를 불러올 수 있지만, Car은 그러지 못한다.



## 6.6 부모에게 도움 받기 : super

자식 클래스에서 부모 클래스의 메서드를 호출할 수 있다.

** super을 사용하는 이유? **
- 상속을 사용하기 위해
- 부모 클래스의 정의가 바뀌면, 자식 클래스에게 변경사항이 반영된다.

## 6.7 자신 : self

자기 자신의 속성과 매서드를 호출하기 위함!

## 6.8 get/set 속성값과 프로퍼티

- 객체지향언어에서 private 값에 접근하기 위해 getter와 setter 메서드를 사용한다.
- python의 모든 속성과 메서드는 public이기에 getter와 setter이 필요없다.
- 하지만 속성에 직접 접근하는 것이 부담스럽다면, getter와 setter 메서드를 작성할 수 있다.
- 프로퍼티를 이용하면, 속성의 정의를 바꿀 때 모든 호출자를 수정할 필요 없이 클래스 정의에 있는 코드만 수정하면 된다.

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
```

1.
```python
    name = property(get_name, set_name)
    # 두 메서드를 name이라는 속성의 프로퍼티로 정의
```

- property()의 첫 번째 인자는 getter()메서드, 두 번째 인자는 setter()메서드이다.
- 클래스의 name을 호출하면 get_name()메서드가 실행, name에 값을 할당하면 set_name()메서드가 실행된다.
- name을 호출하지 않고도, get_name()메서드와 set_name()메서드를 직접 호출할 수 있다.

2.
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

- 데커레이터를 이용하여 프로퍼티를 정의할 수 있다.
- getter메서드 앞에 @property 데커레이터를 쓴다.
- setter메서드 앞에 @name.setter 데커레이터를 쓴다.
- 1번 방법과 동일하게 name속성 호출을 통해 getter, setter을 호출할 수 있다.
- 1번 방법과 다르게 getter, setter메서드를 직접 호출할 수 없다.


## 6.9 private 네임 맹글링

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
```

- 네이밍컨벤션 던더(__)를 사용하면 클래스 정의 외부에서 볼 수 없다.
- 네이밍컨벤션은 속성을 private으로 만들지 않지만, 외부 코드에서 발견할 수 없도록 이름을 맹글링한다.
- 속성을 완벽하게 보호할 수는 없지만, 속성의 의도적인 직접 접근을 어렵게 만든다.

## 6.10 메서드 타입

어떤 데이터(속성)와 함수(메서드)는 클래스 자신의 일부고, 어떤 것은 클래스로부터 생성된 객체의 일부다.

1. 인스턴스 메서드

- 일반적인 클래스를 생성할 때의 메서드 타입
- 인스턴스 메서드의 첫 번째 매개변수는 self
- 이 메서드를 호출할 때 객체를 전달

2. 클래스 메서드

- 클래스 전체에 영향
- 함수에 @classmethod 데커레이터
- 클래스 메서드의 첫 번째 매개변수는 클래스 자신(cls)

3. 정적 메서드

- 클래스나 객체에 영향을 미치지 못함
- 편의를 위해 존재
- @staticmethod 데커레이터
- 첫 번째 매개변수로 self나 cls가 없음
- 메서드 접근을 위해 객체를 생성할 필요가 없음


## 6.11 덕 타이핑

- 클래스에 상관없이 같은 동작을 다른 객체에 적용할 수 있다.

```python
def who_says(obj):
    print(obj.who(), 'says', obj.says())
```
who()와 says()메서드를 가진 모든 객체에서 이 메서드를 실행할 수 있다.

## 6.12 특수 메서드

<참고> 파이썬 매직메소드 : http://schoolofweb.net/blog/posts/%ED%8C%8C%EC%9D%B4%EC%8D%AC-oop-part-6-%EB%A7%A4%EC%A7%81-%EB%A9%94%EC%86%8C%EB%93%9C-magic-method/

## 6.13 컴포지션

- 다른 클래스의 일부 기능을 그대로 사용하고 싶으나, 전체 기능 상속은 피하고 싶을 때 사용한다.

- 상속 : 확장의 개념 : is-a 관계
- 컴포지션 : 사용의 개념 : has-ar관계 / 객체가 또 다른 객체를 구성

<참고> 컴포지션 : https://msryu.tistory.com/entry/%ED%95%AD%EB%AA%A9-16-%EC%83%81%EC%86%8D%EB%B3%B4%EB%8B%A4%EB%8A%94-%EC%BB%B4%ED%8F%AC%EC%A7%80%EC%85%98%EC%9D%84-%EC%82%AC%EC%9A%A9%ED%95%98%EC%9E%90

<참고> 컴포지션 심화 : https://www.fun-coding.org/PL&OOP1-11.html

## 6.14 클래스와 객체, 그리고 모듈은 언제 사용할까?

- 비슷한 행동(메서드)을 하지만 내부 상태(속성)가 다른 개별 인스턴스가 필요할때 객체를 사용한다.
- 클래스는 상속을 지원하지만, 모듈은 상속을 지원하지 않는다.
- 어떤 한 가지 일만 수행한다면 모듈이 가장 좋은 선택이다. 프로그램에서 파이썬 모듈이 참조된 횟수에 상관없이 단 하나의 복사본만 불러온다.
- 여러 함수에 인자로 전달될 수 있는 여러 값을 포함한 여러 변수가 있다면, 클래스를 정의하는 것이 좋다.
- 가장 간단한 문제 해결 방법을 사용한다. 딕셔너리, 리스트, 튜플은 모듈보다 더 작고, 간단하며, 빠르다. 그리고 일반적으로 모듈은 클래스보다 더 간단하다.

### 6.14.1 네임드 튜플

네임드 튜플 = 튜플의 서브클래스

- 이름(.name)과 위치([offset])로 값에 접근 할 수 있다.
- 불변하는 객체처럼 행동한다.
- 객체보다 공간 효율성과 시간 효율성이 더 좋다.
- 딕셔너리 형식의 괄호([]) 대신 점(.) 표기법으로 속성에 접근할 수 있다.
- 네임드 튜플을 딕셔너리의 키처럼 쓸 수 있다.