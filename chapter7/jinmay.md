# 데이터 주무르기

* 문자열 : 텍스트 데이터에 사용되는 유니코드 문자의 시퀀스
* 바이트와 바이트배열 : 이진 데이터에 사용되는 8비트 정수의 시퀀스

## 7.1 텍스트 문자열

### 7.1.1 유니코드

**유니코드는 전 세계 언어의 문자를 정의하기 위한 국제 표준 코드이다.**

#### 파이썬 3 유니코드 문자열

**파이썬 3 문자열은 바이트 배열이 아닌 유니코드 문자열이다.** 파이썬 2 -> 3에서 가장 큰 변화이다. **파이썬 3는 일반적인 바이트 문자열과 유니코드 문자열을 구분한다.**

> **문자열 len 함수는 유니코드의 바이트가 아닌 문자수를 센다**

#### UTF-8 인코딩과 디코딩

* 문자열 -> 바이트 : 인코딩
* 바이트 -> 문자열 : 디코딩

#### 인코딩

문자열을 바이트로 인코딩한다. encode() 함수를 사용한다. 

~~~python
snowman = '\u2603'
len(snowman) # 1

ds = snowman.encode('utf-8')
ds # b'\xe2\x98\x83'

ds1 = snowman.encode('ascii') 
# UnicodeEncodeError: 'ascii' codec can't encode character '\u2603'
~~~

ds1의 경우 유니코드 문자열을 아스키코드로 디코딩을 시도했기 때문에 예외가 발생했다. **인코딩 예외를 피하기 위해 두 번째 인자를 받을 수 있으며 기본값은 'strict'이다.** 

~~~python
snowman = '\u2603'
ds1 = snowman.encode('ascii', 'ignore') # b''
~~~

'ignore' 인자로 알 수 없는 문자를 인코딩하지 않는다. 

#### 디코딩

**바이트 문자열을 유니코드 문자열로 디코딩한다.** 외부 소스에서 텍스트를 얻을때 바이트 문자열로 인코딩 되어있다. **가능한 UTF-8을 사용하는 것이 좋다!!!!!!!!!!**

### 7.1.2 포맷

데이터 값을 문자열에 끼워 넣는 방법(interpolate)이다. 옛 스타일과 새로운 스타일의 두 가지 방법이 존재한다. 

#### 옛 스타일: %

C언어와 같이 **string % data** 형식을 사용한다. 만약 data 부분이 2개 이상 이라면 튜플로 묶어 주어야 한다.

~~~python
# 들어갈 데이터가 두 개 이상인 경우
# 튜플로 묶어야 한다
print('%s and %s' % ('first', 'second'))
~~~

#### 새로운 스타일의 포매팅: {}와 format

파이썬 3을 사용한다면 새로운 스타일의 포매팅을 추천한다.

~~~python
# 기본
print('{} and {}'.format('first', 'second')) # first and second

# 순서를 정할 수 있다
print('{2} and {1} and {0}'.format('first', 'second', 'third')) # third and second and first

# 키워드 인자처럼 쓸 수 있다
print('{t} and {s} and {f}'.format(f='first', t='third', s='second')) # third and second and first
~~~

### 7.1.3 정규표현식

**원하는 문자열 패턴을 정의하여 소스 문자열과 일치하는 지 비교할 수 있다.** 

~~~python
import re
~~~

파이썬 표준 모듈 **re**에서 제공한다.

~~~python
result = re.match('You', 'Young fasfsad')
result # <re.Match object; span=(0, 3), match='You'>
~~~

match의 첫 번째 인자가 패턴이고, 두 번째는 문자열 소스이다. match()는 소스와 패턴의 일치 여부를 확인한다.

~~~python
pattern = re.compile('You')
~~~

패턴 확인을 빠르게 하기 위해 패턴을 먼저 컴파일 할 수 있다

~~~python
result = re.match(pattern, 'Young fasdfasd')
~~~

**패턴을 확인하는 메소드는 match이외에 search / findall / split / sub가 있다.**

~~~python
import re

source = 'Young fsdfas fadfasd'
m = re.match('You', source)
if m:
    print(m.group()) # You

m2 = re.match('fsd', source)
if m2:
    print(m2.group()) # 출력 x
~~~

**match 함수는 소스의 시작부터 패턴이 일치하는 지 확인한다.** 두 번째 경우는 아무것도 출력되지 않는데 이는 match 함수는 소스의 처음부터 비교하기 때문이다.

~~~python
source = 'Young fsdfas fadfasd fsd'
m3 = re.search('fsd', source)
if m3:
    print(m3.group()) # fsd
~~~

반면에 search 함수는 패턴이 아무데나 있어도 작동한다.

#### 첫 번째 일치하는 패턴 찾기: search()

#### 일치하는 모든 패턴 찾기: findall()

search() 함수는 단 하나의 패턴만 찾는다. 일치하는 모든 패턴을 찾기 위해서 findall() 함수를 써야 한다.

~~~python
m4 = re.findall('fas', source)
m4 # ['fas', 'fas']
~~~

