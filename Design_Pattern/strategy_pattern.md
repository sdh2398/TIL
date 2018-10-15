# 전략패턴

전략패턴은 OCP의 실현에도 가장 잘 들어 맞는 패턴이라고 볼 수 있다. 전략 패턴은 자신의 기능 맥락(context)에서 필요에 따라 변경이 필요한 알고리즘을 인터페이스를 통해 통째로 외부로 분리시키고, 이를 구현한 구체적인 알고리즘 클래스를 필요에 따라 런타임 시간에 바꿔서 사용할 수 있게 하는 디자인 패턴이다.

예를 들어 Dao는 전략 패턴의 컨텍스트에 해당한다. 컨텍스트는 자신의 기능을 수행하는데 필요한 기능 중에서 변경 가능한, DB 연결 방식이라는 알고리즘을 인터페이스로 정의하여, 이를 구현한 클래스를(전략이라고 부를 수 있는) 바꿔가면서 사용할 수 있께 분리하는 것이다.
전략 패턴의 적용 방법을 보면 컨텍스트(Dao)를 사용하는 곳에서 컨텍스트가 사용할 전략(DB 연결 방식을 구현한 클래스)을 컨텍스트의 생성자 등을 통해 제공해줘서 사용하는게 일반적이다.

전략패턴은 템플릿 메소드 패턴과 함께 많이 사용되지만 단일 상속만 가능한 자바에서는 템플릿 메소드 패턴보다는 전략 패턴이 더 많이 사용 된다.

<center><img src="..\img\Design_Pattern\Strategy_Pattern_in_UML.png"></center>