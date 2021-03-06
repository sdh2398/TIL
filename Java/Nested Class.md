# 중첩 클래스(nested class)

다른 클래스 내부에 정의되는 클래스를 중첩 클래스(nested class)라고 한다. 중첩 클래스는 독립적인 오브젝트로 만들어질 수 있는 스태틱 클래스(static class)와 자신이 정의된 클래스의 오브젝트 안에서만 만들어질 수 있는 내부 클래스(Inner class)로 구분된다.

일반적으로 클래스는 독립적으로 정의되고 사용되지만 중첩 클래스는 멤버 형태로 클래스를 포함할 수 있으며 중첩되는 클래스의 개수는 제한이 없다. 중첩 클래스는 특정 클래스를 자신의 클래스 내부적인 용도로만 사용하고자 할 때 효율적이다.

중첩 클래스를 포함하는 외부 클래스를 Outer 클래스라고 하며 내부에 포함된 클래스를 Inner 클래스라고 할 때 Inner 클래스는 Outer 클래스의 멤버를 마치 자신의 멤버처럼 사용할 수 있다. 접근 지정자가 private라고 해도 접근이 가능하다. Inner 클래스의 접근은 반드시 Outer 클래스를 통해서 접근할 수 있다. Inner 클래스 안에는 static 변수를 선언할 수 없지만 static Inner 클래스는 static 변수 선언이 가능하고 static Inner 클래스라면 바로 접근이 가능하다.

### 내부 클래스
내부 클래스는 다시 범위(scope)에 따라 세 가지로 구분된다. 멤버 필드처럼 오브젝트 레벨에 정의되는 멤버 내부 클래스(member inner class)와 메소드 레벨에 정의되는 로컬 클래스(local class), 그리고 이름을 갖지 않는 익명 내부 클래스(anonymous inner class)다. 익명 내부 클래스의 범위는 선언된 위치에 따라서 다르다.

##### 익명 내부 클래스
익명 내부 클래스는 이름을 갖지 않는 클래스다. 클래스 선언과 오브젝트 생성이 결합된 형태로 만들어지며, 상속할 클래스나 구현할 인터페이스를 생성자 대신 사용해서 다음과 같은 형태로 만들어 사용한다. 클래스를 재사용할 필요가 없고, 구현한 인터페이스 타입으로만 사용할 경우에 유용하다.
```
new 인터페이스() { 클래스 본문 };
```

참고
http://ccm3.net/archives/20638
토비의 스프링3.1
