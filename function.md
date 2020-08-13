```python
def my_map(function, Object):
    """iterable 한 자료를 함수의 결과로 반환해주는 iterator이다."""
    for i in Object:
        yield function(i)
```


```python
def my_map1(function, Object):
    """iterable 한 자료를 함수의 결과로 반환해주는 generator이다."""
    return (function(i) for i in Object)
```


```python
A = list(my_map(Function, x))
B = list(my_map1(Function, [x[i] for i in x]))
```


```python
print(A)
print(B)
```


```python
def my_filter(function, Object):
    """만약에 함수 반환값이 참이라면 iterable 한 자료를 yield하는 iterator"""
    for i in Object:
        if function(i) == True:
            yield i
        else:
            continue
```


```python
print(list(my_filter(lambda x: x > 0, range(-5,10))))
```


```python
def my_reduce(function, Object, default = None):
    """iterable 을 지정한 함수에 따라 계산한 후 결과를 반환한다."""
    Ob = iter(Object)
    if default == None:
        st = next(Ob)
    else:
        st = default
    for i in Ob:
        st = function(st, i)
    return st
        
```


```python
print(my_reduce(lambda x,y : x+y, [1,2,3,4,5]))
```


```python
def my_reduce(function, Object, default=None):
    """iterable 을 지정한 함수에 따라 계산한 후 결과를 반환한다."""
    for i in Object:
        if default is None:
            dumi = i
            dumi = function(dumi, i)
        else:
            dumi = default
        dumi = function(dumi, i)
    return dumi

```


```python
def prime_range(start, end):
    """입력받은 숫자에 해당되는 범위의 값을 반복 가능한 객체로 만들어 값이 참일때 yeid한다."""
    for i in range(start,end):
        for j in range(2,i):
            if (i%j==0):
                break
            else:
                yield i
                break
```


```python
list(prime_range(1, 102))
```


```python
def calc(value1, value2, operator):
    """값 두개와 함수를 받아 계산값을 리턴해주는 함수"""
    
    operator = eval(operator)
    
    return operator(value1, value2)

def div(value1, value2):

    return value1 / value2

def plus(value1, value2):

    return value1 + value2

def minus(value1, value2):

    return value1 - value2

def multi(value1, value2):

    return value1 * value2

def mod(value1, value2):

    return value1 % value2

def power(value1, value2):

    return value1 ** value2

calc(2, 4, 'power')
```


```python
def show_info(func):
    """함수의 리턴값 위치인자 키워드인자의 정보를 전달해주는 함수"""
    def pythonzoa(*args, **kwargs):
        result = func(*args, **kwargs)
        print("return : args[{}] = ( type : {}, value : {} )".format(result.index(result),type(result),result))
        for index, val in enumerate(args):
            print("index : args[{}] = ( type : {}, value : {} )".format(index,type(val),val))
        for index, val in enumerate(kwargs):
            print("keyword : keyword[{}] = (type : {}, value : {} )".format(index,type(val),val))
        return func
    return pythonzoa
    
@show_info
def other_function(a,b,c="tu"):
    return a+b+c
other_function("hi","hd",c = "cf")
```

    return : args[0] = ( type : <class 'str'>, value : hihdcf )
    index : args[0] = ( type : <class 'str'>, value : hi )
    index : args[1] = ( type : <class 'str'>, value : hd )
    keyword : keyword[0] = (type : <class 'str'>, value : c )





    <function __main__.other_function(a, b, c='tu')>


