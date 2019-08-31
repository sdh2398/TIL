# Java HashMap

HashMap은 JCF(Java Collections Framework)에 속한 구현체 클래스다.
* Map 인터페이스 자체는 Java 5에서 Generic이 적용된 것 외에 처음 선보인 이후 변화가 없지만, HashMap 구현체는 성능을 향상시키기 위해 지속적으로 변화해 왔다.

### HashMap과 HashTable
HashTable
* JDK 1.0부터 있던 Java의 API

HashMap
* Java 2에서 처음 선보인 JCF에 속한 API

둘 다 제공하는 기능은 같지만 HashMap은 보조 해시 함수를 사용하기 때문에 보조 해시 함수를 사용하지 않는 HashTable에 비하여 해시 충돌이 덜 발생할 수 있어 성능상 이점이 있다.

HashMap과 HashTable의 정의
* 키에 대한 해시 값을 사용하여 값을 저장하고 조회하며, 키-값 쌍의 개수에 따라 동적으로 크기가 증가하는 associate array라고 할 수 있다.
* 이 associate array를 지칭하는 다른 용어가 있는데, 대표적으로 Map, Dictionary, Symbol Table 등이다.

### 해시 분포와 해시 충돌
동일하지 않은 어떤 객체 X와 Y가 있을 때 X.eqauls(Y)가 거짓이고 X.hashCode() != Y.hashCode()이면, 이 때 사용하는 해시 함수는 완전한 해시 함수다.

Boolean이나, Integer, Long, Double 같은 Number 객체가 나타내려는 값 자체는 해시 값으로 사용할 수 있기 때문에 완전한 해시 함수 대상으로 삼을 수 있다.
* 하지만 String이나 POJO(plain old java object)에 대하여 완전한 해시 함수를 제작하는 것은 사실상 불가능하다.

적은 연산만으로 빠르게 동작하는 완전한 해시 함수가 있다고 하더라도, 그것을 HashMap에서 사용할 수 있는 것은 아니다.
* HashMap은 기본적으로 각 객체의 hashCode() 메서드가 반환하는 값을 사용하는데, 결과 자료형은 int다. 32비트 정수 자료형으로는 완전한 자료 해시 함수를 만들 수 없다.
* 논리적으로 생성 가능한 객체의 수가 2^32보다 많을 수 있고, 모든 HashMap 객체에서 O(1)을 보장하기 위해 랜덤 접근이 가능하려면 2^32인 배열을 모든 HashMap이 가지고 있어야 한다.

따라서 HashMap을 비롯한 많은 해시 함수를 이용하는 associative array 구현체에서는 메모리를 절약하기 위하여 실제 범위보다 작은 M개의 원소가 있는 배열만 사용한다.
* 따라서 해시 코드의 나머지 값을 해시 버킷 인덱스 값으로 사용한다.
* int index = X.hashCode() % M;

이 방식을 사용하면 서로 다른 해시 코드를 가지는 객체가 1/M 확률로 같은 해시 버킷을 사용하게 된다.
* 이는 해시 함수가 얼마나 해시 충돌을 회피하도록 잘 구현되었느냐에 상관없이 발생할 수 있는 또 다른 종류의 해시 충돌이다.
* 이렇게 해시 충돌이 발생하더라도 키-값 쌍 데이터를 잘 저장하고 조회할 수 있게 하는 방식에는 대표적으로 두 가지가 있다.
    * Open Addressing
    * Separate Chaining

Open Addressing
* 데이터를 삽입하려는 해시 버킷이 이미 사용 중인 경우 다른 해시 버킷에 해당 데이터를 삽입하는 방식
* 데이터를 저장/조회할 해시 버킷을 찾을 때에는 Linear Probing, Quadratic Probing등의 방법을 사용

Separate Chaining
* 각 배열의 인자는 인덱스가 같은 해시 버킷을 연결한 링크드 리스트의 첫 부분(head)이다.

둘 모두 Worst Case O(M)이다.
* 하지만 Open Addressing은 연속된 공간에 데이터를 저장하기 때문에 Separate Chaining에 비하여 캐시 효율이 높다.
* 따라서 데이터 개수가 충분히 적다면 Open Addressing이 Separate Chaining보다 성능이 더 좋다.
* 하지만 배열의 크기가 커질수록(M이 커질수록) 캐시 효율이라는 Open Addressing의 장점은 사라진다.
    * 배열의 크기가 커지면, L1, L2 캐시 적중률(hit ratio)이 낮아지기 때문

Java HashMap에서 사용하는 방식은 Separate Chaining이다.
* Open Addressing은 데이터를 삭제할 때 처리가 효율적이기 어려운데, remove() 메서드는 매우 빈번하게 호출될 수 있기 때문
* 게다가 HashMap에 저장된 키-값 쌍 개수가 일정 개수 이상으로 많아지면, 일반적으로 Open Addressing은 Separate Chaining보다 느리다.
* Open Addressing의 경우 해시 버킷을 채운 밀도가 높아질수록 Worst Case 발생 빈도가 더 높아지기 때문
* 반면 Separate Chaining 방식의 경우 해시 충돌이 잘 발생하지 않도록 '조정'할 수 있다면 Worst Case 또는 Worst Case에 가까운 일이 발생하는 것을 줄일 수 있다.

### Java 8 HashMap에서의 Separate Chaining
Java 2부터 7까지의 HashMap에서 Separate Chaining 구현 코드는 조금씩 다르지만, 구현 알고리즘 자체는 같았다.
* 만약 객체의 해시 함수 값이 균등 분포상태라고 할 때, get()메서드 호출에 대한 기댓값은 E(N/M)이다.
* 그러나 Java 8에서는 이보다 더 나은 E(log(N/M))을 보장한다.
* 데이터 개수가 많아지면, Separate Chaining에서 링크드 리스트 대신 트리를 사용하기 때문이다.
* 데이터의 개수가 많아지면 이 차이는 무시할수 없다.
* 게다가 실제 해시 값은 균등 분포가 아닐뿐더러, 설사 균등 분포를 따른다고 하더라도 birthday problem이 설명하듯 일부 해시 버킷 몇 개에 데이터가 집중될 수 있다. 그래서 데이터의 개수가 일정 이상일 때에는 링크드 리스트 대신 트리를 사용하는 것이 성능상 이점이 있다.

링크드 리스트와 트리를 사용하는 기준은 하나의 해시 버킷에 할당된 키-값 쌍의 개수이다. Java 8 HashMap에서는 상수 형태로 기준을 정하고 있다.
* 하나의 해시 버킷에 8개의 키-값 쌍이 모이면 링크드 리스트를 트리로 변경한다.
* 만약 해당 버킷에 있는 데이터를 삭제하여 개수가 6개에 이르면 다시 링크드 리스트로 변경한다.
* 트리는 링크드 리스트보다 메모리 사용량이 많고, 데이터의 개수가 적을 때 트리와 링크드 리스트의 Worst Case 수행 시간 차이 비교는 의미가 없기 때문이다.
* 8과 6으로 2 이상의 차이를 둔 것은, 만약 차이가 1이라면 어떤 한 키-값 쌍이 반복되어 삽입/삭제 되는 경우 트리와 링크드 리스트를 불필요하게 변경하는 일이 되어 성능 저하가 발생할 수 있기 때문이다.

``` java
static final int TREEIFY_THRESHOLD = 8;

static final int UNTREEIFY_THRESHOLD = 6;
```

Java 8 HashMap에서는 Entry 클래스 대신 Node 클래스를 사용한다.
* Node 클래스 자체는 사실상 Java 7의 Entry 클래스와 내용이 같지만, 링크드 리스트 대신 트리를 사용할 수 있도록 하위 클래스인 TreeNode가 있다는 것이 Java 7 HashMap과 다르다.

이 때 사용하는 트리는 Red-Black Tree인데, JCF의 TreeMap과 구현이 거의 같다.
* 트리 순회시 사용하는 대소 판단 기준은 해시 함수 값이다.
* 해시 값을 대소 판단 기준으로 사용하면 Total Ordering에 문제가 생기는데, Java 8 HashMap에서는 이를 tieBreakOrder() 메서드로 해결한다.

참고
* https://d2.naver.com/helloworld/831311




















