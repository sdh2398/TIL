# Inversion of Control / Dependency Injection

일반적인 경우에는 자기가 사용할 의존성을 자기가 만들어서 사용을 한다.

``` java
class UserController {
    private UserRepository repository = new UserRepository();
}
```

IoC는 사용은 하지만 직접 관리하고 만들지는 않는다.
* 누군가가 밖에서 줄 수 있도록 생성자를 통해 받아온다.
* 의존성을 만드는 일은 더이상 직접 하지 않는다.

``` java
class UserController {
    private UserRepository repo;
    
    public OwnerController(UserRepository repo) {
        this.repo = repo;
}
```

이렇게 의존성을 주입해주는 일을 DI라고 부르고 DI도 IoC의 일종이다.
* 의존성을 관리하는 일 자체를 Inversion(역전) 

스프링이 관리하는 빈으로 등록이 되면 해당 빈이 필요한 곳에 주입을 해준다.
* 스프링에 있는 IoC 컨테이너가 해준다.
* 스프링이 빈이라는 객체를 관리하는 것이다.
* 빈들의 의존성을 관리하고 빈들의 객체를 만들어서 빈으로 등록을 해주고 이렇게 만들어진 객체들을 스프링 컨테이너 안에 있으니 빈이라고 부르고 이 빈들의 의존성을 관리해준다.
* 여기서 의존성을 관리해준다는 것은 필요한 의존성을 서로 주입해준다는 것이다.
* 특정 생성자를 보거나 애노테이션을 보고 주입해준다.
    * 주입해주는 방법도 다양하고, 빈으로 등록하는 방법도 다양하다.

DI는 반드시 스프링이 필요한건 아니고 직접 코드상으로도 해줄 수 있다. 하지만 스프링이라는 프레임워크가 제공하는 풍부한 DI 관련된 기능이라던가 컨테이너의 라이프 사이클 인터페이스를 통해 다양한 확장이 가능해서 스프링이 제공해주는 IoC 컨테이너 기능을 사용하고 있다.