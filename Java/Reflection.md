# 리플렉션

리플렉션은 구체적인 클래스 타입을 알지 못해도, 그 클래스의 메소드, 타입, 변수들을 접근할 수 있도록 해주는 자바 API이다.

구체적인 타입을 알지 못하면 해당 클래스의 정보들을 알아낼 수 없다.
```
public Class Example {
    public void something() {
        // …
    }
}

public class Main {
    public static void main(String[] args) {
        Object example = new Example();
        Example.something(); // 컴파일 에러
    }
}
```

모든 조상 클래스인 Object타입으로 Example 클래스를 담을 수는 있지만, Example 클래스에 대한 정보는 모르기 때문에 해당 클래스에 있는 메소드에는 접근할 수 없다.

코드를 작성할 시점에는 어떤 타입의 클래스를 사용할지 모르는 경우에 사용한다. 컴파일 타임이 아니라 애플리케이션이 실행되고 있는 런타임 시점에 지금 실행하려고 하는 클래스를 가져와서 실행할 때 사용한다.

### 리플렉션을 사용해서 구체적인 클래스 타입을 알지 못해도 해당 정보들을 가져올 수 있는 이유
자바 클래스 파일은 바이트 코드로 컴파일되어 해당 클래스를 사용할 때 클래스 로더를 통해 Runtime Data Area 내부의 Method Area라는 곳에 해당 클래스 정보를 저장해 놓는다.

그렇게 때문에 해당 클래스의 이름만 알고 있으면 해당 클래스에 대한 정보를 알고 싶을 때 Method Area 영역에 있는 정보를 가져와서 사용할 수 있는 것이다.

> Runtime Data Area : JVM이라는 프로그램이 운영체제 위에서 실행되면서 할당받는 메모리 영역

> Method Area : 모든 스레드가 공유하는 영역으로 JVM이 시작될 때 생성된다. JVM이 읽어 들인 각각의 클래스와 인터페이스에 대한 런타임 상수 풀, 필드와 메서드 정보, static 변수, 메서드의 바이트코드 등을 보관한다.

참고
* https://brunch.co.kr/@kd4/8
* https://d2.naver.com/helloworld/1230
