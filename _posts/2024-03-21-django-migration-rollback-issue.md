---
layout: post
category: snippet
---

배포 후 마이그이션 이슈가 발생했다

*migration?*

ORM 맵핑을 사용하는 django 에서 모델의 변경내역을 Table에 전달하는 방법으로 관련 명령어들을 통해 모델 값의 변경을 기록한 migration 파일을 만들어주고, 그 변경사항을 테이블에 적용하는 `migrate` 명령어를 사용하여 테이블을 객체처럼 사용할 수 있게 작업한다.

이때 기록은 `django_migration` 이라는 테이블에 저장되어 어디까지 변경되었는지 기록한다.

```python
# migration 파일 생성
python3 [manage.py](http://manage.py) makemigration 

# 어디까지 migration이 기록되었는지 확인
python3 [manage.py](http://manage.py) model_name showmigration 

# migration 파일을 0번으로 되돌린다.
python3 [manage.py](http://manage.py) 0000 migrate  
```
### Situation

배포 후 에러가 발생했다. 이전 배포로 롤백하였으나, 마이그레이션 파일이 롤백되지 않는 문제가 발생했다. (이전 배포로 진행하면 파일이 롤백될 줄 알았다.)

이 때 같이 하는 팀원분이 새로 생성된 필드를 psql 로 들어가 직접 drop 했고 여러가지 이슈들이 발생했는데, 그 중 궁금했던 부분들을 톺아보았다.

### Result

결론부터 말하자면, django의 경우 `migration` 를 적용하면, `django_migration` 파일에 기록을 한다. 마지막이 최신 버전으로 보인다. 마이그레이션 작업을 롤백하여 이전 마이그레이션으로 변경하면, 해당 `django_migration` 에도 그 기록이 삭제된다.

drop 을 하더라고 django_migration 에 기록이 되어있어 이후 다시 최신 버전으로 마이그레이션하더라도 django_migration 테이블엔 기록이 남아있어 안되는 상황이었다.

### Action

**체크해야할 상황**

- 이전 배포로 돌리면 마이그레이션이 롤백 되는지 여부?
- 배포 후 파이프라인에서 마이그레이션이 잘 진행되었는지 여부
- 이전 배포에서 sql 문으로 직접 드랍 후 다시 최신 버전으로 배포했을 때 마이그레이션이 적용 여부

**이전 배포로 돌리면 마이그레이션이 롤백되는지 여부**

롤백되지 않는다. 배포 코드 자체에 롤백하는 코드가 제공되지 않아서 롤백이 안된다 (있는줄..) 그리고 수정, 생성 같은 필드들은 `migrate` 명령어로 쉽게 롤백이 된다고 한다. 이전 버전으로 롤백할 때 추가된 마이그레이션 파일이 존재한다면,  `python3 [manage.py](<http://manage.py>) migrate` 코드를 통해 롤백을 하고 이전 배포로 갔었어야 했다. 이게 놓친 부분. 

**현재상황**

33번까지 되어있는 상황

```
 [X] 0030_
 [X] 0031_
 [X] 0032_
 [X] 0033_
```

**과거 버전으로 배포**

`showmigration` 으로 확인해보니 30번으로 롤백이 되어있었다

```
 [X] 0028_
 [X] 0029_
 [X] 0030_
```

**DB table 확인**

showmigration만 보면 잘 롤백이 되었구나! 를 알 수 있지만 실제로 `django_migration` 테이블을 보면 최신버전에서 추가된 `new_field` 이 그대로 존재하고 있었다. 

`new_field | character varying(31)|| not null |`

---

**이전 버전에서 Drop 후, 최신 버전으로 배포할 때 마이그레이션 파일이 생성되는가?**

이전 버전인 상황에서 컬럼 드랍

drop `ALTER TABLE _ DROP COLUMN new_field;`

```
Column|Type| Collation | Nullable |Default
--------
 id| integer|| not null
```

삭제된것을 확인 후 최신 버전으로 배포해보았다.

```
 [X] 0030_
 [X] 0031_
 [X] 0032_
 [X] 0033_
```

31,32,33 이 마이그레이션이 되었지만, DB 테이블을 확인해보니

31에서 추가된 `new_field` 가 생성되지 않음을 확인할 수 있었다.

```
Column|Type| Collation | Nullable |Default
-------------------------------+--------------------------+-----------+--
 id| integer|| not null

```

migration 명령어로 30_ 으로 롤백해볼까 했지만, 실패했다.

```
django.db.utils.ProgrammingError: 
column "new_field" of relation "table" does not exist
```

`django_migration` 에서 필드를 확인해보니, 이 파일에는 32,33 기록 없었다.

```
SELECT app, name, applied FROM django_migrations ORDER BY applied DESC;
app|name|applied
-------------------------------------------------------------
 -        | 0031_       | 2024-03-19 07:02:49.831565+00
 -        | 0030_

```

이전 배포에서 삭제한 `new_field` 의 `django_migrations` 기록은 지우지 않아 31이 기록된 상황으로 보인다. 하지만 31에서 추가한 new_field 를 32, 33에서  만들려고 하니 관련 필드가 없으니 에러가 나서 32,33 은 만들수 없던것으로 보인다.

그래서 다시 이전 버전으로 다시 들어가 해당 컬럼을 삭제하고 이전버전으로 다시 배포하였다.

**이전버전 배포**

```
 [X] 0029_
 [X] 0030_
```

이전 버전에서 마이그레이션 삭제

```
...
 463 | _| 0030_| 2023-04-07 08:45:32.752722+00
```

다시 최신 버전 배포

서버 200 확인이 되었다. 잘 마이그레이션이 된것으로 보인다.

```
 [X] 0029_
 [X] 0030_
 [X] 0031_
 [X] 0032_
 [X] 0033_
```

**django_migrations**

```
...
 463 | table| 0030_| 2023-04-07 08:45:32.752722+00
 499 | table| 0031_| 2024-03-28 04:34:43.430881+00
 500 | table| 0032_| 2024-03-28 04:34:43.444747+00
 501 | table| 0033_| 2024-03-28 04:34:43.45712+00

```

인스턴스 들어가서 롤백하면

```

 [X] 0030_
 [ ] 0031_
 [ ] 0032_
 [ ] 0033_

```

마이그레이션 코드로 배포하고, 이전 배포로 돌아가려면 롤백 하고 돌아가야한다. 

왠지 우리도 drop 이 아닌 저 코드를 직접 추가했어야 했을 듯 하다.

코드를 롤백할 필요가 있을 경우 롤백전에 마이그레이션을 하는걸 챙겨야한다.