---
layout: post
category: snippet
---

####  CPU 스케쥴링

프로세스는 명령어를 실행하기 위해서 CPU를 사용한다. OS는 수 많은 프로세스들이 한정된 CPU 자원을 효율적으로 사용할 수 있도록 잘 분배하려고 한다. 
이것을 CPU 스케쥴링이라고 한다.

#### 우선순위

자원을 어떤식으로 배분해야할까? 요청된 순서대로 자원을 배분하면 비효율적일 수 있다.

프로세스는 `I/O bounded process`, `CPU Bounded Process`로 나눌 수 있다. 
이 두 유형의 프로세스가 CPU를 필요로하는 시간의 양에는 큰 차이가 있기 때문에 모든 프로세스에게 동일한 빈도로 CPU 사용을 허용하는 것은 비합리적일 수 있습니다. 
따라서 프로세스별로 우선순위를 부여하여 자원을 배분한다.


우선순위는 프로세스 블록인 PCB 블록에 명시를 하고 처리한다.준비상태 또는 대기상태에 요청될 때 우선순위 큐를 사용해 해당 요청들을 정렬한다.

#### 선점 / 비선점

그럼 우선순위가 가장 높은 프로세스가 급히 들어왔을 때 어떻게 해야할까? 지금 사용하는 프로세스를 중단하고 가장 급한 우선순위로 들어온 프로세스를 처리하는 방법이 있고, 
사용하는 프로세스가 끝나면 들어온 프로세스를 처리하는 방법이 있는데 이게 각각 선점형 스케쥴링 / 비선점형 스케쥴링이라고한다.
선점형에서는 급한 우선순위로 프로세스가 들어오다보니 자원을 독점할 수 없다. 
비선점형은 기다려야하니 독점 사용이 가능하다.
선점이 빼앗는것, 비선점이 기다리는 것 장단점은 콘텍스트 스위칭의 오버헤드 정도.