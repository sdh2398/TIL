# String, StringBuffer, StringBuilder

문자열을 만드는 클래스는 String, StringBuffer, StringBuilder가 가장 많이 사용된다.
* StringBuffer, StringBuilder 클래스에서 제공하는 메서드는 동일하다.
* StringBuffer 클래스는 스레드에 안전하게(ThreadSafe) 설계되어 있어, 여러 스레드에서 하나의 StringBuffer 객체를 처리해도 문제가 되지 않는다.
* StringBuilder 클래스는 단일 스레드에서의 안정성만을 보장한다. 그렇기 때문에 여러 개의 스레드에서 하나의 StringBuilder 객체를 처리하면 문제가 발생한다.

``` java
String a = "ab";
a += "cd";
```

a에 "cd"를 더하면 새로운 String 클래스의 객체가 만들어지고, 이 전에 있던 a 객체는 필요 없는 쓰레기 값이 되어 GC 대상이 되어 버린다.
* 이런 작업이 반복 수행되면서 메모리를 많이 사용하게 되고, 응답 속도에도 많은 영향을 미치게 된다.
* GC를 하면 할수록 시스템의 CPU를 사용하게 되고 시간도 많이 소요된다.

StringBuffer나 StringBuilder는 String과는 다르게 새로운 객체를 생성하지 않고, 기존에 있는 객체의 크기를 증가시키면서 값을 더한다.

String은 무조건 나쁘고, StringBuffer와 StringBuilder 클래스만 사용하기 보다는 다음과 같이 상황에 맞게 쓰면 된다.
* String은 짧은 문자열을 더할 경우 사용한다.
* StringBuffer는 스레드에 안전한 프로그램이 필요할 때나, 개발 중인 시스템의 부분이 스레드에 안전한지 모를 경우 사용하면 좋다.
* 만약 클래스에 static으로 선언한 문자열을 변경하거나, singleton으로 선언된 클래스에 선언된 문자열일 경우에는 StringBuffer 클래스를 사용해야만 한다.
* StringBuilder는 스레드에 안전한지의 여부와 전혀 관계 없는 프로그램을 개발할 때 사용하면 좋다. 만약 메서드 내에 변수를 선언했다면, 해당 변수는 그 메서드 내에서만 살아있으므로, StringBuilder를 사용하면 된다.

> JDK 5.0 이상에서는 String을 사용해도 컴파일러에서 자동으로 StringBuilder로 변환하여 준다.

참고
- 자바 성능 튜닝 이야기