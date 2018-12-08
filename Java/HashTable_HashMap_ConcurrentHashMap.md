# HashTabe vs HashMap vs ConcurrentHashMap
HashTable, HashMap, ConcurrentHashMap 모두 Map 인터페이스를 구현한 콜렉션들이다. 모두 기본적으로 hash알고리즘에 의해 <key, value> 구조를 가지게 되지만 서로 조금씩 다르게 구현되어 있다.

### HashTable
HashTable은 데이터 변경 메소드들에 synchronized 키워드가 선언되어 있다. 즉, 메소드 호출 전 쓰레드간 동기화 락을 통해 멀티 스레드 환경에서 데이터 무결성을 보장해준다. 또한, key, value에 null을 허용하지 않는다.

### HashMap
HashMap은 메소드들에 synchronized 키워드가 없다. 즉, 멀티 스레드에서 여러 스레드가 동시에 객체의 data를 조작하는 경우 data가 깨져버리고 심각한 오류가 발생할 수 있다. 다만, 동기화 락이 매우 느린 동작이기 때문에 HashTable보다 HashMap이 빠르다. 또한, HashTable과는 다르게 key, value에 null을 허용한다.

### ConcurrentHashMap
ConcurrentHashMap은 HashMap을 thread-safe하도록 만든 클래스이다. 하지만, HashMap과는 다르게 key, value에 null을 허용하지 않는다.

참고
https://jdm.kr/blog/197
https://blog.naver.com/PostView.nhn?blogId=soundholick&logNo=220924579873&proxyReferer=https%3A%2F%2Fwww.google.co.kr%2F
http://limkydev.tistory.com/40
