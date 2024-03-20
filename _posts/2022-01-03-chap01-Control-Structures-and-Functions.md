---
layout: post
category: writing Idiomatic python
---

## **chapter 1. 제어문과 함수**

### **1. If 문**

### **1. 연쇄 비교시 간결하게 사용하자.**

> python 은 연쇄 연결이 가능하다. 이 표현을 통해 문장을 간결하게 만들고 성능을 향상시킬 수 있다.
> 

🙅‍♀️

```python
if x <= y and y <= z:
     return True
```

🙆‍♀️

```python
if x <= y <= z:
     return True
```

### **2. 조건문 `:` 옆에 분기 코드를 두지말자**

> 들여쓰기를 사용하여 범위를 나타내면 가독성이 좋고, 조건문을 수행할 항목을 쉽게 정할 수 있다. if, else, elif 또한 들여쓰기를 사용해서 각 줄에 표시하는게 좋다.
> 

🙅‍♀️

```python
name = 'Jeff'
address = 'New York, NY'
if name: print(name) print(address)
```

🙆‍♀️

```python
name = 'Jeff'
address = 'New York, NY'
if name: print(name)
    print(address)
```

### **3. 반복된 변수 이름을 사용하지 말자**

> if 문 안에 변수에 여러값 이름을 확인할 때, 그 때 마다 변수 이름을 쓰는건 장황하다. iterable 을 사용하면 가독성이 좋아진다.
> 

🙅‍♀️

```python
is_generic_name = False
name = 'Tom'
if name == 'Tom' or name == 'Dick' or name == 'Harry':

is_generic_name = True
```

🙆‍♀️

```python
name = 'Tom'
is_generic_name = name in ('Tom', 'Dick', 'Harry')
```

### **4. True, False, None를 직접 비교하지 말자.**

모든 값은 boolean 값이 아니더라도,  `true`, `false` 의 값을 가지고 있다. 직접 비교하는 것 보다 객체 내부 값에 의존하는걸 선호한다.

**False 에 해당하는 값**

- None
- False
- zero for numeric types
- empty sequences
- empty dictionaries
- a value of 0
- False returned when either `__len__`
- `__nonzero__` iscalled

외의 값은 다 `True` 가 반환된다.

🙅‍♀️

```python
if foo == True:
```

🙆‍♀️

```python
if foo:
```

하지만 None 은 직접 비교하는게 좋다.

```python
def insert_value(value, position=None):
"""Inserts a value into my container, optionally at the specified position"""
if position is not None:
  ...
```

이 때 `if position:` 으로 비교하면 None 이 아닌 False 로 비교되기 때문에 `is not None` 을 사용하는게 좋다. python 싱글톤 비교는 `is or not` 이며, `==` 가 아니다.

🙅‍♀️

```python
def number_of_evil_robots_attacking():
  return 10

def should_raise_shields():
# "We only raise Shields when one or more giant robots attack, # so I can just return that value..."
 return number_of_evil_robots_attacking()

if should_raise_shields() == True:
  raise_shields()
  print('Shields raised')
else:
  print('Safe! No giant robots attacking')

```

🙆‍♀️

```python
def number_of_evil_robots_attacking():
  return 10

def should_raise_shields():
# "We only raise Shields when one or more giant robots attack, # so I can just return that value..."
 return number_of_evil_robots_attacking()

if should_raise_shields():
  raise_shields()
  print('Shields raised')
else:
  print('Safe! No giant robots attacking')
```

### **5. if/else 삼항연산자**

> 삼항연산자가 없지만, 대체 형식을 사용할 수 있다.
> 

**🙅‍♀️**

```python
foo = True
value = 0
if foo:
  value = 1
print(value)
```

🙆‍♀️

```python
foo = True
value = 1 if foo else 0 print(value)
```

## Chap02 For loops


#### **1. index 변수 대신 enumerate 사용하기**

> 기본 다른 프로그래밍 언어는 index 변수를 사용하지만, python 은 enumerate 를 사용한다
> 

🙅‍♀️

```python
my_container = ['Larry', 'Moe', 'Curly']
index = 0

for element in my_container:
  print('{} {}'.format(index, element))
  index += 1
```

🙆‍♀️

```python
my_container = ['Larry', 'Moe', 'Curly']
 for index, element in enumerate(my_container):
    print('{} {}'.format(index, element))
```

#### **2. `in` 키워드를 통해 내부 값 가져오기**

> 배열 인덱스 값이 있어야 value 값을 가져왔던 기존 프로그래밍 방식. python 에서는 in 키워드를 사용하면 자동으로 내부 값을 가져온다
> 

🙅‍♀️

```python
my_list = ['Larry', 'Moe', 'Curly']
index = 0

while index < len(my_list):
  print(my_list[index]) index += 1
```

🙆‍♀️

```python
my_list = ['Larry', 'Moe', 'Curly']
for element in my_list:
  print(element)
```

#### **3. for loop 끝난 후 else 문 실행하기**

> python 의 for loop 에 else 를 사용할 수 있다. if 문이 다 동작했음에도 break 로 안끊기면, else 문이 시행되는 값이다.
> 

```python
data = [2, 4, 5, 11, 3]
test = 0

for i in data:
  if i > 10:
    test = 1 break

if(test == 0):
  print('10 보다 큰 수 없음')
```

이런 문법을

```python
data = [2, 4, 5, 11, 3]

for i in data:
  if i > 10:
    break
else:
  print('10 보다 큰 수 없음')
```

이렇게 쓸 수 있다.

## **Chapter 3. Functions**

#### **1. mutable object를 function args 로 이용하지 말자**

인터프리터는 실행 후 함수 정의 시 한번만 파이썬 인수를 호출한다. 호출을 하더라도 인수에 대한 다른 평가가 호출되지 않는다.

가변 인수를 받으면, 해당 인자에 값을 추가했을때, 새로운 값을 반환하는게 아닌 기존 인자의 값이 바뀐다.

#### **mutable variable**

- list
- dict
- set
- class instance

### **immutable object**

- string
- int
- Tuple

mutable 을 사용하면 기존 값이 재사용되면서 값이 변경되기 때문에 문제가 생길 수 있다.

🙅‍♀️

```python
def f(a, L=[]):
  L.append(a)
  return L

print(f(1))
print(f(2))
print(f(3))

# [1]
# [1, 2]
# [1, 2, 3]
```

🙆‍♀️

```python
def f(a, L=None):
  if L is None:
    L = []
  L.append(a)
  return L

print(f(1))
print(f(2))
print(f(3))

# This will print
# [1]
# [2]
# [3]
```

#### **2. return value 에 반환식을 사용하자**

보통 우리는 `return value` 를 사용하지만, true 가 나오는 표현식 같은 경우에는 반환식을 return 에 사용하는걸 권장한다. 단순 식 반환이 훨씬 간결하다.

🙅‍♀️

```python
def all_equal(a, b, c):
  result = False
  if a == b == c:
    result = True
return result
```

🙆‍♀️

```python
def all_equal(a, b, c):
  return a == b == c
```

### **3. 키워드 매개변수를 적절히 사용하는법을 배워보자**

#### **키워드인수란?**

> quadratic(a=31, b=93, c=62): 에서 c=62 같은 것
> 

print하는 함수의 경우, 프린트할 값을 고유의 변수로 전달한다. 또한 값 사이의 구분 기호로 사용되는 문자를 변경하고 싶은 경우가 있다. 이럴 때 키워드인수를 적절히 사용해보자.

🙅‍♀️

```python
def print_list(list_value, sep):
  print('{}'.format(sep).join(list_value))

the_list = ['a', 'b', 'c']
the_other_list = ['Jeff', 'hates', 'Java']

print_list(the_list, ' ')
print_list(the_other_list, ' ') print_list(the_other_list, ', ')
```

🙆‍♀️

```python
def print_list(list_value, sep=' '):
  print('{}'.format(sep).join(list_value))

the_list = ['a', 'b', 'c']
the_other_list = ['Jeff', 'hates', 'Java']

print_list(the_list)
print_list(the_other_list)
print_list(the_other_list, ', ')
```

#### **4. `args`, `*kwargs` 사용해서 임의의 변수 허용하기**

보통 함수는 임의의 변수를 받을 상황이 새이는데, 이 때 `*args`, `**kwargs` 를 받아 사용한다.

🙅‍♀️

```python
def make_api_call(foo, bar, baz):
  if baz in ('Unicorn', 'Oven', 'New York'):
    return foo(bar)
  else:
    return bar(foo)

# I need to add another parameter to `make_api_call`
# without breaking everyone's existing code.
# I have two options...
def so_many_options():
  # I can tack on new parameters, but only if I make
  # all of them optional...
    def make_api_call(foo, bar, baz,
                      qux=None, foo_polarity=None,
                      baz_coefficient=None,
                      quux_capacitor=None,
                      bar_has_hopped=None,
                      true=None, false=None,
                      file_not_found=None):
      # ... and so on ad infinitum
      return file_not_found

def version_graveyard():
  # ... or I can create a new function each time the signature
  # changes.
  def make_api_call_v2(foo, bar, baz, qux):
    return make_api_call(foo, bar, baz) - qux

  def make_api_call_v3(foo, bar, baz, qux, foo_polarity):
    if foo_polarity != 'reversed':
      return make_api_call_v2(foo, bar, baz, qux)
    return None
```

🙆‍♀️

```python

def make_api_call(foo, bar, baz):
  if baz in ('Unicorn', 'Oven', 'New York'):
    return foo(bar)
  else:
    return bar(foo)

# I need to add another parameter to `make_api_call`
# without breaking everyone's existing code.
# Easy...
def new_hotness():
  def make_api_call(foo, bar, baz, *args, **kwargs):
    # Now I can accept any type and number of arguments
    # without worrying about breaking existing code.
    baz_coefficient = kwargs['the_baz']
    # I can even forward my args to a different function without # knowing their contents!
    return baz_coefficient in new_function(args)
```

#### **언제 사용을 할까?**

> exception 이랑 다르게하더라도, 간결하게 할 수있음 한다.
> 
> 
> keyword argument 를 써서 옵션으로 들어오는 경우가 있다면, 받을 수 있다.
> 

#### **5. 함수를 값으로 처리하기**

파이썬은 모든 것은 객체이기 때문에, 함수도 객체로 취급된다. 따라서 함수 호출한 값을 리턴할 수 있다.

🙅‍♀️

```python
def print_addition_table():
  for x in range(1, 3):
    for y in range(1, 3):
      print(str(x + y) + '\n')

def print_subtraction_table():
  for x in range(1, 3):
    for y in range(1, 3):
      print(str(x - y) + '\n')

def print_multiplication_table():
  for x in range(1, 3):
    for y in range(1, 3):
      print(str(x * y) + '\n')

def print_division_table():
  for x in range(1, 3):
    for y in range(1, 3):
      print(str(x / y) + '\n')

print_addition_table()
print_subtraction_table()
print_multiplication_table()
print_division_table()
```

🙆‍♀️

```python
import operator as op
def print_table(operator):
  for x in range(1, 3):
    for y in range(1, 3):
      print(str(operator(x, y)) + '\n')

for operator in (op.add, op.sub, op.mul, op.itruediv):
  print_table(operator)
```

## **1.4 Exception**

#### **1. 예외를 두려워하지 말자.**

파일 이름을 인자로 받고, 파일 내용에 대해 처리하는 함수일 경우, 해당 경로의 파일을 찾을 수 없는 경우에 대한 건은 예외 처리를 하지 않는다. 파일 시스템 자체를 사용할 수 없는 경우 예외를 발생시키는게 좋다.

#### **❓file not found 정도면 해야하는거아냐?**

> 파일이 없는게 심각한 문제냐. 심각하지 않다. 심각한 상황에서만 예외처리를 해라. 빈 내용을 반환해도 된다면, 심각하지 않음.
> 

예외처리를 오남용하는것은 좋지 않다.

- 프로그램의 흐름을 따라가기 어렵게 만든다
- 함수를 호출 전파할 때 짐이 된다.
- 성능에 영향을 끼치는 점

때문에 많은 언어에서는 예외를 규정하는 명시적 표준이 존재한다.

파이썬의 경우 예외를 사용한다. for문에서도 사용하는데, iter(), getitem 을 반복할 때마다

```
StopIteration
```

이 사용된다.

```python
#!py
words = ['exceptions', 'are', 'useful']
for word in words:
  print(word)
```

`__iter__()` 및 `__getitem__()` 함수는 반복할 항목이 소진될 때 예외를 발생시키는 데 필요합니다. `__iter__()`는 앞에서 설명한 대로 StopIteration 예외를 발생시키고 `__getitem__()`은 IndexError 예외를 발생시킵니다. 이것은 멈출 때를 아는 방법입니다.
따라서 파이썬에서 예외를 사용해도 괜찮은지 궁금할 때마다 이것만 기억하세요. 가장 사소한 프로그램을 제외한 모든 프로그램에서 이미 사용하고 있을 것입니다.

#### **2. EAFP 스타일로 예외 작성하기.**

예외를 사용하지 않는 코드는 `if` 문을 통해 예외가 날만한 부분을 작성하는데, 이렇게 if 가 많아지면 명확해지지 않고, 다중 스레드 환경에서 실패할 수 있다.

> ❓멀티쓰레드?? 왜?
> 
> 
> typecasting 하거나, 올바르지 않을 때 조작할대 lbyl 인건데, 멀티쓰레드 환경이 되면, 변환되는 중간에 접근을 할 수 있다. 쓰레드가 나온게 메모리는 어떻게 효율적으로 쓸것이냐. 공유메모리가 생긴다. 여러 쓰렉드가 같이 쓰는 값을 생긴다. 같은 함수를 호출하는데, 다른 호출을 할 때 들어온 **인수가 같은 값을 가르키고 있다면**, 조작하고 잇을 때 같은 값으로 실행해버리면, 문제가 생길 수 있다.
> 

#### **LBYL(Look Before You Leap)**

코드를 타기 전에 예외 처리하기. 우리는 모든 에러를 예측할 수 없기 때문에 EAFP 스타일로 예외를 작성해야 한다.

#### **Easy to Ask For Forgiveness than Permission**

#### **[사과하는게 허락을 구하는것보다 낫다. 저지르고봐라]**

원칙에 따라 작성된 코드는 잘 될 거라고 가정하고, 그렇지 않은 경우 예외를 포착.

"[It's] Easy to Ask for Forgiveness than Permission(EAFP)'' 원칙에 따라 작성된 코드는 일이 잘 될 것이라고 가정하고 그렇지 않은 경우 예외를 포착합니다. 코드의 진정한 목적을 전면 중앙에 두어 명확성을 높입니다.

🙅‍♀️

```python
def get_log_level(config_dict):
  if 'ENABLE_LOGGING' in config_dict:
    if config_dict['ENABLE_LOGGING'] != True:
      return None
    elif not 'DEFAULT_LOG_LEVEL' in config_dict:
      return None
    else:
      return config_dict['DEFAULT_LOG_LEVEL']
    else:
      return None
```

🙆‍♀️

```python
def get_log_level(config_dict): try:
    if config_dict['ENABLE_LOGGING']:
      return config_dict['DEFAULT_LOG_LEVEL']
    except KeyError:
      # if either value wasn't present, a # KeyError will be raised, so
      # return None
      return None
```

if 로 분기처리 대신 except 로 예외 잡기.

#### **3. `swallowing` 예외를 피해라**

초보자들은 except를 사용하면 raise 를 통해 오류를 없애햐한다고 생각한다.

예외가 있을경우 그걸 잡아야된다고 생각하는데, 처리할 의도가 없다면 bare raise 를 추가해라.

🙅‍♀️

```python
import requests
 def get_json_response(url):
    try:
      r = requests.get(url)
      return r.json()
    except:
      print('Oops, something went wrong!')
      return None
```

🙆‍♀️

```python
import requests
def get_json_response(url):
  return requests.get(url).json()

# If we need to make note of the exception, we # would write the function this way...
def alternate_get_json_response(url):
  try:
    r = requests.get(url)
    return r.json()
  except:
    # do some logging here, but don't handle the exception
    raise
```

> exception 의 골자: 치명적인 에러가 있을 경우 진행하지 마라.
> 
> 
> 로직을 간결하게 하는거지, 치명적인거에 대응하라는게 아님. 파이썬으로 코드를 작성하는ㄱ ㅘ정에서도 치명적인 상황이 있을 경우에, raise 나 return 을 해버리면, 로그가 사진다. 이 에러는 적절히 처리되어서 문제가 되지 않는다라는 뜻이기 때문에 exception 을 쓸 때 로그를 삼키지 말아라. 이게 모든 언어에서 다 나오는 내용이다. 모든 클린코드에 다 나오는 내용. 그래서 다른 책을 찾아도 볼 수 있는 표현이어서 대충 정리하긴 했는데. return 대신 raise 를 쓰라는 내용.
>