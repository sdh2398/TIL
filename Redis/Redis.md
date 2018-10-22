# Redis란

REmote Dictionary Server의 약어인 Redis는 Nosql의 일종으로 key-value 저장소이다.

### Redis의 특징
- Redis는 데이터베이스를 메모리에 보관하고, 지속성을 위해서만 사용한다.
- Redis는 많은 key-value 저장소와 비교하여 풍부한 데이터 타입들을 가지고 있다.
- Redis는 원하는 만큼 복제하여 사용할 수 있다.

### Redis의 장점
- Redis는 1초에 110000의 set, 81000의 get을 수행할 수 있을 정도로 매우 빠르다.
- Redis는 개발자가 이미 알고 있는 list, set, sorted set, hash와 같은 대부분의 자료구조를 지원한다. 개발자들은 어떤 자료구조를 이용하여 어떤 문제를 해결해야 하는지 알기 때문에 다양한 문제를 쉽게 해결할 수 있다.
- 모든 작업은 원자적으로 실행되기 때문에, 두 클라이언트가 동시에 접근해도 Redis서버가 업데이트된 값을 수신하는 것을 보장한다.
- Redis는 다중 유틸리티 도구이며 캐싱, 메시징 큐, 그리고 웹 애플리케이션의 세션, 웹 페이지 방문 횟수와 같은 수명이 짧은 데이터 등 많은 경우에서 사용할 수 있다.

참고
https://www.tutorialspoint.com/redis/redis_overview.htm
