# 흘러가는 데이터

## 8.1 파일 입출력

데이터를 지속하는 가장 간단한 방법으로는 파일이 있다. 보통 이것을 플랫 파일이라고 부르며, **단지 파일 이름으로 저장된 바이트 시퀀스이다.** 컴퓨터는 파일로부터 데이터를 읽어서 메모리에 올리고, 메모리에서 저장할 데이터를 파일로 쓴다. 

##### 파일을 읽고 쓰기 전에, 파일을 열어야 한다.

~~~python
# ex)
fileobj = open(filename, mode)
~~~

위 코드에 대한 설명이다.

* fileobj는 open()에 의해 반환되는 파일 객체이다.
* filename은 파일의 문자열 이름이다.
* mode는 파일 타입과 파일로 무엇을 할지 명시하는 문자열이다.

##### mode는 두 글자로 이루어져 있으며, 아래와 같은 옵션을 가진다.

1. mode의 첫 번째 글자
   * r: 파일 읽기
   * w: 파일 쓰기(파일이 존재하지 않으면 생성하고, 존재하면 덮어쓴다)
   * x: 파일 쓰기(파일이 존재하지 않을 경우에만 해당)
   * a: 파일 추가하기(파일이 존재하면 파일의 끝에서부터 쓴다)

2. mode의 두 번째 글자
   * t(또는 아무것도 명시하지 않음): 텍스트 타입
   * b: 이진 타입

파일을 열고 다 사용했으면, 닫아야 한다.

~~~python
fileobj.close()
~~~

### 8.1.1 텍스트 파일 쓰기: write()

~~~python
text = '''Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries.'''

f = open('lorem.txt', 'wt')
f.write(text) # 286 출력 => 파일에 쓴 바이트 수를 반환한다
f.close()
~~~

lorem.txt 라는 파일이 생길 것이다. 

write() 함수는 파일에 쓴 바이트 수를 반환한다. 그리고 print() 함수처럼 스페이스나 줄바꿈(\\n)을 추가하지 않는다. 함수 이름과는 다르게 print()는 출력 뿐만아니라 파일을 쓰는데에도 사용할 수 있다.

##### print() 함수의 인자
* sep => 구분자이며 기본값은 스페이스이다.
* end => 문자열의 끝이며 기본값은 \n(줄바꿈) 이다.

#### print()를 사용한 파일 io

~~~python
text = '''Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries.'''

f = open('lorem2.txt', 'w')
print(text, file=f, sep='', end='\n\n')
f.close()
~~~

write() 함수처럼 lorem2.txt 파일을 생성한다. 하지만 end 인자에 주어진 값대로 문장의 끝에는 두 개의 줄바꿈이 삽입된다.

#### 파일에 쓸 문자열이 크면 특정 단위(chunk-청크)로 나누어서 파일에 쓴다

~~~python
text = '''Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries.'''

f = open('lorem3.txt', 'w')
size = len(text)
offset = 0
chunk = 50
while True:
    if offset > size:
        break
    f.write(text[offset:offset+chunk])
    offset += chunk
f.close()
~~~

50글자씩 나누어서 write 한다.

만약 파일이 중요하다면 x 모드를 사용해서 파일을 덮어쓰지 않도록 하는 것이 좋다.

~~~python
f = open('lorem3.txt', 'x')
f.write('haha')
f.close()
# FileExistsError: [Errno 17] File exists: 'lorem3.txt' 예외 발생
~~~

### 8.1.2 텍스트 파일 읽기: read(), readline(), readlines()

**read() 함수** : 인자 없이 호출해서 한 번에 전체 파일을 읽는다. 아주 큰 파일을 read() 함수를 써서 읽으면 메모리가 소비될 수 있으므로 주의해야 한다.

~~~python
f = open('lorem3.txt', 'r')
text = f.read()
f.close()
print(text)
~~~

쓰기와 마찬가지로 한 번에 얼마만큼 읽을지 크기를 제한할 수 있다. 

~~~python
output = ''
f = open('lorem3.txt', 'r')
chunk = 70
while True:
    fragment = f.read(chunk)
    if not fragment:
        break
    output += fragment
f.close()
print(output)
len(output) # 286
~~~

파일을 다 읽어서 끝에 도달하면 read() 함수는 빈 문자열을 반환한다. 즉, fragment가 False가 되며 while 반복문을 나오게 된다. 

**readline() 함수** : 파일을 라인 단위로 읽을 수 있다. 

~~~python
output = ''
f = open('lorem3.txt', 'r')
while True:
    line = f.readline()
    if not line:
        break
    output += line
f.close()
~~~

이터레이터를 이용해서 readline()처럼 코드를 작성할 수 있다.

~~~python
output1 = ''
f = open('lorem3.txt', 'r')
for line in f:
    output1 += line
f.close()
~~~

f 객체는 이터레이터 객체이기 때문에 순회 가능하며, 한 번에 한 라인씩 반환한다. 따라서 앞서 했던 readline() 함수와 비슷한 효과를 낸다.

readlines() 함수 : 한 번에 모든 라인을 읽고, 한 라인으로 된 문자열의 리스트를 반환한다.

~~~python
f = open('lorem3.txt', 'r')
lines = f.readlines()
f.close()
print(type(lines)) # <class 'list'>
~~~

### 8.1.3 이진 파일 쓰기: write()

b 모드로 파일을 열게되면 이진 모드를 사용한다. 문자열 대신 바이트를 읽고 쓴다.

~~~python
bdata = bytes(range(0, 256))
f = open('bfile', 'wb')
f.write(bdata) # 256
f.close()
~~~

### 8.1.4 이진 파일 읽기: read()

rb 모드를 사용한다.

~~~python
f = open('bfile', 'rb')
bdata = f.read()
len(bdata) # 256
f.close()
~~~

### 8.1.5 자동으로 파일 닫기: with

open 함수를 통해 파일을 열었다면 close 함수를써서 닫아주어야 한다. 보통의 경우에서는 큰 문제를 일으키지는 않지만 만약의 상황에 대비해서 항상 닫아 주는 것이 좋다.

파이썬에는 파일을 여는 것과 같은 일을 수행하는 컨텍스트 매니저가 있다.

~~~python
with open('lorem3.txt', 'a') as f:
    f.write(output)
~~~

with 블록이 끝나게 되면 자동으로 파일을 닫아준다.

### 8.1.6 파일 위치 찾기: seek()

tell() 함수는 파일의 시작으로부터의 현재 오프셋을 바이트 단위로 반환한다. seek() 함수는 다른 바이트 오프셋으로 위치를 이동할 수 있다. 

~~~python
f = open('bfile', 'rb')
f.tell() # 0

f.seek(255) # 255로 이동
f.tell() # 255
~~~

## 8.2 구조화된 텍스트 파일

어떤 프로그램에서 데이터를 저장하거나 이를 다른 프로그램으로 보낼 때, 구조화된 데이터가 필요하다.

* 여러 구분자를 이용(, | 스페이스)
* 태그: XML, HTML
* 구두점: JSON
* 들여쓰기: YAML

### 8.2.1 CSV

구분자로 된 파일은 스프레드시트와 데이터베이스의 데이터 교환에 자주 사용된다.

* 쓰기 예제

~~~python
import csv

lists = [
    ['a', 'first'],
    ['b', 'second'],
    ['c', 'third'],
    ['d', 'fourth'],
    ['e', 'fifth'],
    ['f', 'sixth']
]

with open('test2.txt', 'w') as f:
    csvout = csv.writer(f)
	csvout.writerows(lists)
~~~

* 읽기 예제

~~~python
import csv

with open('test2.txt', 'r') as f:
    var = csv.reader(f)
    lists = [row for row in var]

# [['a', 'first'],
#  ['b', 'second'],
#  ['c', 'third'],
#  ['d', 'fourth'],
#  ['e', 'fifth'],
#  ['f', 'sixth']]
~~~

* 읽기 예제(dict)

~~~python
import csv

with open('test2.txt', 'r') as f:
    var = csv.DictReader(f, fieldnames = ['alphabet', 'number'])
    aaa = [row for row in var]

# [OrderedDict([('alphabet', 'a'), ('number', 'first')]),
#  OrderedDict([('alphabet', 'b'), ('number', 'second')]),
#  OrderedDict([('alphabet', 'c'), ('number', 'third')]),
#  OrderedDict([('alphabet', 'd'), ('number', 'fourth')]),
#  OrderedDict([('alphabet', 'e'), ('number', 'fifth')]),
#  OrderedDict([('alphabet', 'f'), ('number', 'sixth')])]
~~~

### 8.2.4 JSON

데이터를 교환하는 형식이다. 

> dumps : 데이터 => JSON 문자열로 인코딩
> loads : JSON 문자열 => 데이터로 디코딩

### 8.2.5 YAML

YAML도 키와 값을 가지고 있다. 하지만 날짜와 시간 같은 데이터 타입을 더 많이 처리한다. 파이썬 표준 라이브러리는 YAML 처리를 지원하지 않기 때문에 yaml 서드파티 패키지를 이용해야 한다. 

> dump : 데이터 => YAML 문자열로 인코딩
> load : YAML 문자열 => 데이터로 디코딩

### 8.2.9 직렬화하기: pickle

자료구조(객체)를 파일로 저장하는 것을 직렬화(serialization)이라고 한다. **JSON과 같은 형식은 파이썬에서 모든 데이터 타입을 직렬화하는 컨버터가 필요하다.** 파이썬은 바이너리 형식으로 된 객체를 저장하고 복원할 수 있는 pickle 모듈을 제공한다. 