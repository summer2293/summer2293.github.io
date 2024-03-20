---
layout: post
category: writing Idiomatic python
---

## **1. 재발명 피하기**

#### **1. PyPI 알아보기**

https://pypi.org/

필요한 라이브러리가 있는 경우 PyPI 에 있는지 검색해보고 사용한다.

`pip install ~`

### **2. python 표준 라이브러리 공부하기**

표준 라이브러리 기능을 구현하지 말고, 관련 라이브러리를 사용하자

- 시간절약
- 명확한 코드

표준라이브러리를 사용하는 것 만큼 품질을 보장하는 것은 없다.

## **2. 모듈**

#### **1. itertools 모듈 배우기**

#### **itertools**

빠르고, 메모리 효율을 제공하는 라이브러리. 체이닝을 제공한다.

https://velog.io/@aonee/Python-itertools-%EB%AA%A8%EB%93%88%EC%9D%84-%EC%9D%B4%EC%9A%A9%ED%95%B4-%ED%8E%B8%EB%A6%AC%ED%95%98%EA%B2%8C-%EB%B0%98%EB%B3%B5%EC%9E%90%EB%A5%BC-%EB%A7%8C%EB%93%A4%EC%9E%90

```python
letters = ['a', 'b', 'c', 'd', 'e', 'f']
booleans = [1, 0, 1, 0, 0, 1]
decimals = [0.1, 0.7, 0.4, 0.4, 0.5]

print list(itertools.chain(letters, booleans, decimals))
```

## **5. 디렉토리 경로로 작업 시 `os.path` 모듈 사용**

파일 경로를 다룰 때 복잡한 문자열을 수행하는데, os.path 를 사용하면 명확하고 쉽게 코드를 이해할 수 있다.

🙅‍♀️

```python
from datetime import date
import os
filename_to_archive = 'test.txt'
new_filename = 'test.bak'
target_directory = './archives'
today = date.today()
os.mkdir('./archives/' + str(today))
os.rename(filename_to_archive, target_directory + '/' + str(today) + '/' + new_filename)

```

🙆‍♀️

```python
from datetime import date
import os
current_directory = os.getcwd()
filename_to_archive = 'test.txt'
new_filename = os.path.splitext(filename_to_archive)[0] + '.bak'
target_directory = os.path.join(current_directory, 'archives')
today = date.today()

new_path = os.path.join(target_directory, str(today))
if (os.path.isdir(target_directory)):
  if not os.path.exists(new_path):
    os.mkdir(new_path)
    os.rename(os.path.join(current_directory, filename_to_archive),
    os.path.join(new_path, new_filename))
```

## **4.3 Testing**

#### **1. 자동화된 테스팅 도구 사용하기**

unittest 표준 라이브러리로도 충분하다.

- 자동화된 테스트 검색
- 테스트 활성화 / 비활성화 기능

#### **다른 테스팅도구들**

- nose
- py.test

## **2. 테스트 코드와 앱 코드 분리**

테스트 코드와 동일한 모듈에 테스트 하는 코드를 포함하고 싶어하는데, 의존성을 발생시킨다.

- 테스트 모듈은 명령줄에서 독립적으로 실행할 수 있다
- 테스트 코드를 쉽게 리팩토링할 수 있다
- 테스트 코드는 테스트 하는 코드 보다 덜 자주 수정되어야한다.
- 테스트 전략이 변경되더라도 소스 코드를 변경할 필요가 없다.

#####

#### **3. 리팩토링을 위한 단위 테스트 사용**

코드 리팩토링 - 동작을 변경하지 않고 코드를 재구성 하는 것.

리팩토링 할 때 함수 분리되거나 코드 변경시 단위테스트를 통해 버그를 찾을 수 있다.

단위 테스트는 이러한 목적에 도움이 되는 테스트다. 네트워크 또는 쿼리를 모킹해서 시뮬레이션 함으로 테스트가 실패하는 경우는 코드에 문제가 있다는걸 알 수 있다.

단위테스트를 자동화해서 개발자의 부담을 줄이고 반복성을 높일 수 있다.

### **4. 단위테스트에서 적절한 `assert`메서드 사용하기**

unittest 에는 다양한 assert 메서드가 포함되어있다. 적절하게 사용하면 검사가 명확해진다

🙅‍♀️

```python
class Test(unittest.TestCase):
  def test_adding_positive_ints(self):
    """Does adding together two positive integers work?"""
    self.assertTrue(my_addition(2, 2) == 4)

  def test_increment(self):
    """Does increment return a value greater than what was passed as an argument?"""
    self.assertTrue(increment(1) > 1)

  def test_divisors_of_prime_number(self):
    self.assertTrue(get_divisors(11) is None)

```

🙆‍♀️

```python
class Test(unittest.TestCase):
  def test_adding_positive_ints(self):
    """Does adding together two positive integers work?"""
    self.assertEqual(my_addition(2, 2), 4)

  def test_increment(self):
    """Does increment return a value greater than what was passed as an argument?"""
    self.assertGreaterThan(increment(1), 1)

  def test_divisors_of_prime_number(self):
    self.assertIsNone(get_divisors(11))
```

```python
from functools import lru_cache
@lru_cache()
def list_jobs2(job_queue, job_name):
    filters = [{'name': 'JOB_NAME', 'values': [job_name]}]
    params = {'jobQueue': job_queue, 'filters': filters, 'maxResults': 100}
    response = batch.client().list_jobs(**params)
    jobs = []
    jobs += response.get("jobSummaryList")
    while "nextToken" in response:
        params["nextToken"] = response["nextToken"]
        response = batch.client().list_jobs(**params)
        jobs += response.get("jobSummaryList")
    return jobs
```