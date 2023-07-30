# 2023-system-design-interview

**_가상 면접 사례로 배우는 대규모 시스템 설계 기초_**

![cover](images/book-cover.jpeg)

<br/>

### 목차

-   옮긴이의 글
-   지은이의 글

**1장 사용자 수에 따른 규모 확장성**

-   단일 서버
-   [데이터베이스](01장%20사용자%20수에%20따른%20규모%20확장성/데이터베이스.md)

    -   (p. 4, SM) WAS와 DB를 분리하지 않는 방식이 그냥 단일 EC2 서버 내에 데이터베이스 설치하는 방식이고, 도커를 사용하거나 RDS 사용하는 방식이 데이터베이스를 따로 분리해내는 방식이 맞나?
    -   (p. 9, SM) 주 데이터베이스 서버가 다운되는 경우, 부서버에 보관된 데이터를 최신 상태로 맞추기 위해 복구 스크립트를 돌리는 과정이 Mysql의 mysqldump, Redis AOF와 같은 데이터 복구 기능과 연관이 있는가?

-   [수직적 규모 확장 vs 수평적 규모 확장](01장%20사용자%20수에%20따른%20규모%20확장성/수직적%20규모%20확장%20vs%20수평적%20규모%20확장.md)

    -   (p. 5, GC) NoSQL이 아주 낮은 응답 지연시간(latency)을 보장하는 이유?
    -   (p. 5, GC) 아주 많은 양의 데이터를 저장할 때, NoSQL이 SQL보다 더 나은 이유?
        -   (+SM) 비관계형 DB를 사용하면 좋은 경우 중 하나가 아주 많은 양의 데이터를 저장할 필요가 없는 경우인데, 경우에 따라 관계형 DB는 대용량의 데이터를 스키마 형태로 저장하는 것에 많은 시간이 소요됨, 둘의 저장 구조 기법에서 시간 차이가 많이 나는 것 같은데 왜인지?
    -   (p. 5, SM) "데이터를 직렬화하거나 역직렬화 할 수 있기만 하면됨" 이라면 SQL에서는 그밖의 과정이 더 필요한 것인지?

-   [캐시](01장%20사용자%20수에%20따른%20규모%20확장성/캐시.md)

    -   (p. 12, SM) SPOF를 피하려면 여러 지역에 걸쳐 캐시 서버를 분산시켜야 한다 하는데, Redis의 경우 master-slave 구조로 클러스터링하여 SPOF 을 피할 수 있는가?

-   콘텐츠 전송 네트워크(CDN)
-   무상태(stateless) 웹 계층
-   데이터 센터
-   [메시지 큐](01장%20사용자%20수에%20따른%20규모%20확장성/메시지%20큐.md)
    -   (p. 23, SM) 메시지 큐의 크기가 커지면 더 많은 작업 프로세스를 추가해야 처리 시간을 줄일 수 있다는게 무슨 의미인가?
    -   (p. 23, SM) 메시지 큐를 사용하면 왜 결합이 느슨해져 규모 확장성이 보장되어야 하는 어플리케이션을 구성하기에 좋을까?
-   로그, 메트릭 그리고 자동화
-   데이터베이스의 규모 확장
-   백만 사용자, 그리고 그 이상
-   참고문헌

**2장 개략적인 규모 추정**

-   2의 제곱수
-   모든 프로그래머가 알아야하는 응답지연 값
-   가용성에 관계된 수치들
-   예제: 트위터 QPS와 저장소 요구량 추정
-   팁
-   참고문헌

**3장 시스템 설계 면접 공략법**

-   효과적 면접을 위한 4단계 접근법

**4장 처리율 제한 장치의 설계**

-   1단계 문제 이해 및 설계 범위 확정
-   [2단계 개략적 설계안 제시 및 동의 구하기](04장%20처리율%20제한%20장치의%20설계/2단계%20개략적%20설계안%20제시%20및%20동의%20구하기.md)
    -   (p. 59, SM) 갑작스런 트래픽 급증에 토큰 버킷 알고리즘이 적합한 이유?
-   [3단계 상세 설계](04장%20처리율%20제한%20장치의%20설계/3단계%20상세%20설계.md)
    -   (p. 69, GC) 처리율 제한 장치를 미들웨어로 뒀을 때, 미들웨어가 SPOF가 되지 않을까?
    -   (p. 71, SM) Redis Sorted Set이 어떻게 락(Lock)의 경쟁 조건 이슈 해결 기능을 대체할 수 있는가?
    -   (p. 71, GC) 작업 프로세스에서 규칙을 캐시 서버에 저장해두고 처리율 제한 미들웨어가 해당 캐시를 읽어서 처리를 한다. 이때, 만약 캐시가 오염되어있다면 어떻게 하는가?
    -   (p. 72, GC) 처리율 제한 장치를 다중화 했을 때, 한 장치가 죽었다면 Failover는 어떻게 할 수 있을까?
    -   (p. 72, GC) 분산 데이터 저장소가 중앙 집중형 데이터 저장소보다 좋은 점은 없을까?
-   4단계 마무리
-   참고문헌

**5장 안정 해시 설계**

-   해시 키 재배치(rehash) 문제
-   안정 해시
-   마치며
-   참고문헌

**6장 키-값 저장소 설계**

-   문제 이해 및 설계 범위 확정
-   단일 서버 키-값 저장소
-   [분산 키-값 저장소](06장%20키-값%20저장소%20설계/분산%20키-값%20저장소.md)
    -   (p. 100, SM) 키-값 저장소의 강한 일관성이 보장되려면, N=3 / W=R=2가 아니라 W=R=3이어야 하지 않나?
    -   (p. 100, SM) 일관성 모델과 관련하여, AWS S3은 최종 일관성에서 강한 일관성을 제공하도록 변경되었는데, DynamoDB 는 여전히 기본값이 최종 일관성인 이유?
    -   (p. 114, SM) 버저닝 및 벡터 시계를 사용한 충돌 해소는 높은 일관성을 위한 해결 방법인데, 왜 쓰기 연산에 대한 높은 가용성을 보장한다 하는가?
-   요약
-   참고문헌

**7장 분산 시스템을 위한 유일 ID 생성기 설계**

-   1단계 문제 이해 및 설계 범위 확정
-   2단계 개략적 설계안 제시 및 동의 구하기
-   3단계 상세 설계
-   4단계 마무리
-   참고문헌

**8장 URL 단축기 설계**

-   1단계 문제 이해 및 설계 범위 확정
-   2단계 개략적 설계안 제시 및 동의 구하기
-   3단계 상세 설계
-   [4단계 마무리](08장%20URL%20단축기%20설계/4단계%20마무리.md)
    -   (p. 138, SM) 많은 트래픽의 URL 단축 요청이 들어왔을때 이미 웹 서버와 DB도 여러대 두고 있는데, 어느 부분에서 잠재적인 "보안" 결함을 가지고 있다는 것인가?
-   참고문헌

**9장 웹 크롤러 설계**

-   1단계 문제 이해 및 설계 범위 확정
-   2단계 개략적 설계안 제시 및 동의 구하기
-   3단계 상세 설계
-   4단계 마무리
-   참고문헌

**10장 알림 시스템 설계**

-   1단계 문제 이해 및 설계 범위 확정
-   2단계 개략적 설계안 제시 및 동의 구하기
-   [3단계 상세 설계](10장%20알림%20시스템%20설계/3단계%20상세%20설계.md)
    -   (p. 172, GC) 일반적으로 알림을 구현할 때 Redis를 사용하는 이유?
    -   (p. 174, GC) 알림 서버를 다중화했고 각 3자 서비스 각각에 요청을 보내는 것이므로 메시지 큐 도입하지 않아도 장애 전파가 안 일어나지 않을까?
    -   (p. 176, SM) 분산 시스템 특성상 왜 알림의 중복 전송이 일어나게 되는가?
-   4단계 마무리
-   참고문헌

**11장 뉴스 피드 시스템 설계**

-   1단계 문제 이해 및 설계 범위 확정
-   2단계 개략적 설계안 제시 및 동의 구하기
-   [3단계 상세 설계](11장%20뉴스%20피드%20시스템%20설계/3단계%20상세%20설계.md)
    -   (p. 192, SM) 포스트ID 관계가 캐시에만 저장이 되는건데, 메모리는 휘발성이므로 안전하지 않은데 이렇게 한 이유?
    -   (p. 194, GC) 횟수 값을 디비에 갖고있지 않고 캐시에만 저장한다는 것이 올바른가?
    -   Appendix : Kubernetes 운영을 위한 etcd 기본 동작 원리의 이해
-   4단계 마무리
-   참고문헌

**12장 채팅 시스템 설계**

-   1단계 문제 이해 및 설계 범위 확정
-   2단계 개략적 설계안 제시 및 동의 구하기
-   [3단계 상세 설계](12장%20채팅%20시스템%20설계/3단계%20상세%20설계.md)
    -   (p. 215, SM) 채팅방 인원이 많아지면, 사용자 별로가 아닌 채팅방 별로 큐를 생성하는게 좋은가?
-   4단계 마무리
-   참고문헌

**13장 검색어 자동완성 시스템**

-   1단계 문제 이해 및 설계 범위 확정
-   2단계 개략적 설계안 제시 및 동의 구하기
-   3단계 상세 설계
-   4단계 마무리
-   참고문헌

**14장 유튜브 설계**

-   1단계 문제 이해 및 설계 범위 확정
-   2단계 개략적 설계안 제시 및 동의 구하기
-   3단계 상세 설계
-   4단계 마무리
-   참고문헌

**15장 구글 드라이브 설계**

-   1단계 문제 이해 및 설계 범위 확정
-   2단계 개략적 설계안 제시 및 동의 구하기
-   3단계 상세 설계
-   4단계 마무리
-   참고문헌

**16장 배움은 계속된다**

-   실세계 시스템들
-   회사별 엔지니어링 블로그
