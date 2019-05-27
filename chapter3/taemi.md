# chapter3 파이 채우기 : 리스트, 튜플, 딕셔너리, 셋

## 3.1 리스트와 튜플

- 리스트
    - 변경가능
- 튜플
    - 불변

## 3.2 리스트

### 3.2.1 리스트 생성하기 : [] 또는 list()

- [' ',  ' ']
- list = list() : list 라는 빈 리스트 생성
- 4.6에서 리스트 컴프리핸션 (list comprehension) 설명
- 순서 상관없이 유일한 값으로 유지 : 리스트보다 셋(set)을 사용

### 3.2.2 다른 데이터 타입을 리스트로 변환하기 : list()

- list() 함수는 다른 데이터 타입을 리스트로 변환
- list('cat')
    - 한 단어를 한 문자 문자열의 리스트로 변환
- list('튜플 형태')
    - 튜플을 리스트로 변환
- .split('구분자')
    - 구분자로 나눠서 리스트로 변환
    - 구분자가 여러개 있을 경우
        - 구분자 사이에는 빈문자열이 들어감

### 3.2.3 [offset]으로 항목 얻기

- 문자열과 마찬가지로 리스트는 오프셋으로 하나의 특정값 추출 가능

### 3.2.4 리스트의 리스트

- 리스트는 리스트뿐만 아니라 다른 타입의 요소도 포함 가능
- 리스트 안에 또 리스트가 들어가 있으면 2개의 인덱스로 표현 간으
    - ex. all_birds[1][0]

### 3.2.5 [offset]으로 항목 바꾸기

- marxe[2] = 'taemi' ==> 세 번째 항목 taemi로 변환

### 3.2.6 슬라이스로 항목 추출하기

- 서브시퀀스 추출 가능
- 리스트의 슬라이스 또한 리스트
     - taemi = ['a', 'b', 'c']
     taemi[0:2]
     ==> ['a','b']
- 스텝 사용 가능
    - [::-2] ==> ['c','a']
    - 리스트 반전 : [::-1]

### 3.2.7 리스트의 끝에 항목 추가하기 : append()

- taemi.append('d')
taemi
==> ['a', 'b', 'c', 'd']

### 3.2.8 리스트 병합하기 : extend() 또는 +=

- 다른 리스트와 병합 가능
    - taemi 리스트에 others 리스트 병합
        - others = ['e', 'f']
        taemi.extent(others)
        taemi
        ==> ['a', 'b', 'c', 'd']
        - other = ['e', 'f']
        taemi += others
        taemi
        ==> ['a', 'b', 'c', 'd']
- **주의**
     - append(others)를 쓰게 되면 병합하지 않고, others가 하나의 **리스트**로 추가된다.

### 3.2.9 오프셋과 insert()로 항목 추가하기

- append()
    - 리스트 마지막에 항목 추가
- insert()
    - 리스트 원하는 위치에 항목 추가
    - insert(원하는 위치 오프셋, 넣고 싶은 항목)
    - 0이면 제일 첫단에, 더 높은 값이면 제일 마지막단에 추가 됨
    - 따라서 예외 없음

### 3.2.10 오프셋으로 항목 삭제하기 : del

- taemi = ['a','b','c','d']
 del taemi[-1] ==> ['a', 'b', 'c']

### 3.2.11 값으로 항목 삭제하기 remove()

- 리스트에서 삭제할 항목의 자리를 모르는 경우 유용하다
- taemi = ['a','b','c','d'] 에서 taemi.remove('c') ==> taemi == ['a','b','d']

### 3.2.12 오프셋으로 항목을 얻은 후 삭제하기 : pop()

- 리스트에서 항목을 가져오는 동시에 삭제
- 인자가 없다면 -1을 사용
- pop(0) : 리스트의 헤드(head, 머리, 시작)을 반환
- pop() 혹은 pop() : 리스트의 테일(tail, 꼬리, 끝)을 반환
- append() 후 pop() 사용 ==> LIFO (후입선출) , stack
- append() 후 pop(0) 사용 ==> FIFO (선입선출), queue
### 3.2.13 값으로 항목 오프셋 찾기 : index()

- taemi = ['a','b','c','d'] 
taemi.index('b') ==> 1

### 3.2.14 존재여부 확인하기 : in

- taemi = ['a','b','c','d'] 
'a' in taemi ==> True
'f' in taemi ==> False
- bool형태로 출력
- 같은 값이 여러개 있어도 해당 값이 적어도 하나라도 존재한다면 True를 반환한다

### 3.2.15 값 세기 : count()

- taemi = ['a', 'b', 'c', 'd', 'd']
taemi.count('a') ==> 1
taemi.count('d') ==> 2

### 3.2.16 문자열로 변환하기 : join()

- taemi = ['a', 'b', 'c', 'd', 'd']
','.join(taemi) ==> ' a, b, c, d, d'
- taemi.join(',')의 형태는 **사용할 수 없다!**
- **split()과 반대**
    - taemi = ['a','b','c']
    separator = '*'
    joined = separator.join(taemi)
    joined ==> 'a*b*c'
    separated = joined.stlit(separator)
    separated ==> ['a','b','c']
    separated == friends ==> True
    - 지정한 separator를 이용해서 join은 합치고, split은 나눈다.

### 3.2.17 정렬하기 : sort()

- 내부적, 복사본
    - sort() : 리스트 자체를 **내부적으로** 정렬
    - sorted() : 리스트의 정렬된 **복사본**을 반환
- 방식
    - 숫자 : 오름차순
    - 문자열 : 알파벳순
    - 정수와 부동소수점 혼합 : 파이썬이 자동으로 타입을 형변환해서 항목들을 정렬
    - 반대 정렬 : 인자에 reverse=True를 추가
        - ex.sort(reverse=True)

### 3.2.18 항목 개수 얻기 : len()

- 항목수를 반환
- taemi = ['a', 'b','c','d']
len(taemi) ==> 4

### 3.2.19 할당 : =, 복사 : copy()

- 할당
    - 한 리스트를 두 곳에 할당했을 경우, 한 리스트를 변경하면 **나머지 한 리스트도 변경된다.**
    - ex.
    a = [1,2,3]
    b = a
    a[0] = 10
    a ==> [10, 2, 3]
    b ==> [10, 2, 3]
- 복사
    - copy() 함수
    - list() 변환 함수
    - 슬라이스 [:]
    - ex> 
    원본 a = [1,2,3]
    b = a.copy()
    c = list(a)
    d = a[:]
    - b,c,d는 a의 **복사본**. 따라서 복사본을 바꾸더라도 원본에는 지장이 없음.

## 3.3 튜플

- 리스트와 다르게 **불변**
    - 추가, 삭제, 수정을 할 수 없음

### 3.3.1 튜플 생성하기 : ()

- taemi = ()
taemi ==> ()
- 하나 이상의 요소가 있는 튜플을 만들기 위해서는 각 요소 뒤에 콤마 (,)를 붙인다.
    - taemi = 'i am groot',
    taemi ==> ('i am goort',)
- 두 개 이상의 요소가 붙어 있을 경우, 마지막 요소에는 콤마를 붙이지 않는다.
    - taemi = 'i', 'am', 'groot'
    taemi ==> ('i','am','groot')
- 파이썬은 튜플을 출력할 때 괄호가 붙음
- 튜플을 정의할 때는 괄호가 필요 없다
    - 뒤에 콤마가 붙으면 튜플 정의
    - 괄호도 묶어도 되긴 됨
- **튜플은 한 번에 여러 변수를 할당할 수 있음**
    - taemi = ('i', 'am', 'groot')
    a,b,c = taemi
    a ==> 'i'
    b ==> 'am'
    c ==> 'groot'
    - **튜플 언패킹(tuple unpacking)** 이라고 부른다
    - 한 문장에서 값 교환을 위해 임시변수를 사용하지 않고 튜플을 사용
        - first = 'one'
        second = 'two'
        first, second = second, first
        first ==> 'two'
        second ==> 'one'
        - 한 번에 여러 변수를 할당할 수 있으므로 가능
- tuple() : 다른 객체를 튜플로 만듦
    - taemi = ['i','am', 'groot']
    tuple(taemi) ==> ('i','am', 'groot')

### 3.3.2 튜플과 리스트

- 튜플은 리스트에서 사용하는 다양한 함수를 사용할 수 없음
- 그럼 리스트를 써야지 왜 튜플을 쓸까?
    - 튜플은 더 적은 공간을 사용
    - 실수로 튜플의 항목이 손상될 염려가 없음
    - 튜플은 딕셔너리 키로 사용할 수 있음
    - **네임드 튜플(named tuple)**은 객체의 단순한 대안이 될 수 있음
    - 함수의 인자들은 튜플로 전달
    - 일반적으로 리스트와 딕셔너리를 더 많이 사용

## 3.4 딕셔너리

- 순서 없음
- 오프셋으로 항목 선택 불가
- 값(value)에 해당하는 키(key)를 지정
- 다른 언어에서는 딕셔너리를 *연관배열*, *해시*, *해시맵*이라고 부름
- 파이썬에서는 딕셔너리를 *딕트(dict)*라고도 부름

### 3.4.1 딕셔너리 생성하기 : {}

- 빈 딕셔너리 : taemi = {}
- taemi = {'first' : 'one',
'second' : 'two',
}

### 3.4.2 딕셔너리로 변환하기 : dict()

- 두 항목의 리스트로 구성된 리스트
    - 
    taemi = [['a','b'],['c','d'],['e','f']]
    dict(taemi) ==> {'a':'b','c':'d','e':'f' }
- 두 항목 튜플로 된 리스트
    - 
    taemi = [('a','b'),('c','d'),('e', 'f')]
    dict(taemi) ==> {'a':'b','c':'d','e':'f' }
- 두 항목 리스트로 된 튜플
    -
    taemi = (['a','b'],['c','d'],['e','f'])
    dict(taemi) ==> {'a':'b','c':'d','e':'f' }
- **두 문자 문자열로 된 리스트**
    - 
    taemi = ['ab','cd','ef']
    dict(taemi) ==> {'a':'b','c':'d','e':'f' }

- **두 문자 문자열로 된 튜플**
    - 
    taemi = ('ab','cd','ef')
    dict(taemi) ==> {'a':'b','c':'d','e':'f' }

### 3.4.3 항목 추가/ 변경하기 : [key]

- 키는 반드시 유일해야 한다.
- 항목 추가
pythons = {
    'Chapman':'Graham',
    'Cleese':'John',
}
pythons['Park'] = 'taemi
pythons ==> { 'Chapman':'Graham','Cleese':'John','Park': 'taemi'}
- 항목 변경
python['Park'] = 'Taemi'
pythons ==> { 'Chapman':'Graham','Cleese':'John','Park': 'Taemi'}
- 만약 같은 키가 2개 있다면 마지막 값이 남게 된다.
    - 키를 가지고 있는 마지막 값만 살아남고 나머지는 없어짐

### 3.3.4 딕셔너리 결합하기 : update()

- taemi1 = {'i':'ice', 'a':'ant'}
taemi2 = {'j':'join', 'l':'lion'}
taemi1.update(taemi2)
taemi1 ==> {'i':'ice', 'a':'ant','j':'join', 'l':'lion'}
- 만약 병합할 시 두 딕셔너리에 같은 키 값이 있다면
두번째 딕셔너리에 있는 값이 승리 ( 괄호 안의 딕셔너리 )

### 3.4.5 키와 del로 항목 삭제하기

- taemi1 = {'i':'ice', 'a':'ant','j':'join', 'l':'lion'}
del taemi1['i']
taemi1 ==> { 'a':'ant','j':'join', 'l':'lion'}

### 3.4.6 모든 항목 삭제하기 : clear()

- 딕셔너리 키와 값을 모두 삭제
- taemi1.clear()
taemi1 ==> {}

### 3.4.7 in으로 키 멤버십 테스트하기

- 딕셔너리에 키가 존재하는지 확인 : in
- taemi = {'i':'ice', 'a':'ant','j':'join', 'l':'lion'}
'i' in taemi ==> True
'd' in taemi ==> False

### 3.4.8 항목 얻기 : [key]

- taemi['i'] ==> 'ice'
- 키가 존재 하지 않으면 예외
    - 이 문제를 피하려면 in을 이용해서 있는지 확인
    - 이 문제를 피하려면 get() 함수 사용
        - 키가 존재 하지 않으면 옵션을 지정해서 그 값을 출력
        - taemi.get('q', 'not a taemi')
        - 옵션 지정이 없으면 None을 얻음 ( 대화식 인터프리터에 표기 x)
        
### 3.4.9 모든 키 얻기 : keys()

- taemi = {'i':'ice', 'a':'ant','j':'join', 'l':'lion'}
taemi.keys() ==> dict_keys(['i','a','j','l'])
- python2에서 keys() : 리스트 반환
- python3에서 keys() : 순회 가능한 키들을 보여주는 dict_keys()를 반환
    - 따라서 리스트 변환 가능 
    - list(taemi.keys())

### 3.4.10 모든 값 얻기 : values()

- taemi = {'i':'ice', 'a':'ant','j':'join', 'l':'lion'}
list(taemi.values())==> ['ice', 'ant','join', 'lion']

### 3.4.11 모든 쌍의 키-값 얻기 : items()

- list(taemi.items()) ==> [('i', 'ice'),('a','ant'),('j','join'),('l','lion')]
- 키와 값은 튜플 형태로 변환

### 3.4.12 할당 : =, 복사 : copy()

- 할당
    - 리스트와 마찬가지
    - 하나를 수정하면 나머지도 전부 수정된다.
- 복사 
    - taemi2 = taemi1.copy()
    - taemi1을 수정해도 taemi2에겐 영향이 없다

## 3.5 셋(set)

- 값은 버리고 키만 남은 딕셔너리와 같다
- 어떤 것이 존재하는지 여부만 판단하기 위해서는 셋을 사용한다
- 키에 정보를 넣고 싶다면 딕셔너리를 이용
- 유니온(union, 합집합)과 인터섹션(intersection, 교집합)을 참고

### 3.5.1 셋 생성하기 : set()

- taemi = set()
taemi ==> set()
- taemi = {1,2,3,4,5}
taemi ==> {1,2,3,4,5}
- 순서 없음

### 3.5.2 데이터 타입 변환하기 : set()

- 리스트, 문자열, 튜플, 딕셔너리로부터 중복된 값을 버린 셋 생성 가능
    - set('letters') ==> {'l', 'e','t','r','s'}
    - set(리스트)
    - set(튜플)
    - set(딕셔너리)
        - 키만 사용

### 3.5.3 in으로 값 멤버십 테스트하기

- 일반적으로 사용되는 셋의 용도
- 들어 있는 멤버들 중의 특정한 값이 있는 키를 골라준다.

### 3.5.4 콤비네이션 연산자

- 셋 인터세션 연산자(set intersection operator, 셋 교집합 연산자) : &
    - a.intersection(b) : a와 b가 가지고 있는 값 중 중복값 출력 (튜플)
- | 연산자와 union() 함수
    - a | b 또는 a.union(b) : a와 b의 인자들 중복 값을 제외하고 출력
- difference()
    - a - b 또는 a.diffentce(b) : a에서 b와 다른 값만 출력
- 익스클루시브(exclusive)
    - ^ 또는 symmetric_difference() : 서로 다른 값을 출력
- 서브셋(subset)
    -  <= 또는 a.issubset(b): a가 b에 종속되어 있는가? a는 b의 부분집합인가?
    - 모든 셋은 자신의 서브셋
- 프로퍼 서브셋(proper subset, 진 부분집합)
    - a < b : b 는 a를 전부 포함하고 그 이상의 멤버가 있어야 한다
- 슈퍼셋 ( super set )
    - ' >= 나 issuperset() : b가 a에 종속되어 있는가?
    - 모든 셋은 자신의 슈퍼셋
- 프로퍼 슈퍼셋 (proper superset)
    - ' > 연산자
    - 모든 셋은 자신의 프로퍼 슈퍼셋이 될 수 없다

## 3.6 자료구조 비교하기

- 리스트
    - []
- 튜플
    - 콤마(,)
- 딕셔너리
    - {}
- 공통
    - 대괄호([])를 이용해서 접근 가능
        - 리스트, 튜플 : [오프셋]
        - 딕셔너리 : [키]

## 3.7 자료구조를 더 크게

여러 자료구조는 서로 포함시킬 수 있으며, 사용할 때에는
변할 수 있는 것과 불변하는 것을 유의해야한다.




# 주의할 점 ( 헷갈리는 것 )
- [offset]
    - 문자열 : 불변
    - 리스트 : 변함
- del 은 리스트 함수가 아니라 파이썬 구문이다. 즉 taemi.del()을 수행할 수 없다
    - del taemi[] 이런 식으로 작성해야 한다.
- 각각의 함수 혹은 구문들이 어떻게 사용되는지 정리
     - 예를들면 len()는 len(taemi)로 사용하고 sort는 taemi.sort()로 사용하는 것
- 3.2.19 복사에서 a를 b에 복사 했을 때 a를 변경하면 b도 변경되는 것.

# Q
-  3.4.9 에서
python2에서 keys() : 리스트 반환
python3에서 keys() : 순회 가능한 키들을 보여주는 dict_keys()를 반환
라고 하는데 dict_keys()를 반환하는 것이 형태로 반환핳는 건지, 무엇인지 모르겠다.
- 3.5.3 이 왜 set에 작은 분류로 들어갔는지?
