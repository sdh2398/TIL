# Spring Boot Test

### @SpringBootTest
@SpringBootTest는 통합 테스트를 제공하는 기본적인 스프링 부트 어노테이션이다.
* 애플리케이션이 실행 될 떄의 설정을 임의로 바꾸어 테스트를 진행할 수 있으며 여러 단위 테스트를 하나의 통합된 테스트로 수행할 때 접합하다.
* 실제 구동되는 애플리케이션과 똑같이 애플리케이션 컨텍스트를 로드하여 테스트하기 때문에 모든 테스트를 수행할 수 있다.
* 애플리케이션 규모가 클수록 느려지기 때문에, 단위 테스트라는 의미가 희석된다.

### @RunWith
JUnit 프레임워크가 테스트를 실행할 시 테스트 실행방법을 확장할 때 쓰는 애노테이션이다.
* @RunWith(SpringRunner.class)로 JUnit에 내장된 러너 대신 애노테이션에 러너를 정의할 수 있다.
* SpringRunner는 SpringJUnit4ClassRunner의 다른 이름이다.

### @WebMvcTest
* MVC를 위한 테스트, 웹에서 테스트하기 힘든 컨트롤러를 테스트하는데 적합하다.
* 웹상에서 요청과 응답에 대한 테스트 진행
* 시큐리티 혹은 필터까지 자동으로 테스트하며 수동으로 추가/삭제 가능
* MVC 관련된 설정인 @Controller, @ControllerAdvice, @JsonComponent와 Filter, WebMvcConfiguer, HandlerMethodArgumentResolver만 로드되기 때문에 @SpringBootTest 어노테이션보다 가볍게 테스트할 수 있다.