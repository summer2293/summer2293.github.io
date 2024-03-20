---
layout: post
category: writing Idiomatic python
---

## **1. formatting**

## **1. 모든 상수값은 대문자로 사용하기**

어디서 이 값을 가져왔는지 구별하기 위해  대문자로 선언하자

🙅‍♀️

```python
seconds_in_a_day = 60 * 60 * 24

def display_uptime(uptime_in_seconds):
    percentage_run_time = (
        uptime_in_seconds/seconds_in_a_day) * 100
    return 'The process was up {percent} percent of the
day'.format( percent=int(percentage_run_time))

uptime_in_seconds = 60 * 60 * 24
display_uptime(uptime_in_seconds)
```

🙆‍♀️

```python
SECONDS_IN_A_DAY = 60 * 60 * 24

def display_uptime(uptime_in_seconds):
    percentage_run_time = (
        uptime_in_seconds/SECONDS_IN_A_DAY) * 100
    return 'The process was up {percent} percent of the day'.format( percent=int(percentage_run_time))
# ...
uptime_in_seconds = 60 * 60 * 24
display_uptime(uptime_in_seconds)
```

## **2.PEP8 적용하기**

pep8 - python 언어 표준 규칙

pep8을 적용하고 스타일 검사 플러그인을 설치하면 가독성이 좋아지고, 코드 관리에 좋음

## **3. 싱글라인 코드 지양하기**

`;`을 사용해 싱글라인으로 코드를 짤 수 있지만 가독성이 좋지 않다.

🙅‍♀️

```python
for element in my_list: print(element); print('--------')
```

🙆‍♀️

```python
for element in my_list:
  	print(element)
    print('--------')
```

## **Documentation**

#### **1. PEP-257에서 설명된 docstring 사용하기**

pep257에서 형식적인 규칙을 제시한다. 좋은 문서를 작성하는 규칙은 pep-257을 따르면 도움이 된다.

🙅‍♀️

```python
def calculate_statistics(value_list):
  # calculates various statistics for a list of numbers
	<The body of the function>
```

🙆‍♀️

```python
def calculate_statistics(value_list):
  """Return a tuple containing the mean, median, and mode of a list of integers
    Arguments:
    value_list -- a list of integer values
	"""
   <The body of the function>
```

### **2. docstring 과 주석을 구분하자**

초보자가 하는 실수는 과도하게 문서화 하는 것인데, 주석처리가 과도하다면 코드가 명확하지 않다는 것일 수 있다.

🙅‍♀️

```python
def calculate_mean(numbers):
  """Return the mean of a list of numbers"""
    # If the list is empty, we have no mean!
    if not numbers: return 0
    # A variable to keep track of the running sum
    total = 0
    # Iterate over each number in the list
    for number in numbers: total += number
    # Divide the sum of all the numbers by how
    # many numbers were in the list
    # to arrive at the sum. Return this value.
    return total / len(numbers)
```

🙆‍♀️

```python
def calculate_mean(numbers):
  """Return the mean of a list of numbers"""
  return sum(numbers) / len(numbers)
```

### **3. 작동방식보다 무엇에 대한 코드인지 쓰기**

코드가 수행하는 방식보다 코드가 수행하는 작업을 문서화해야 한다. 문서의 독자는 작동방식을 알 필요는 없다. 작동방식을 알 경우 추상화된 코드에 약점을 만들 수 있다.

🙅‍♀️

```python
def is_prime(number):
  """Mod all numbers from 2 -> number and return True if the value is never 0"""
  for candidate in range(2, number):
    if number % candidate == 0:
      print(candidate) print(number % candidate)
      return False
  return number > 0

```

🙆‍♀️

```python
defs is_prime(number):
  """Return True if number is prime"""
  for candidate in range(2, number):
    if number % candidate == 0:
      return False
```

## **3.imports**

#### **1. import문 순서대로 정리하기**

import 수가 많아지는데, 아래 순서가 표준 순서.

1. standard library modules
2. third-party library modules installed in site-packages
3. modules local to the current project

🙅‍♀️

```python
import os.path
import concurrent.futures
from flask import render_template
from flask import (Flask, request, session, g,
    redirect, url_for, abort,
    render_template, flash, _app_ctx_stack)
import requests

if __name__ == '__main__':
    import this_project.utilities.sentient_network as skynet
    import this_project.widgets
    import sys
```

🙆‍♀️

```python

import concurrent.futures
import os.path
import sys
from flask import (Flask, request, session, g,
    redirect, url_for, abort,
    render_template, flash, _app_ctx_stack)
import requests
import this_project.utilities.sentient_network as skynet
import this_project.widgets
```

## **2. Absolute import 사용하기**

#### **절대 경로**

sys.path 에서 도달할 수 있는 위치에서 모듈 위치 지정

`<package>.<module>.<submodule>`

#### **상대경로**

현재 파일시스템에서 모듈 위치를 기준으로 지정

`..other_module import foo`

상대경로는 네임 스페이스를 복잡하게한다. 큰 모듈의 경우 막대가 어디에서 왔는지 명확하지 않을 수 있다.

🙅‍♀️

```python
from ...package import other_module
```

🙆‍♀️

```python
import package.other_module
import package.other_module as other
```

#### **3. * 사용하지말기**

- 를 사용하지말고 가져오는 모듈 양이 많아지면, `()`를 사용하자. 정의한 이름과 패키지에 이름이 충돌할 경우가 존재한다.

🙅‍♀️

```python
from foo import *
```

🙆‍♀️

```python
from foo import (bar, baz, qux, quux, quuux)
# or even better...
import foo
```

#### **4. try block을 사용하여 패키지가 이용 가능한지 결정하기**

라이브러리를 작성할 때 사용자의 컴퓨터에서 특정 패키지를 사용할 수 없다면, try/except 블록을 사용해서 대체 패키지를 가져와야한다.

🙅‍♀️

```python
import cProfile
print(cProfile.__all__)
```

🙆‍♀️

```python
try:
  import cProfile as profiler
except:
  import profile as profiler
print(profiler.__all__)
```

❓언제 이런게 있을지 궁금

#### **5. 튜플을 사용하여 긴 리스트의 모듈 임포트하기**

특정 모듈에서 많은 임포트가 발생할 때, 튜플을 사용하자.

🙅‍♀️

```python
 from django.db.models import AutoField, BigIntegerField, BooleanField, CharField
 from django.db.models import CommaSeparatedIntegerField, DateField, DateTimeField
```

🙆‍♀️

```python
 from django.db.models import (AutoField, BigIntegerField, BooleanField, CharField, CommaSeparatedIntegerField, DateField, DateTimeField)
```

## **4. Modules and Packages**

#### **1. init.py 를 사용하여 패키지 인터페이스를 단순화하기**

`__init__.py` 에 패키지를 임포트하여 단순화한다.

🙅‍♀️

```python
# If the gizmo directory has an emtpy __init__.py,
# imports like the ones below are necessary, even
# if Gizmo and GizmoHelper are all that clients should ever need to use
from gizmo.client.interface import Gizmo
from gizmo.client.contrib.utils import GizmoHelper
```

🙆‍♀️

```python
# __init__.py:
from gizmo.client.interface import Gizmo
from gizmo.client.contrib.utils import GizmoHelper
#client code:
from gizmo import Gizmo, GizmoHelper
```

## **5. 실행가능한 스크립트**

#### **1. `if __name__ == '__main__'` 패턴을 사용하여 파일을 가져와 실행하기**

Python은 기본 진입점이 없고, 소스파일을 로드하는 즉시 명령문을 실행한다.

독립실행형 스크립트로 상용하기 위해서 `if __name__ == '__main__'` 를 사용하자.

🙅‍♀️

```python
import sys
import os
FIRST_NUMBER = float(sys.argv[1])
SECOND_NUMBER = float(sys.argv[2])
def divide(a, b):
  return a / b
# I can't import this file (for the super
# useful 'divide' function) without the following # code being executed.
if SECOND_NUMBER != 0:
  print(divide(FIRST_NUMBER, SECOND_NUMBER))
```

🙆‍♀️

```python
3.5.1.2 Idiomatic
import sys
import os
def divide(a, b):
  return a / b

if __name__ == '__main__':
  first_number = float(sys.argv[1])
	second_number = float(sys.argv[2])
  if second_number != 0:
    print(divide(first_number, second_number))
```

#### **2. python script를 직접 실행할수 있게 만들기**

`/usr/bin/env python` 첫 번째 줄에서 스크립트를 직접 실행할 수 있다.

`chmod +x <script_name>` 명령을 통해 스크립트를 실행 가능하다.

"python manage.py ''를 입력하는 대신 manage.py 파일을 직접 실행할 수 있기 때문입니다.

#### **3. sys.exit를 사용하여 적절한 오류 코드를 반환**

성공적으로 실행했을 때 0 을 반환하게 하려면 sys.exit 호출하면된다.

🙅‍♀️

```python
if __name__ == '__main__':
  import sys

  if len(sys.argv) > 1:
    argument = sys.argv[1]
    result = do_stuff(argument)
    if result:
      do_stuff_with_result(result)

```

🙆‍♀️

```python
def main():
  import sys
  if len(sys.argv) < 2:
    sys.exit('You forgot to pass an argument')
  argument = sys.argv[1]
  result = do_stuff(argument)
  if not result:
    sys.exit(1)
    do_stuff_with_result(result)
    return 0

  if __name__ == '__main__':
        sys.exit(main())
```

#### **5. sys.argv 사용해서 커맨드라인 파라미터 참조하기**

sys.argv를 사용하여 들어온 파라미터 인자를 처리할 수 있다.

🙅‍♀️

```python
import argparse
if __name__ == '__main__':
  parser = argparse.ArgumentParser(usage="my_cat.py <filename>")
  parser.add_argument('filename', help='The name of the file to use')
  parsed = parser.parse_args(sys.argv)
  print(open(parsed['filename']).read())
```

🙆‍♀️

```python
if __name__ == '__main__':
  try:
print(open(sys.argv[1]).read())
  except IndexError:
    print('You forgot the file name!')
```