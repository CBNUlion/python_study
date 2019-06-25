#chapter 8 흘러가는 데이터

## 8.1 파일 입출력

> 파일 입출력을 하려면 파일을 1. 열고, 2. 작업 후 3. 닫아야 함
- 파일 열기
```python
fileobj = open(filename, mode)
```
여기서<br>
- fileobj : open()에 의해 반환되는 파일 객체
- filename : 파일 이름
- mode : 파일로 무엇을 할지
- mode의 첫 글자
    - r : 읽기
    - w : 쓰기 
        - 파일 존재 o : 덮어쓰기
        - 파일 존재 x : 파일 새로 생성
    - x : 쓰기
        - 파일이 존재하지 않을 때만
    - a : 추가하기 
        - 파일이 존재하면 파일의 끝에서부터 쓴다
- mode의 두번 째 글자
    - t (또는 아무것도 명시하지 않음): 텍스트타입
    - b : 이진 타입
### 8.1.1 텍스트 파일 쓰기 : write()

```python
>>>taemi = '''my name is taemi
    yes'''

>>> fout = open('relativity', 'wt') #파일을 쓰기용, 텍스트타입으로 열거임
>>> fout.write(taemi)       # write는 파일에 쓴 바이트 수 반환
#20
>>> fout.close()        #파일을 닫아주는 함수
```
- write : 파일에 쓴 바이트 수 반환
    - 스페이스나 줄바꿈은 추가하지 않음
<br>
- print사용해서 파일 입력
```python
>>> fout = open('relativity','wt')
>>> print(taemi, file=fout)
>>> fout.close()
```
<br>
> write? print? 무엇을 사용해야 하나?
 - print() : 각 인자 뒤에 스페이스를, 끝에 줄바꿈을 추가함
 > print() 를 write() 처럼 쓰려면?
 - 두 인자를 전달
    1. sep(구분자, 기본값은 스페이스(' ')이다.)
    2. end(문자열 끝, 기본값을 줄바꿈('/n')이다.)
> 특정 단위로 나누어서 파일에 작성하기
```python
>>> fout = open('relativity','wt')
>>> size = len(taemi) 
>>> offset = 0
>>> chunk = 100
>>> while True:
        if offset > size:
            break
        fout.write(taemi[offset:offset+chunk])
        offset += chunk
```
- 중요한 파일은 x모드로 열어서 파일을 덮어쓰지 않게 하는데, 이때 파일 에러가 났을 때 이미 파일이 있다고 표시 해주는 예외처리가 필요하다.
```python
>>> try:
        fout = open('relativity','xt')
        fout.write('stop')
    except FileExistsErrorL
        print('이미 파일이 있음')

# 이미 파일이 있음
```
### 8.1.2 텍스트 파일 읽기 : read(), readline(), readlines()
- read()
    - 한번에 파일 전체를 읽어 온다.
    - 용량이 큰 파일일 경우 주의
    - read(' 한 번에 읽을 수 있는 제한량')
    - 다 읽어서 끝에 도달하면 빈 문자열 반환 (' ')
- readline()
    - 라인 단위로 읽을 수 있다.
    - iterator를 사용할 수 있음
```python
>>> poem = ' '
>>> fin =open('relativity', 'rt')
>>> for line in fin:
        poem += line

>>> fin.close()
>>> len(poem)
#150
```
- readlines()
    - 한 번에 모든 라인을 읽고, 한 라인으로 된 문자열들의 리스트를 반환

### 8.1.3 이진 파일 쓰기 :write()
- b : mode에 추가하면 이진파일모드

### 8.1.4 이진 파일 읽기 : read()
```python
fin = open('bfile', 'rb') # rb 모드로 열어주면 됨
```
### 8.1.5 자동으로 파일 닫기 : with
```python
>>> with open('relativity', 'wt') as fout :
        fout.write(poem)
```
함수 안에 파일을 열어놓고 함수가 끝나면 파일도 닫힌다.

### 8.1.6 파일 위치 찾기 : seek()
- tell() : 파일의 시작으로부터 현재 오프셋을 바이트 단위로 반환
- seek() : 다른 바이트 오프셋으로 위치를 이동
    - 함수의 처음부터 읽지 않아도 바로 마지막 바이트를 읽을 수 있다.
```python
# seek 함수의 형식
seek(offset, origin)
```
1. origin = 0 : 기본값, 시작 위치에서 offset 바이트 이동
2. origin = 1 : 현재 위치에서 offset 바이트 이동
3. origin = 2 : 마지막 위치에서 offset바이트 전 위치로 이동

- 텍스트 파일에도 사용할 수 있으나, 1바이트를 쓰지 않는 이상 offset을 예측하기 힘들다.

## 8.2 구조화된 텍스트 파일

- CSV
    - 탭('\t'), 콤마(','), 수직바('|')와 같은 문자를 **구분자** 혹은 **분리자**로 사용.
- XML, HTML
    - 태그 <>
- JSON 
    - 구두점
- YAML
    - 들여쓰기

### 8.2.1 CSV
- 구분된 파일은 스프레드시트와 데이터베이스의 데이터 교환 형식으로 자주 사용
### 8.2.2 XML
- 잘 알려진 마크업 형식
- 데이터를 구분하기 위해 태그를 이용
- 태그 안에 태그를 자식이라고 함
- 데이터 피드와 메세지 전송에 많이 쓰임
- RSS와 아톰 같은 하위 형식이 있다.

### 8.2.3 HTML
### 8.2.4 JSON
- 자바 스크립트의 서브셋이자 파이썬의 유효한 구문
- 하나의 메인 모듈 : json
- 데이터와 JSON문자열 사이에 인코딩과 디코딩이 가능하다

### 8.2.5 YAML
- JSON과 유사하게 키와 값을 가지고 있음
- 날짜와 시간 같은 데이터 타입을 더 많이 처리
- 표준 파이썬 라이브러리는 아직 YAML 처리를 지원하지 않아서 yaml이라는 써드파티 라이브러리를 설치한다.
- load() : YAML 문자열을 파이썬 데이터로
- dump() : 파이썬 데이터를 YAML문자열로

### 8.2.6 보안노트

### 8.2.7 설정파일
### 8.2.8 기타 데이터 교환 형식
이진 데이터 교환 방식 
- MsgPack
- Protocol Buffers
- Avro
- Thrift

### 8.2.9 직렬화 하기 : pickle
- **직렬화** : 자료구조를 파일로 저장하는 것


 # Q
 
 - wirte() print()랑 차이가 이해가 잘.. 둘 다 똑같이 적히긴 적히는데
 - 233 마지막 예제도 뭘 나타내려는 건지 잘 모르겠다.
- 240p에 origin이 0인데 왜 마지막에서 간다고 하는지

