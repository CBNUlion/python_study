# 5�� ���� �����ϱ� : ���, ��Ű��, ���α׷�

������ Ÿ�� < �ڷᱸ�� < �Լ� < Ŭ���� < ��� < ��Ű�� < ���α׷�

## 5.1 ���ĵ��� ���α׷�

OS���κ��� �����Ͽ� ��ü������ ������ ������ ���α׷�

��ȭ�� ���������� ���� ��� .py ������ ����� �͹̳ο��� �����Ѵ�. 


## 5.2 Ŀ�ǵ� ���� ����

**sys.argv**

���α׷� ���� �� ���ڸ� list()�������� ��ȯ���ش�.

```python
import sys

if len(sys.argv) is 1:
  print("�ɼ��� ���� �ʰ� �� ��ũ��Ʈ�� �����ϼ̱���")


print("�ɼ� ����: %d" % (len(sys.argv) - 1))


print("\n< �ɼ� ��� >")

for i in range(len(sys.argv)):
  print("sys.argv[%d] = '%s'" % (i, sys.argv[i]))
```

> <����> ���̽� argparse (Ŀ�ǵ���� ���ڸ� �ٷ�� ���) : http://blog.naver.com/PostView.nhn?blogId=cjh226&logNo=220997049388&parentCategoryNo=&categoryNo=17&viewDate=&isShowPopularPosts=false&from=section 


## 5.3 ���� import��

���α׷��� ������� ����, ������ ���� ���� ���� ���Ϸ� ������.

���� ���α׷��� ��� ������ �Լ��� ���Ǹ� �������� �ʰ��� ����� �� �ִ�.

--> ���

import���� ���� ����� �ڵ带 �����Ѵ�.

### 5.3.1 ��� ����Ʈ�ϱ�

- �Լ� �ۿ��� import : ����Ʈ�� �ڵ尡 ���� ��ҿ��� ���Ǵ� ���
- �Լ� �ȿ��� import : ����Ʈ�� �ڵ��� ����� ���ο� ���ѵǴ� ���

### 5.3.2 �ٸ� �̸����� ��� ����Ʈ�ϱ�

as�� ����Ͽ� �ٸ� �̸����� ����Ʈ�� �� �ִ�.

**import [���] as [�ٸ� �̸�]**

### 5.3.3 �ʿ��� ��⸸ ����Ʈ�ϱ�

��� ��ü Ȥ�� ����� �ʿ��� �κи� ����Ʈ�� �� �ִ�.

**from [���] import [����� �Լ�]** 

**from [���] import [����� �Լ�] as [�ٸ� �̸�]**

### 5.3.4 ��� �˻� ���

����� ��� ���

```python
import sys

for place in sys.path:
	print(place)

```

�ߺ��� �̸��� ����� �ִٸ�, ù ��° ������ ����Ѵ�.

> <����> https://docs.python.org/ko/3/tutorial/modules.html

## 5.4 ��Ű��

��Ű���� ����� ���丮 �������� ����ȭ�� ���̴�.

> <����> https://offbyone.tistory.com/106


## 5.5 ���̽� ǥ�� ���̺귯��

> <����> ǥ�� ���̺귯�� : https://docs.python.org/ko/3/tutorial/stdlib.html

### 5.5.1 ������ Ű ó���ϱ� : setdefault(), defaultdict()

- setdefault() : get()�Լ��� ���� ����, Ű�� ������ ��� �׸��� �Ҵ��� �� �ִ�.

- defaultdict() : setdefault()�Լ��� ���� ����, �Լ��� ���ڸ� ������ Ű�� �Ҵ��Ѵ�.

### 5.5.2 �׸� ���� : Counter()

**from collections import Counter**

- most_common()�� �̿��� ��� ��Ҹ� ������������ ��ȯ�Ѵ�.
- '+' �� '-' �����ڸ� ����� �� �ִ�.
- '&' �� '|' �����ڸ� ����� �� �ִ�.

### 5.5.3 Ű �����ϱ� : OrderedDict()

**from collections import OrderedDict**

**OrderedDict([('key1':'value1'), ('key2':'value2')])**

### 5.5.4 ���� + ť == ��ũ

**from collections import deque**

      =========================
          |    |    |    |    |  **����**
      =========================

      =========================
          |    |    |    |       **ť**
      =========================

      =========================
          |    |    |    |    #  **��ũ**
      =========================

����� �� �ִ� �Լ�

 - append
 - appendleft
 - count
 - extend
 - extendleft
 - index
 - insert
 - maxlen
 - pop
 - popleft
 - remove

### 5.5.5 �ڵ� ���� ��ȸ�ϱ� : itertools

 - chain() : ��ȸ ������ ���ڸ� �ϳ��� ��ȯ�Ѵ�.
 - cycle() : ���ڸ� �������� ��ȯ�Ѵ�.
 - accumulate(,fun) : ������ ���� ���� ����Ѵ�.
 - repeat() : ��Ҹ� ���� ������ŭ �ݺ��Ѵ�.

> <����> itertools : https://hamait.tistory.com/803

### 5.5.6 ����ϰ� ����ϱ� : pprint()

 ���� ������ ȣȣ

 �������� ���� ��ҵ��� �����Ͽ� ����Ѵ�.

## 5.6 ���͸� ���� : �ٸ� ���̽� �ڵ� ��������

 PyPi, github, readthedocs���� ���¼ҽ��� ����غ���.

