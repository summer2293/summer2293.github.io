---
layout: post
category: Understanding the Digital World
---

# 소프트웨어

하드웨어는 물리적 기계. 빠른 처리를 해준다면,

일종의 뭘 해야하는지를 알려주지 않으면 아무것도 못한다.

명령어를 알려주는 것이 소프트웨어!

#### **알고리즘**

특정 과제를 해결하기 위한 이상적인 절차

## **018. 알고리즘과 초콜릿 케이크 레시피**

#### **알고리즘**

> 결과를 정확하게 계산하도록 보장된 일련의 단계
> 
> 
> 연산의 의미와 수행방법에 의해 의심의 여지가없을정도로 정확한 연산을 해야한다.
> 
> 효율성: 데이터 양에 따라 소요되는 시간
> 

## **019. 반에서 가장 키 큰 사람 찾기**

모든 학생에게 물어봐야 알 수 있다.

#### **조건에 따라 다름**

키 큰 사람이 중복일 경우에는? 한명출력? 여러명출력? 에 따라 달라진다.

#### **자료구조**

> 계산 과정에서 필요한 정보를 표현하는 방법
> 

#### **효율성**

> 주어진 데이터를 처리하는데 시간이 얼마나 걸릴것으로 예상되느냐?
> 
> 
> #### **큰 키는**
> 
> 한번씩 다 물어봐야하니까 양에따라 비례하게 시간이 늘어난다
> 
> #### **= 선형시간 알고리즘**
> 
> 왼쪽부터 오른쪽까지 쭉 찾아보는 알고리즘
> 
> #### **= 이진 알고리즘**
> 
> 다 찾아봐야하는 문제를 대체하기 위해 나온 알고리즘
> 
> 나눠서 보는듯.
> 

## 0**20. 10억 개 전화번호에서 이름 찾기: 이진 검색**

정렬된 값을 중간부터 찾는 방식

절반을 제거해도 되니 크기를 2로 나눠 찾아 가는 방법

#### **divide and conquer**

각 단계마다 남아있는 항복의 절반이 제외하는 전략

> 단계의 수
> 
> 
> 전체 항목의 크기를 계속 나눠 항목 크기가 1에 도달하게 하는 횟수.
> 

## 0**21. 검색을 쉽게 만드는 정렬**

#### **정렬**

> 항목을 순서대로 배열해서 검색이 빨리 실행될 수 있도록 해주는 방법
> 

#### **선택 정렬**

> 계속 선택
> 
> - 리스트에서 최소값을 찾음
> - 그 값을 맨 앞에 위치한 값과 교체
> - 나머지 리스트를 반복

#### **퀵 정렬**

> 반으로 나눔
> 
> 
> #### **1-200 정렬 시**
> 
> 1-5, 6- 10 으로 나눔
> 
> 1-2, 3-5, 6-7, 8-10 으로 나눔
> 
> 1나눔 2나눔 3, 4-5 나눔, 6나눔 7나눔 8, 9-10 나눔
> 
> 1, 2, 3 4나눔, 5나눔,  6나눔, 7나눔, 8, 9나눔, 10나눔
> 
> #### **속도**
> 
> 로그 엔
> 
> 특징
> 
> 같은 두 그룹의 크기를 나눌 수 있도록 중간 데이터 값을 추측해야한다.
> 

## 0**22. 100개 도시를 최단거리로 여행하는 법**

#### **알고리즘 복잡도**

이진검색

log N  - 효율 좋음

선형 검색

N 복잡도. 일의 양이 데이터 양에 정비례

#### **퀵정렬**

N log N (N 보다는 효율이 낮으나, 양이 많아질수록 효과적)

지수 복잡도

#### **엔제곱 비율**

하나의 항복을 추가하면 할일의 양이 두배가 된다.

모든 경우를 하나씩 시도해봐야만 하는 상황에서 발생

바로 푸는 일이 계산상 실행 불가능할 정도의 N을 선택하여 공격을 방지할 수도 있다.

어떤 문제는 처리하기 쉽지만, 다른 문제는 더 어려워보인다.

#### **NP문제**

비결정적 다항. 해결책을 빨리 찾을 수 없지만, 옳게 추측하는 알고리즘이 있다면 NP 문제가 알고리즘에 의해 다항시간 내에 해결할 수 있다

- > 옳은 알고리즘을 사용하면 다항시간 내에 해결이 가능하다.

#### **여행하는 외판원문제**

- 완전탐색
- 문제 중 다수가 서로 동등하다. 한 문제를 해결하는 다항 알고리즘을 찾을 수 있다면, 모든 문제에 대한 다항 시간 알고리즘을 찾아낼 수 있다.

## 0**23. 요약**

#### **얼마나 빨리 계산할 수 있는가? 개념**

알고리즘, 복잡도를 잘 포착하는데 관심을 둔다.

알고리즘 복잡도 연구는 컴퓨터 과학의 주요 영역으로, 이론 실제 적용 모두 중요한 연구 대상이다.

암호기법.

목표 수신자만 읽을 수 있도록 비밀 메세지를 보내는 기술은 알고리즘에 크게 의존한다.

## **024. 알고리즘은 이상, 프로그래밍은 현실**

#### **알고리즘**

> 추상적이고 이상적인 절차.
> 
> 
> 구체적이고 명시된 기본 연산을 사용하여 모든 가능한 상황을 다룬다.
> 

#### **프로그램**

> 실제로 컴퓨터가 작업을 수행해야하는 단계를 기술한 것. 프로그램 내부에 알고리즘이 처리하는 형태로 들어간다.
> 
> 
> 프로그램은
> 
> - 메모리
> - cpu 속도
> - 유효성 데이터
> - 하드웨어 결함
> - 네트워크 연결 불량
> - 인간적인 문제
> 
> 를 고려해서 작성해야 한다.
> 

## **025. 다른 프로그램을 처리하기 위한 프로그램**

프로그래밍의 초창기 어려움

- 명령어와 데이터를 이진수로 변환
- 천공카드로 기계가 판독할 수 있게함
- 메모리 적재

해당 반복작업을 처리하기 위해, 프로그램을 위한 프로그램을 만든게 어셈블러!

#### **어셈블러**

- 명령에 의미 있는 단어를 붙힌다 (5 -> ADD)
- 특정 메모리 위치를 나타내는 이름을 사용한다 (14 -> SUM)

프로그램을 작성하면, 어셈블러가 명령어와 데이터 값이 메모리상 어떤 위치에 있을지 파악해준다.

어셈블러의 경우 아키텍처에 특화된 언어기 때문에, 호환이 안된다.

특정 프로세서 용 언어 프로그램을 다른 프로세서 용으로 변환하고 싶다면 프로그램을 완전히 새로 작성해야한다.

## **026. 고수준 언어에서 프로그래밍 실행까지**

고수준 프로그래밍 언어가 개발됨!

#### **컴파일러가 추가됨**

전단부:

컴파일러가 어셈블러로 변경

후단부:

어셈블러를 바이너리로 변경

### **컴파일단계**

- 에러 점검 가능

#### **언어소개**

#### **포트란 (Fomula Tranlation)**

#### **코볼**

#### **베이직**

## **27. 작문과 비슷한 프로그래밍**

코볼, 베이직 -> 해석을 위한 도구

#### **대규모 시스템 프로그래밍을 위한 언어의 탄생**

> c, c++
> 

#### **WWW 의 등장**

> Java
> 

#### **가독성을 위한 프로그래밍 언어 등장**

> Python
> 

## **28. 구글 같은 서비스는 어떻게 개발할까?**

#### **라이브러리, 인터페이스, 개발 키트**

하나부터 짜지 않고 다른 사람들이 짠 코드를 갖다 쓴다.

#### **SDK (software development kit)**

개발할 수 있는 환경을 제공해준다

#### **버그**

프로그래밍을 하다보면 발생하는 오류. 어디에든 있다 안보일 뿐

#### **테스트**

버그를 잡기위한 테스트 코드

## **029. 구글과 오라클의 저작권 소송**

#### **지적재산권**

발명, 저작같은 개인의 창작 활동으로 생겨난 무형 자산

소프트웨어도 지적 재산권이다.

#### **소프트웨어에서 지적 재산권을 보호하는 매커니즘**

> 영업 비밀상표저작권특허라이선스
> 

#### **영업 비밀**

> 기밀 유지 협약서 같은 계약으로 계약에 의해서만 다른이에게 공개됨 코카콜라
> 

#### **상표**

> 회사의 서비스를 구별해주는 단어, 문구, 이름, 로고 등 특정한 색상
> 

#### **저작권**

> 창작 표현물을 보호한다.제한된 기간에 걸쳐 작품을 활용하고 수익을 얻을 권리를 준다.
> 
> 
> #### **디지털 자료의 저작권 (DRM)**
> 
> - 내가 작성한 프로그램은 내 소유이다.
> 
> #### **클린 룸 개발 기법**
> 
> #### **특허**
> 
> - 발명에 대한 법적 보호를 제공한다.
> 
> 소프트웨어는 `수학` 카테고리여서, 특허를 받을 수 없었다.
> 

#### **아마존의 원 클릭 특허**

이 클릭으로 라이선스를 챙긴다.

#### **특허 관리 전문 사업자 증가**

#### **라이선스**

- 제품을 사용할 권한을 승인하는 합의.

#### **API의 저작권 문제**

오라클이 자바를 인수하면서 구글에 고소.

## **030. 기술 표준의 중요성**

#### **표준**

상호 운용성을 보장하고 공개 경쟁이 이루어지도록 하는 데 결정적인 요소.

어떻게 만들어지고 작동되는 것일까?

를 상세하게 기술한 것.

#### **하드웨어의 표준 혜택**

플러그 사용 -> 전압 표준

TV 신호 -> 방송, 케이블 표준

#### **소프트웨어 표준**

- 아스키코드
- 유니코드
- 프로그래밍 언어
- 암호화와 압축 알고리즘
- 프로토콜

## **031. 자유로운 소프트웨어, 오픈소스**

#### **소스코드**

프로그래머가 작성하는 코드

#### **오브젝트 코드**

컴파일 한 결과

### **오픈소스**

연구와 개선 활동을 위해 다른사람들도 소스코드를 자유롭게 사용할 수 있도록 하는 대안.

### **GNU Project(Gnu's Not Unix)**

운영체제와 프로그래밍 언어용 컴파일러 같은 중요한 소프트웨어 시스템의 무료 공개 버전을 만드는 일

- 모든 버전을 공유하고 변경할 수 있는 자유를 보장하는 의도

돈은 어떻게?

- 기술지원
- 교육
- 품질보증
- 시스템 통합
- 기타 서비스 이용

## **032. 요약**

프로그래밍 언어는 하드웨어 자원을 활용하도록 진화되어 왔다. 고수준 언어가 되면서, 메모리 사용을 자동으로 관리하는 메커니즘을 제공한다.

### **프로그래밍 언어**

> 컴퓨터에게 무엇을 해야 할지 알려줄 때 쓰는 언어.
> 

### **여러 프로그래밍 언어가 있는 이유**

> 각자 특성에 맞는 프로그램이 있다.
> 

## **033. 컴퓨터를 작동하게 하는 운영체제**

### **운영체제**

하드웨어를 관리하고, 다른 프로그램을 실행하게 해주는 것. 모든 컴퓨터는 운영체제를 가지고 있다.

### **프로그램**

애플리케이션. 우리가 사용하는 프로그램들

### **역사**

1950

프로그램 = 운영체제 였다. 왜냐하면 성능이 제한적이어서 한 컴퓨터에 하나의 프로그램만 띄울 수 밖에 없었음

컴퓨터가 발전하면서 하드웨어 성능이 좋아지다보니, 운영체제를 통해 여러 프로그램을 관리할 수 있었다.

- 유닉스 운영체제
- 리눅스 운영체제

컴퓨터 구조

- 프로세서(CPU)
- 메모리
- 디스크
- 디스플레이
- 입출력
- 네트워크 인터페이스

로 이루어져있는데, 이 요소들을 효과적으로 동시에 사용할 수 있도록 해주는게 운영 체제이다.

- 입출력 대기
- 동시 출력

### **역할**

1. 자원 제어 및 할당
2. 주기억 장치 관리
    
    가상 메모리
    
    메모리를 일부만 가져와 실행하고, 비활성화가 되면 디스크로 옮기는 스와핑 작업을 진행함. 프로그램은 이걸 모르고, 배후에서 메모리 주소를 실제 메모리상에 진짜 주소로 변환하는 것
    
3. 보조 기억장치에 저장된 정보를 관리
    1. 파일시스템 구조가 계층 구조를 제공한다.
4. 컴퓨터에 연결된 장치를 관리, 조종

## **034. 가상 운영 체제와 가상 머신**

운영체제 = 프로그램

최초 = 1개의 프로그램만 실행이 되었다. 갈수록 발전.

### **운영체제 위에 운영체제**

하드웨어 개발 시에 운영체제 위에 다른 운영체제를 실행하기도 한다

운영체제를 프로그램처럼 띄움

### **부트캠프**

맥 os 위에 window를 실행 시키는 것

### **가상 운영체제**

virtual operating system

- Vmware, virtual box, xen

### **가상 머신**

- 하드웨어인 척 하는 소프트웨어 . 컴퓨터 처럼 작동하는 소프트웨어
- 브라우저에서 자바 컴파일러

하드웨어를 만들어서 출하하는 것 보다, 소프트웨어로 하는게 편해서이다.

### **클라우드 컴퓨팅**

가상머신. 물리적인 컴퓨터를 대량 보유하면서, 해당 자원을 이용해 고객에게 컴퓨팅 성능을 제공한다. 고객은 몇개의 가상 머신을 사용하는데, 컴퓨팅의 수는 훨신 더 적게 지원받는다.

## 035. 운영체제가 일하는 법

부팅

- 컴퓨터가 켜질 때 ROM 에 저장된 명령어를 실행해 작동을 시작
- 유용한 작업을 할 때 까지 명령어를 읽는 과정

부팅 과정

- 컴퓨터와 연결된 외부 장치 확인
- 관련 드라이버 로드

프로그램은 운영체제에 짧은 시간 조각을 할당받는데, 시스템 서비스를 요청하거나 프로그램에 할당된 시간이 다 되면 끝난다.

#### 시스템 콜

운영체제는 H/W S/W 간 인터페이스를 제공한다.

운영체제는 애플리케이션이 구축될 수 있는 ‘플랫폼’ 을 제공한다.

운영체제는 애플리케이션에 제공하는 작업이나, 서비스 집합을 정의한다.

이 서비스 집합을 합의된 방식으로 이용하게 해준다.

운영체제에 서비스가 진입할 수 있는 진입점을 시스템 콜이라고 한다.

#### 디스크 드라이버

드라이버

- 특정 장치가 어떤 일을 하도록 하는 방법

다양한 디지털 장치와 운영체제

- 범용 운영체제
    - 록립
- 기술발달로 별도의 운영체제보다 범용적인 운영체제를 사용하는 방식이 타당하다.

## 036. 파일 시스템과 블록

파일시스템

- 물리적 저장 매체를 폴더의 계층 구조처럼 보이게 하는 부분
- 여러 장치에 정보를 동일한 인터페이스로 보여준다.

폴더, 디렉토리

- 조직화 된 구조를 제공하는 파일

파일

- 문서, 사진, 음악 등 실질적인 데이터

- 파일시스템은 파일의 정보를 관리하며, 앱, 운영체제가 정보를 읽고 쓸 수 있도록 접근을 가능하게 만든다.
- 파일에 대한 접근이 서로 간섭하지 않게 조정한다. (이메일의 일부가 스프레드 시트에 나오지 않게)

보조 기억 장치 파일 시스템

- 1블록이 1kb
- 한 파일에서 사용하는 블럭을 다른 파일의 데이터를 넣지 않는다.

폴더 엔트리

- 파일의 크기, 블록 주소를 담고 있다.

웨어라벨링

- 블록이 같은 횟수로 사용되도록 데이터를 이동시키는 처리

## 037. 파일을 휴지통에 넣을 때 일어나는 일

**파일 제거하기**

- 파일을 제거하면 휴지통으로 파일이 복사된다
    - 파일 엔트리가 휴지통에 복사되고 이동함
- 휴지통 비우기를 누르면 폴더 엔트리가 지워지고 블록은 미사용 목록에 추가된다.
    - 하지만 내용은 삭제가 되지 않는다. 새로운 파일에 할당되기 전까지는 새로운 내용으로 덮어써지지 않는다.
- 이점: 디스크에 뭔가 이상이 되어 시스템이 엉망이 되었을 때도 정보 복원이 가능하다.
- 블록을 0과 1 값을 여러번 덮어 씌움으로 파일을 제거해야한다.
- 하드디스크를 자석 근처에 놓아 자성을 없앤다.
- 폴더 엔트리도 이전 블록의 내용을 복원 가능하다.

네트워크 파일 시스템

- 소프트웨어를 활용하여 다른 컴퓨터에 있는 파일시스템을 접근하게 해준다.
- 인터페이스를 제공
- 

## 038. 여러 작업을 수행하는 애플리케이션

애플리케이션

- 운영체제를 플랫폼으로 작업을 수행하는 프로그램이나 소프트웨어 시스템

시스템 콜

---

브라우저는 웹 서버에 요청을 보내고, 화면에 표시할 정보를 웹 서버에 받아온다.

- 비동기적 이벤트 처리
    - 링크 클릭 시, 페이지를 스크롤 하면 즉각 반응해야한다

## 039. 소프트웨어 계층 구조

- 하드웨어가 밑바닥
- 운영체제. 핵심부분이어서 커널이라고함.
    - 커널
        - 하드웨어의 특수한 속성을 숨기고, 특정 하드웨어의 여러가지 세부사항과 독립된 인터페이스 또는 외관을 제외한다.
        - 인터페이스가 잘 설계되어 있으면, 동일한 운영체제 인터페이스를 다양한 운영체제에 사용할 수 있다.
- 라이브러리
    - 프로그래머가 사용할 수 있는 API 를 제공한다.
- 커널, 라이브러리, 애플리케이션이 명확하지 않다.
    - 경계선 지침
        - 애플리케이션이 다른 애플리케이션 동작에 간섭하지 않도록 하는데 필요한 것은 운영체제가 하는 일

## 040. 요약

- 애플리케이션은 사용자가 원하는 작업을 처리한다
- 운영체제는 애플리케이션이 자원을 효율적으로 관리할 수 있도록 조정한다.