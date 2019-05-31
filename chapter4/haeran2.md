# ch.4 코드 구조

제너레이터부터 이어서

# generator

---

 모든 제너레이터는 반복자이다

- 반복자(iterator)와 같은 루프의 작용을 컨트롤 하기 위해 쓰여지는 특별한 함수 또는 루틴
- 모든 generator는 iterator (역 성립x)
- 호출을 할 수 있는 파라미터를 가지고 있고, 연속적인 값들을 만들어 낸다
- 한번에 모든 값을 포함한 배열을 만들어 리턴하는 대신 yield 구문을 이용해 한 번 호출 될 때마다 하나의 값만을 리턴
- 일반 iterator보다 아주 작은 메모리 필요로 한다

    #일반 함수
    def call_numbers(nums):
        result = []
        for i in nums:
            result.append(i)
        return result
    
    call_numbers([1,2,3,4,5,6,7,8,9,10]) 
    
    #output :[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

    #generator
    def call_numbers(nums):
        for i in nums:
            yield i
        print('모든 element들을 호출했슴니다')
    call_numbers([1,2,3,4,5,6,7,8,9,10])
    
    #output: <generator object call_numbers at 0x0000024080A492B0>

- generator를 만들고 호출해봤더니 genrator 객체자체가 나왔다. 원래 의도대로 리스트에 담긴 함수들을 출력하려면?

        #generator
        def call_numbers(nums):
            for i in nums:
                yield i
            print('모든 element들을 호출했슴니다')
            
        generator=call_numbers([1,2,3,4,5,6,7,8,9,10])
        
        for i in range(11):
            print(next(generator))
        
        #output :
        1
        2
        3
        4
        5
        6
        7
        8
        9
        10
        모든 element들을 호출했슴니다
        ---------------------------------------------------------------------------
        StopIteration                             Traceback (most recent call last)
        <ipython-input-13-7b638fc729f4> in <module>
              8 
              9 for i in range(11):
        ---> 10     print(next(generator))
        
        StopIteration:

    generator 객체를 변수에 저장하고 next메서드로 10번 진행한다.

    - 띠용? 그치만 11번 진행 후 print문까지 잘 출력 됐지만 stopIteration exeption이 났다.10번 진행하면 print문이 안나온다! 저 프린트문까지 출력되고 exeptionn이 나지 않으려면 어케 해야할까?

            #generator
            def call_numbers(nums):
                for i in nums:
                    yield i
                    print('i를 넘겨줬습니다')
                print('모든 element들을 호출했습니다')
                
                
            generator=call_numbers([1,2,3,4,5,6,7,8,9,10])
            
            for i in generator:
                print(i)
            
            #output
            1
            i를 넘겨줬습니다
            2
            i를 넘겨줬습니다
            3
            i를 넘겨줬습니다
            4
            i를 넘겨줬습니다
            5
            i를 넘겨줬습니다
            6
            i를 넘겨줬습니다
            7
            i를 넘겨줬습니다
            8
            i를 넘겨줬습니다
            9
            i를 넘겨줬습니다
            10
            i를 넘겨줬습니다
            모든 element들을 호출했습니다

        위에는 for in range(10)를 for in generator로 접근하자! 그리고 출력은 i로

        여기서 헷갈리지 말아야 할건, 첫번째 출력때 "i를 넘겨줬습니다"는 출력되지 않음. yeild()에 걸리면 다음 호출이 걸릴 때 까지 freezing상태이다. 

- 오키 이제 알았고 컴프리헨션에 적용해보자

        #컴프리헨션 적용 진짜 안보고 해본다 -> 실패
        generator = (x for x in [1,2,3,4,5,6,7,8,9,10])
            
        
        for i in generator:
            print(i)
        print('모든 element 호출을 마쳤습니다')
        
        #output
        1
        2
        3
        4
        5
        6
        7
        8
        9
        10

    넘나 간단하게 []→ ()로 바꾸면 [1,2,3,4,5,6,..,10] 원소들을 맹그는 제너레이터가 생기고

    같은 방식으로 출력하면 된다 ~~ 쏘 씸플!

- for문을 쓰지 않고 제너레이터 데이터를 한번에 보고 싶다면??

    제너레이터를 리스트로 맹글자! 

        generator = (x for x in [1,2,3,4,5,6,7,8,9,10])
            
        list1 = list(generator)
        print(list1)
        print('모든 element 호출을 마쳤습니다')
        
        #output
        [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
        모든 element 호출을 마쳤습니다

    컴프리헨션이 되는건 다 바꿀 수 있나?

        generator = (x for x in [1,2,3,4,5,6,7,8,9,10])
            
        set1 = set(generator)
        print(set1)
        print('모든 element 호출을 마쳤습니다')
        
        ----------------------------------------------------------------------
        generator = ((x,'a') for x in [1,2,3,4,5,6,7,8,9,10] )
            
        dict1 = dict(generator)
        print(dict1)
        print('모든 element 호출을 마쳤습니다')

    응 너무 잘돼~~

참고자료:[http://schoolofweb.net/blog/posts/파이썬-제너레이터-generator/](http://schoolofweb.net/blog/posts/%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EC%A0%9C%EB%84%88%EB%A0%88%EC%9D%B4%ED%84%B0-generator/)

# 함수

---

- 인자: 함수로 전달한 값
- 인자와 함수를 호출하면 인자의 값은 함수 내에서 해당하는 매개변수에 복사된다.
- return 값이 따로 없으면 None 반환 → 다른 언어의 null과 같은 맥락

    def fn1(a): # a: 매개변수
    	pass
    
    fn1(b) # b: 인자

### 위치 인자

값을 순서대로 상응하는 매개변수에 복사함

    def fn1(a,b,c):
        print('a={},b={},c={}'.format(a,b,c))
    fn1('aa','bb','cc')
    
    #output 
    a=aa,b=bb,c=cc

뭐 맨날 쓰던거다. 함수 정의 할 때 매개변수를 (a,b,c) 순서로 한거니까 넣은 순서대로 들어간거

→ 그치만 이렇게 하면 a,b,c 순서를 알아야함! →근데 요즘은 다 나오던디

### 키워드 인자

위치인자는 매개변수 순서를 알아야 하니까 귀찮 → 호출할때 fn(a='aa',b='bb','c'=cc) 이렇게 쓰면 된다 ~~ 물론 위치인자랑 섞어 쓸 수 있움

***위치 인자와 키워드 인자로 함수를 호출한다면 위치 인자가 먼저 와야 한다***

    def fn1(a,b,c):
        print('a={},b={},c={}'.format(a,b,c))
        
    fn1('bb',c='aa',b='cc')
    
    #output
    a=bb,b=cc,c=aa

위치인자가 먼저 와야 한다 < = > 위치인자 자리는 매개변수자리와 똑같이 들어감

→ 저기 코드에서 fn('bb', a = ' aa', c ='cc') 

→ 내 생각: aa,bb,cc 순서로 들어가겠지

→**실제: a='bb'들어가고 'aa'가 또 들어가니까 오류뜸,,,**

이걸 과연 진짜 쓸까?.. → 키워드 인자가 매번 매개변수 순서를 알아야 하는게 귀찮아서 쓴건데 혼용해서 쓰면 이걸 쓰는 이유가 있능교 

### 기본 매개변수값 지정하기

매개변수에 기본값을 지정하자!

호출자가 대응하는 인자를 제공하지 않으면 기본값을 사용하게!

    def fn1(a,b,c=[1,2,3,4]):
        print('a={},b={},c={}'.format(a,b,c))
        
    fn1('aa','bb')
    
    #output
    a=aa,b=bb,c=[1, 2, 3, 4]

### 위치 인자 모으기 : *

매개변수에 *(애스터리스크)를 사용하면 매개변수에서 위치 인자 변수들을 튜플을 묶는다.

    def fn1(*args):
        for e in args:
            print(e)
        
    print(fn1())
    
    #output
    None

    def fn1(*args):
        for e in args:
            print(e)
        
    fn1(1,2,3,4,5,6) #당연할 수도 있지만 1,2,..6 저거 ()로 안감싸도 된다! 새삼 신기하네
    
    #output
    1
    2
    3
    4
    5
    6 

- *args → arg로 바꾸면?

        def fn1(arg):
            for e in arg:
                print(e)
            
        fn1(1,2,3,4,5,6)
        
        #output
        ---------------------------------------------------------------------------
        TypeError                                 Traceback (most recent call last)
        <ipython-input-32-6bd141a8d3a5> in <module>
              3         print(e)
              4 
        ----> 5 fn1(1,2,3,4,5,6)
        
        TypeError: fn1() takes 1 positional argument but 6 were given

    fn1()함수는 매개변수가 1갠데 왜 6개씩이나 한바가지 넣어? 라는 오류가 뜬다

    - 이 상태에서 list나 dict를 넣으면?

            def fn1(arg):
                for e in arg:
                    print(e)
                
            fn1([1,2,3,4,5,6])
            
            #output
            1
            2
            3
            4
            5
            6

            dict1 = {1:'a',2:'b'}
            
            dict1.items()
            
            #output
            dict_items([(1, 'a'), (2, 'b')])

        이것도 어떻게 보면 당연 → 싸서 하나로 주니까

물론 fn1(a,b,*args) 이렇게 혼용해도 된다~~~

### 키워트 인자 모으기 : **

아까는 위치인자 묶었으니까 이번엔 키워드 인자를 묶어보자!

- 키워드 인자를 딕셔너리로 묶는다
- 인자의 이름은 키고 값은 이 키에 대응하는 딕셔너리 값이다
- 사실 이것도 잘 사용 안할거 같지만 함 해보자! → 엥 아니다 django에서 많이 쓰는거 봤다

    def fn(**kwargs):
        print(kwargs)
        print(a)
    
    fn(a='1',b='2')
    
    #output
    {'a': '1', 'b': '2'}
    ---------------------------------------------------------------------------
    NameError                                 Traceback (most recent call last)
    <ipython-input-67-045178aa3bfc> in <module>
          3     print(a)
          4 
    ----> 5 fn(a='1',b='2')
    
    <ipython-input-67-045178aa3bfc> in fn(**kwargs)
          1 def fn(**kwargs):
          2     print(kwargs)
    ----> 3     print(a)
          4 
          5 fn(a='1',b='2')
    
    NameError: name 'a' is not defined

내 생각: 키워드 인자로 a,b라는 변수 이름으로 넣어줬으니 당연히 fn함수 내에서도 a,b 개별적으로 접근 가능하다

실제: name 'a' is not defined

- 그러면 'a','b'를 개별적으로 접근하려면 어떻게 해야할까?

        def fn(**kwargs):
            for i,e in kwargs.items():
                if e=='1':
                    print('앗 value가 1이다!')
        
        fn(a='1',b='2')
        
        #output
        앗 value가 1이다

***우왕 근데 dict_item은 i,e로 for문 접근할 수 있구나***

→ dic_items() → dict_items([(1, 'a'), (2, 'b')]) 이렇게 key-value가 튜플로 묶이니까 가능하다!

- for문을 안쓴다면? → if '1' in kwargs.keys() 로 가능할까?

        def fn(**kwargs):
        #     for i,e in kwargs.items():
        #         if e=='1':
        #             print('앗 value가 1이다!')
            if '1' in kwargs.keys():
                 print('앗 value가 1이다!')
            else:
                print('없다')
        
        fn(a='1',b='2')
        
        #output
        없다!

안된다. ㅎ.ㅎ 이건 너무 될거같은데.. 왜 안되는 걸까? 물어보자

### docstring

- 함수 몸체 시작 부분에 문자열을 포함시켜 함수 정의에 문서를 붙일 수 있다.
- 길게 작성할 수 있으며 서식을 추가할 수도 있다
- docstring을 출력하려면 help()함수를 호출한다. 함수 인자의 리스트와 서식화된 docstring을 읽기 위해 함수 이름을 인자로 전달한다

나중에 멋있는 사람이 되면 함 해보자

    def fn1(a,b,*args):
        '''
        안녕 이건 fn1 함수이고 args로 받은걸 출력하는 함수야
            1.서식이
            그냥
            이런걸
            말하는 걸까..?
        '''
        print(args)
        
    help(fn1) #서식이 없는걸 출력하고 싶다면 ech.__doc__ 을 하자
    
    #output
    Help on function fn1 in module __main__:
    
    fn1(a, b, *args)
        안녕 이건 fn1 함수이고 args로 받은걸 출력하는 함수야
            1.서식이
            그냥
            이런걸
            말하는 걸까..?

### decorator

- 소스코드를 바꾸지 않고, 사용하고 있는 함수를 수정하고 싶을 때 사용
- 하나의 함수를 취해서 또 다른 함수를 반환하는 함수
- *args와 &kwargs
- 내부 함수
- 함수 인자

    def main_function():
        print("안녕 나는 메인 함수얌")
        
    def sub_function1():
        print("안녕 나는 서브 함수 1이얌")
        
    def sub_function2():
        print("안녕 나는 서브 함수 2이얌")

이런 main_funnction부터 sub_function1 ~ n개까지 무수히 많을 때, 각 함수에 똑같은 기능을 추가하고 싶다. → 그러면 일일이 모든 함수에 똑같은 코드를 쳐야 하는가?

→놉 ! 데코레이터 라는 걸 추가 해보자!

    import datetime
    
    def datetime_decorator(func):
        def decorated():
            print(datetime.datetime.now())
            func()
            print(datetime.datetime.now())
        return decorated
    
    @datetime_decorator
    def main_function():
        print("안녕 나는 메인 함수얌")
    @datetime_decorator 
    def sub_function1():
        print("안녕 나는 서브 함수 1이얌")
    @datetime_decorator
    def sub_function2():
        print("안녕 나는 서브 함수 2이얌")
        
    main_function()
    
    
    #output
    2019-05-31 19:24:42.829966
    안녕 나는 메인 함수얌
    2019-05-31 19:24:42.829966

1. 먼저 decorator 역할을 하는 함수를 정의하고, 이 함수에서 decorator가 적용될 함수를 인자로 받는다. python은 함수의 인자로 다른 함수를 받을 수 있다는 특징을 이용하는 것이다.
2. decorator역할을 하는 함수 내부에 또 한번 함수를 선언(nested function)하여 여기에 추가적인 작업(시간 출력)을 선언해 주는 것이다
3. nested 함수를 리턴해주면 된다

이렇게 해주면 된다!

***주의: 대상 함수의 수행 중간에 끼어드는 구문은 할 수 없다. → 원래 작업의 앞 뒤에 추가적인 작업을 손쉽게 사용 가능하도록 도와주는 역할이니까!***

또한 한 함수에 여러개의 데코레이터를 할당할 수 있따

- class 형태로 decorator를 맹글어 보자

        import datetime
        
        class Datetime_decorator:
            def __init__(self,f):
                self.func = f
                
            def __call__(self,*args,**kwargs):
                print(datetime.datetime.now())
                self.func(*args, **kwargs)
                print(datetime.datetime.now())
        #         return decorated
        
        class MainClass:
            @Datetime_decorator
            def main_function():
                print("안녕 나는 메인 함수얌")
            
        a =MainClass()
        a.main_function()

### 네임스페이스와 스코프

네임스페이스: 특정 이름이 유일하고, 다른 네임스페이스에서의 같은 이름과 관계가 없는 것을 말한다.

    a = '안녕'
    
    def print_global():
        a = '빠이'
        print('inside print'+a)
        print(id(a))
       
    print(id(a))
    print('outside print '+a)
    print_global()

print_global() 함수에 있는 a는 '안녕'의 전역변수 a와 다른 변수다.

만약 a='빠이'를 print문 다음으로 넣는다면 오류가 뜬다 왜 ? → 전역변수는 static인데 바꾸려고 했으니까!

- 함수 내에서 전역변수 a에 접근하려면?

        a = '안녕'
        
        def print_global():
            global a     
            a = '빠이'
            print('inside print'+a)
            print(id(a))
           
        print(a)
        print_global()
        print(a)
        
        #output
        안녕
        inside print빠이
        2722929030840
        빠이

    근데 global a = '빠이' 이렇게 붙여쓰면 안된다 왜지..?

    아 그리고 생각해보니까 저 a가 바뀌기 전 후 id값이 다른건 당연한거임 → str은 immutable이니까