# String 객체 메모리

Java에서 String을 생성하는 방식은 두 가지가 있다.
* new 연산자를 이용한 방식
    * Heap 영역에 존재하게 된다.
* 리터럴을 이용한 방식
    * String constant pool이라는 영역에 존재

### String을 리터럴로 선언할 경우의 동작 방식
내부적으로 String의 intern() 메서드가 호출되게 된다. intern() 메서드는 주어진 문자열이 string constant pool에 존재하는지 검색하고 있다면 그 주소값을 반환하고 없다면 string constant pool에 넣고 새로운 주소값을 반환하게 된다.

### String constant pool 위치 변경
자바6까지 string constant pool의 위치는 Perm영역에 존재했었다. 자바7부터는 Heap영역으로 변경되었다.
* 자바6까지는 String의 intern() 메서드를 호출하는 것은 OOM을 발생시킬 수 있고, 그 부분을 컨트롤 할 수 없었다.
* Perm 영역은 고정된 사이즈고 Runtime에 사이즈가 확장되지 않는다.
* Heap영역으로 옮기면서 문자열도 GC의 대상이 될 수 있도록 바뀌었다.

참고
* https://medium.com/@joongwon/string-%EC%9D%98-%EB%A9%94%EB%AA%A8%EB%A6%AC%EC%97%90-%EB%8C%80%ED%95%9C-%EA%B3%A0%EC%B0%B0-57af94cbb6bc