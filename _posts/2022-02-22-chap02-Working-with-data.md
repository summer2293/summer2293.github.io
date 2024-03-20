---
layout: post
category: writing Idiomatic python
---

## **1. 변수**

#### **1. 같은 값의 변수는 다중 할당을 사용해라**

파이썬은 다중 할당을 지원한다. 간결하게 값을 정의할 수 있다.

🙅‍♀️

```python
x = 'foo'
y = 'foo'
z = 'foo'
```

🙆‍♀️

```python
x = y = z = 'foo'
```

#### **2. 변수 값 스와핑 할 때 임시변수를 사용하지 마라.**

파이썬에선 튜플을 사용하면 좋다

🙅‍♀️

```python
foo = 'Foo'
bar = 'Bar'
temp = foo
foo = bar
bar = temp
```

🙆‍♀️

```python
foo = 'Foo'
bar = 'Bar'
(foo, bar) = (bar, foo)
```

## **2. Strings**

### **1.체인을 통한 간단한 string 변경하기**

일부 데이터에 대한 변형을 연속적으로 할 때, 호출을 연결하는 것이 임시 변수를 사용하는 것 보다 훨씬 간결합니다. 너무많은 연결은 좋지 않고, 3개정도가 좋습니다.

🙅‍♀️

```
book_info = ' The Three Musketeers: Alexandre Dumas'

formatted_book_info = book_info.strip()
formatted_book_info = formatted_book_info.upper()
formatted_book_info = formatted_book_info.replace(':', ' by')
```

🙆‍♀️

```
book_info = ' The Three Musketeers: Alexandre Dumas'

formatted_book_info = book_info.strip().upper().replace(':', ' by')
```

#### **2. ''.join 사용해 리스트값 단순한 문자열 만들기**

''.join 을 사용하면 더 빠르고 메모리도 덜 사용할 수 있다. '' 안에는 합칠 때 추가하고싶은 기호를 쓰면 추가가 된다.

**🙅‍♀️**

```python
result_list = ['True', 'False', 'File not found']

result_string = ''
for result in result_list:
  result_string += result
```

**🙆‍♀️**

```python
result_list = ['True', 'False', 'File not found']
result_string = ''.join(result_list)
>>> result_string
'TrueFalseFile not found'

result_string = ','.join(result_list)
>>> result_string
'True,False,File not found'
```

#### **3. ord 사용하여 아스키코드 쉽게 쓰기**

문자를 ascii 코드로 변환하거나, ascii코드를 문자로 변환할 경우 `ord()` 함수를 사용하면 간편하다.

🙅‍♀️

```python
hash_value = 0
character_hash = {
'a': 97, 'b': 98, 'c': 99, # ... 'y': 121, 'z': 122,
}

some_string = "abcabc"
for e in some_string:
  hash_value += character_hash[e]

hash_value
```

🙆‍♀️

```python
hash_value = 0
some_string = "abcabc"
for e in some_string:
  hash_value += ord(e)

hash_value
```

#### **4. format string 을 위한 함수를 선호**

문자열을 포맷하는 방법

1. 하드코딩 문자열과 변수가 혼합된 문자열 생성
2. `+` 를 이용한 문자열 변수 결함
3. % 를 이용한 방법

문자열 형식을 지정하기 위해 format 함수를 을 사용하는게 제일 좋다. 간결하며, 이름이 지정된 자리 표시자를 사용하고, 문자열 너비를 제어할 수 있다.

🙅‍♀️

```python
def get_formatted_user_info_worst(user):
  # 변환 오류가 발생하기 쉽다.
  return 'Name: ' + user.name + ', Age: ' + \
          str(user.age) + ', Sex: ' + user.sex

def get_formatted_user_info_slightly_better(user):
# 타입을 알 필요 없다.
# 문자열과 자리표시자의 구분이 없다.
  return 'Name: %s, Age: %i, Sex: %c' % (user.name, user.age, user.sex)
```

🙆‍♀️

```python
def get_formatted_user_info(user):
# 간결하다. 어디가 포맷하는 곳인지 알 수 있다.
  return 'Name: {user.name}, Age: {user.age}, Sex: {user.sex}'.format(user=user)
```

## **3. Lists**

### **1. comprehension 을 사용한 기존 목록 변형하기**

기존 데이터를 변형할 때 comprehension 을 사용하면 코드의 명확성이 높아진다. cPy

thon을 사용하기 때문에 성능 또한 높아진다.

🙅‍♀️

```
some_other_list = range(10)
some_list = list()

for element in some_other_list:
  if is_prime(element):
    some_list.append(element + 5)
```

🙆‍♀️

```
some_other_list = range(10)
some_list = [element + 5
             for element in some_other_list
             if is_prime(element)
            ]
```

### **2. 음수 인덱스 사용하기**

음수 인덱스를 사용하면 목록의 끝에서 시작해서 거꾸로 계산된다.

🙅‍♀️

```
def get_suffix(word):
  word_length = len(word) return word[word_length - 2:]
```

🙆‍♀️

```
def get_suffix(word):
  return word[-2:]
```

#### **3. map, filter 보다 comprehension 사용하기**

python에서 사용하는 map, filter외에 comprehension 사용이 훨씬 간결하고 읽기 쉽다.

🙅‍♀️

```python
the_list = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

def is_odd(number):
  return number % 2 == 1 odd_numbers = filter(is_odd, the_list)

odd_numbers_times_two = list(map(lambda x: x * 2, odd_numbers))
```

🙆‍♀️

```python
the_list = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
odd_numbers_times_two = [n * 2 for n in the_list if n % 2 == 1]
```

#### **4. built-in 함수 사용하기**

초보 개발자들은 sum 을 놓치는 경우가 많다. 내장 함수가 있다면 내장 함수를 사용하는 것이 가장 좋다.

🙅‍♀️

```python
the_list = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
the_sum = 0
for element in the_list:
  the_sum += element
```

🙆‍♀️

```python
the_list = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
the_sum = sum(the_list)
```

#### **5. all()을 이용해 iterable 요소가 true인지 확인하기**

sum 과 마찬가지로 all 또한 개발 초보들이 놓치는 함수. iterable 요소가 모두 true 면 true를 반환해준다.

🙅‍♀️

```python
def contains_zero(iterable):
  for e in iterable:
    if e == 0: return True
  return False
```

🙆‍♀️

```python
def contains_zero(iterable):
  # 0 is "Falsy," so this works
  return not all(iterable)
```

#### **6. `` 연산자를 이용하여 나머지 나타내기**

함수에 대한 인자를 다룰 때 `*` 연산자를 사용해 시퀀스의 나머지 부분을 나타낼 수 있다.

🙅‍♀️

```python
 some_list = ['a', 'b', 'c', 'd', 'e']
(first, second, rest) = some_list[0], some_list[1], some_list[2:]
print(rest)
(first, middle, last) = some_list[0], some_list[1:-1], some_list[-1]
print(middle)
(head, penultimate, last) = some_list[:-2], some_list[-2], some_list[-1]
print(head)
```

🙆‍♀️

```python
some_list = ['a', 'b', 'c', 'd', 'e']
(first, second, *rest) = some_list
print(rest)
(first, *middle, last) = some_list
print(middle)
(*head, penultimate, last) =
some_list
print(head)
```

## **4.Dictionaries**

#### **1. Switch...case 대신 dict사용하기**

python 에는 switch..case 구문이 없다. `if` `else` 를 사용하는건 느리고, dict를 통해 해결할 수 있다.

🙅‍♀️

```python
def apply_operation(left_operand, right_operand, operator):
  if operator == '+':
    return left_operand + right_operand
  elif operator == '-':
    return left_operand - right_operand
  elif operator == '*':
    return left_operand * right_operand
  elif operator == '/':
    return left_operand / right_operand
```

🙆‍♀️

```python
def apply_operation(left_operand, right_operand, operator):
  import operator as op
  operator_mapper = {
    '+': op.add,
    '-': op.sub,
    '*': op.mul,
    '/': op.truediv
  }
  return operator_mapper[operator](left_operand, right_operand)
```

#### **2. dict.get 사용해 default value 적용하기**

🙅‍♀️

```python
log_severity = None
if 'severity' in configuration:
  log_severity = configuration['severity']
else:
  log_severity = 'Info'
```

🙆‍♀️

```python
log_severity = configuration.get('severity', 'Info')
```

#### **3. dict comprehenstion 사용해서 명확성 높이기**

list comprehension 을 사용하는것 처럼 dict comprehension 을 사용할 수 있다.

**🙅‍♀️**

```python
user_email = {}
 for user in users_list:

if user.email:
 user_email[user.name] = user.email
```

🙆‍♀️

```python
user_email = {user.name: user.email
              for user in users_list if user.email}
```

## **2.5 Sets**

### **1. set operation의 이해**

set은 dict처럼 `{}`를 사용하지만, dict과 달리 비슷하지만, value 가 없다.

set class는 interable, container를 가지고있어 for loop 사용이 가능하다.

### **합집합: A, B, 또는 A 및 B 모두의 요소를 결합합니다 (A | B)**

### **교집합: A와 B 모두에 있는 이러한 요소의 교차점 (A & B)**

### **차집합 가 아닌 A에서 요소 간의 차이점. (A - B)**

### **참고: 여기에서 순서가 중요합니다. A - B는 반드시 B - A와 동일하지 않습니다.**

### **대칭 차이: A ^ B**

데이터 목록에서, 스퀀스 기반으로 요소를 찾을 수 있다.

**🙅‍♀️**

```
def get_both_popular_and_active_users():
  # Assume the following two functions each return a
  # list of user names
  most_popular_users = get_list_of_most_popular_users()
  most_active_users = get_list_of_most_active_users()
  popular_and_active_users = []
  for user in most_active_users:
    if user in most_popular_users:
      popular_and_active_users.append(user)
```

🙆‍♀️

```
def get_both_popular_and_active_users():
  # Assume the following two functions each return a # list of user names
  return(set(get_list_of_most_active_users()) & set(get_list_of_most_popular_users()))
```

### **2. set comprehension 을 정확하게 사용하기**

set comprehension을 사용하면 간결하게 나타낼 수 있다.

**🙅‍♀️**

```
users_first_names = set()
for user in users:
    users_first_names.add(user.first_name)
```

🙆‍♀️

```
users_first_names = {user.first_name for user in users}
```

### **3. set을 사용하여 중복값 제거하기**

중복된 값을 목록 중 고유한 값을 필요로 할 때 set을 사용.

1. 값에 고유한 요소만 존재
2. 존재하는 요소가 들어올 경우 무시

**🙅‍♀️**

```
unique_surnames = []
for surname in employee_surnames:
  if surname not in unique_surnames:
    unique_surnames.append(surname)

def display(elements, output_format='html'):
  if output_format == 'std_out':
    for element in elements:
      print(element)
  elif output_format == 'html':
    as_html = '<ul>'
    for element in elements:
    as_html += '<li>{}</li>'.format(element)
    return as_html + '</ul>'
  else:
    raise RuntimeError('Unknown format {}'.format(output_format))
```

🙆‍♀️

```
unique_surnames = set(employee_surnames)
def display(elements, output_format='html'):
  if output_format == 'std_out':
    for element in elements:
      print(element)
  elif output_format == 'html': as_html = '<ul>'
    for element in elements:
      as_html += '<li>{}</li>'.format(element)
      return as_html + '</ul>'
else:
  raise RuntimeError('Unknown format {}'.format(output_format))
```

### **2. 튜플**

```
>>> t1 = ()
>>> t2 = (1,)
>>> t3 = (1, 2, 3)
>>> t4 = 1, 2, 3
>>> t5 = ('a', 'b', ('ab', 'cd'))
```

### **1. `collections.namedtuple` 을 사용해 많은 튜플들을 더 깔끔하게 사용하기**

튜플 - 논리적으로 배열된 데이터를 사용

데이터베이스 테이블 단일 행 반환과 같은 목록으로 사용한다. `namedtuple`을 사용하면 인덱스가 아닌 이름으로 필드에 액세스 할 수 있다.

가독성과 유지보수성을 높일 수 있다.

**🙅‍♀️**

```
def print_employee_information(db_connection):
  db_cursor = db_connection.cursor()
  results = db_cursor.execute('select * from employees').fetchall()
  for row in results:
    print(row[1] + ', ' + row[0] + ' was hired '
    'on ' + row[5] + ' (for $' + row[4] + ' per annum)'
    'into the ' + row[2] + ' department and reports to ' + row[3])
```

🙆‍♀️

```
from collections import namedtuple

EmployeeRow = namedtuple('EmployeeRow', ['first_name', 'last_name', 'department', 'manager', 'salary', 'hire_date'])

EMPLOYEE_INFO_FMT = '{last_name}, {first_name} was hired on \
{hire_date} (for ${salary} per annum) into the {department} \
department and reports to {manager}'

def print_employee_information(db_connection):
  db_cursor = db_connection.cursor()
  results = db_cursor.execute('select * from employees').fetchall()
  for row in results:
    employee = EmployeeRow._make(row)
    print(EMPLOYEE_INFO_FMT.format(**employee._asdict()))
```

### **2. 무시해야하는 튜플에는 `_`사용하기**

튜플을 데이터와 매칭할 때, 보통 모든 데이터를 필요로 하지 않는다. 이때 사용하지 않는 데이터에는 `_`를 붙혀서 이 데이터는 사용하지 않는다고 알려주는것이 좋다.

🙅‍♀️

```python
(name, age, temp, temp2) = get_user_info(user)
if age > 21:
    output = '{name} can drink!'.format(name=name)
# "Wait, where are temp and temp2 being used?"
```

🙆‍♀️

```python
(name, age, _, _) = get_user_info(user)
if age > 21:
    output = '{name} can drink!'.format(name=name)
```

### **3. 튜플을 사용하여 압축 풀기**

하나하나 풀지 않고 (a, b, c)로 한번에 풀 수 있다.

🙅‍♀️

```python
list_from_comma_separated_value_file = ['dog', 'Fido', 10]
animal = list_from_comma_separated_value_file[0]
name = list_from_comma_separated_value_file[1]
age = list_from_comma_separated_value_file[2]
output = ('{name} the {animal} is {age} years old'.format(
    animal=animal, name=name, age=age))
```

🙆‍♀️

```python
list_from_comma_separated_value_file = ['dog', 'Fido', 10]
(animal, name, age) = list_from_comma_separated_value_file

output = ('{name} the {animal} is {age} years old'.format(
    animal=animal, name=name, age=age))
```

### **4. 튜플을 사용하여 다양한 변수값 리턴하기**

함수에서 여러값을 반환하는게 필요할때 이상적으로 사용할 수 있다.

🙅‍♀️

```python
from collections import Counter

STATS_FORMAT = """Statistics:
Mean: {mean}
Median: {median}
Mode: {mode}"""

def calculate_mean(value_list):
  return float(sum(value_list) / len(value_list))

def calculate_median(value_list):
  return value_list[int(len(value_list) / 2)]

def calculate_mode(value_list):
  return Counter(value_list).most_common(1)[0][0]

values = [10, 20, 20, 30]
mean = calculate_mean(values)
median = calculate_median(values)
mode = calculate_mode(values)

print(STATS_FORMAT.format(mean=mean, median=median,
        mode=mode))
```

🙆‍♀️

```python
from collections import Counter

STATS_FORMAT = """Statistics:
Mean: {mean}
Median: {median}
Mode: {mode}"""

def calculate_staistics(value_list):
  mean = float(sum(value_list) / len(value_list))
  median = value_list[int(len(value_list) / 2)]
  mode = Counter(value_list).most_common(1)[0][0]
  return (mean, median, mode)

(mean, median, mode) = calculate_staistics([10, 20, 20, 30])
print(STATS_FORMAT.format(mean=mean, median=median, mode=mode))
```

## **7. classes**

### **1. `isinstance` 함수를 사용하여 객체 타입 결정**

파이썬은 유형을 지정하지 않지만 내부적으로 정해지기 때문에 타입 에러가 발생할 수 있다.

`isinstance`를 이용해 변수 타입이 달라질 때마다 작동방식을 변경할 수 있다.

🙅‍♀️

```python
def get_size(some_object):
"""Return the "size" of *some_object*, where size = len(some_object) for sequences, size = some_object for integers and floats, and size = 1 for True, False, or None."""
	try:
		return len(some_object)
	except TypeError:
		if some_object in (True, False, type(None)):
			return 1
  	else:
			return int(some_object)

print(get_size('hello'))
print(get_size([1, 2, 3, 4, 5]))
print(get_size(10.0))

```

🙆‍♀️

```python
def get_size(some_object):
  if isinstance(some_object, (list, dict, str, tuple)):
    return len(some_object)
  elif isinstance(some_object, (bool, type(None))):
    return 1
  elif isinstance(some_object, (int, float)):
    return int(some_object)

  print(get_size('hello'))
print(get_size([1, 2, 3, 4, 5]))
print(get_size(10.0))
```

### **2. private를 사용할땐 `_` 를 쓰기**

파이썬에서 모든 속성은 public이지만, priviate value로 사용할 경우 의도를 명확하게 하기위해 `__ 를 붙힌다.

1. 클라이언트가 사용하지 않는 `protected`값은 `_`하나를 사용한다.
2. 서브클래스가 접근할 수 없는 `private` 속성은 `__` 두개를 사용한다.

🙅‍♀️

```python
class Foo():
  def __init__(self):
          self.id = 8
          self.value = self.get_value()
  def get_value(self):
    pass

  def should_destroy_earth(self):
    return self.id == 42

class Baz(Foo):
  def get_value(self, some_new_parameter):
    pass

class Qux(Foo):
  def __init__(self):
    super(Qux, self).__init__()
    self.id = 42

q = Qux()
b = Baz()  # Raises 'TypeError'
q.should_destroy_earth()  # returns True
q.id == 42  # returns True

```

🙆‍♀️

```
class Foo():
  def __init__(self):
      self.__id = 8
      self.value = self.__get_value() # Our 'private copy'

  def get_value(self):
    pass

  def should_destroy_earth(self):
    return self.__id == 42

class Baz(Foo):
  def get_value(self, some_new_parameter):
    pass

class Qux(Foo):
def __init__(self):
    self.id = 42
    # No relation to Foo's id, purely coincidental
    super(Qux, self).__init__()

q = Qux()
b = Baz()
with pytest.raises(AttributeError):
  getattr(q, '__id')
```

### **3. `@property` 를 사용하여 직접 클래스 구현에 대한 대비**

`@property` 를 사용하여 데이터 액세스를 대비할 수 있다. @property 를 사용함으로써 미래 여러값들 getter, setter 값을 다르게 적용하여 사용할 수 있다.

🙅‍♀️

```
class Product():
    def __init__(self, name, price):
        self.name = name
        # We could try to apply the tax rate here, but the object's price
        # may be modified later, which erases the tax
        self.price = price
```

🙆‍♀️

```
class Product():
    def __init__(self, name, price):
        self.name = name
        self._price = price
    @property
    def price(self):
        # now if we need to change how price is calculated, we can do it
        # here (or in the      "setter" and __init__)
        return self._price * TAX_RATE
    @price.setter
    def price(self, value):
        # The "setter" function must have the same name as the property
        self._price = value
```

### **🤔4 기계가 읽을 수 있는 클래스를 위해 `__repr__` 사용하기**

`__str__` 은 사람이 읽을 수 있는 방식으로 클래스를 사용하지만`__repr__` 는 기계가 사용할수 있는 방식으로 사용된다. 객체를 재구성하는데 필요한 모든 정보가 포함되어야 하며 이걸 통해 다른 인스턴스를 구분할 수 있다.

🙅‍♀️

```python
class Foo():
  def __init__(self, bar=10, baz=12, cache=None):
        self.bar = bar
        self.baz = baz
        self._cache = cache or {}
  def __str__(self):
    return 'Bar is {}, Baz is {}'.format(self.bar, self.baz)

  def log_to_console(instance):
      print(instance)
log_to_console([Foo(), Foo(cache={'x': 'y'})])
```

🙆‍♀️

```python
class Foo():
	def __init__(self, bar=10, baz=12, cache=None):
    	self.bar = bar
       self.baz = baz
       self._cache = cache or {}
	def __str__(self):
			return '{}, {}'.format(self.bar, self.baz)

  def __repr__(self):
    return 'Foo({}, {}, {})'.format(self.bar, self.baz, self._cache)

def log_to_console(instance):
  print(instance)

log_to_console([Foo(), Foo(cache={'x': 'y'})])
```

??어렵다

사용자한테 필요 없어repr에만 넣은건가?

기계는 컴퓨터 디바이스를 말하는건가

### **5. 객체 출력시 `__str__` 를 이용하여 사람들이 읽을수 있게 반환**

인스턴스를 `print`로 출력하면 인스턴스 아이디 값이 나오지만, `__str__` 를 사용해 사람들이 읽을 수 있게 변환할 수 있다.

🙅‍♀️

```python
class Point():
  def __init__(self, x, y):
    self.x = x
    self.y = y

p = Point(1, 2)
print(p)
```

🙆‍♀️

```python

class Point():
  def __init__(self, x, y):
        self.x = x
        self.y = y
  def __str__(self):
    return '{0}, {1}'.format(self.x, self.y)

  p = Point(1, 2)
print(p)

# Prints '1, 2'
```

## **8. Context Managers**

### **1. 컨텍스트 관리자 사용하기**

### **컨텍스트 매니저**

원하는 타이밍에 정확하게 리소스를 할당하고 제공하는 역할

리소스 관리를 안전하고 명확하게 만들 수 있다. 컨텍스트 관리자를 사용하지 않으면 에러가 발생했을 때 열린 파일을 닫을 수 없다.

🙅‍♀️

```python
file_handle = open(path_to_file, 'r')
for line in file_handle.readlines():
  if raise_exception(line):
    print('No! An Exception!')

```

🙆‍♀️

```python
with open(path_to_file, 'r') as file_handle:
  for line in file_handle:
    if raise_exception(line):
      print('No! An Exception!')
```

## **9. Genorators**

#### **1. 간단한 이터레이션에 generator expression 사용하기**

리스트 컴프리헨션을 사용하면 모든 데이터를 메모리에 적재시키므로, 하나씩 올리는 제너레이터를 사용하자

🙅‍♀️

```python
for uppercase_name in [name.upper() for name in get_all_usernames()]:
  process_normalized_username(uppercase_name)
```

🙆‍♀️

```python
for uppercase_name in (name.upper() for name in get_all_usernames()):
  process_normalized_username(uppercase_name)
```

#### **2. 제너레이터를 사용한 레이지로드**

한번에 처리하는게 계산이 많이 거릴것 같은 경우에는 이터레이터를 반환하는 제너레이터를 사용해서 호출을 중단처리를 통해 효율을 높이는게 좋은듯?

🙅‍♀️

```python
def get_twitter_stream_for_keyword(keyword):
  imaginary_twitter_api = ImaginaryTwitterAPI()
  if imaginary_twitter_api.can_get_stream_data(keyword):
    return imaginary_twitter_api.get_stream(keyword)

current_stream = get_twitter_stream_for_keyword('#jeffknupp')

for tweet in current_stream:
    process_tweet(tweet)

def get_list_of_incredibly_complex_calculation_results(data):
  return [first_incredibly_long_calculation(data),
            second_incredibly_long_calculation(data),
            third_incredibly_long_calculation(data),
            ]
```

🙆‍♀️

```python
def get_twitter_stream_for_keyword(keyword):
  imaginary_twitter_api = ImaginaryTwitterAPI()
  while imaginary_twitter_api.can_get_stream_data(keyword):
    yield imaginary_twitter_api.get_stream(keyword)

for tweet in get_twitter_stream_for_keyword('#jeffknupp'):
  if got_stop_signal:
    break
    process_tweet(tweet)

def get_list_of_incredibly_complex_calculation_results(data):
  yield first_incredibly_long_calculation(data)
  yield second_incredibly_long_calculation(data)
  yield third_incredibly_long_calculation(data)
```
