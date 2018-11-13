# Structuring Your Code

### 디폴트 패키지 사용을 피해야 한다.
스프링 부트 프로젝트에서 패키지를 정의하지 않으면 default package에 있는 것으로 간주된다. default는 일반적으로 권장되지 않기 때문에 피해야 한다. default package에서는 jar의 모든 클래스가 읽히기 때문에 @ComponentScan, @EntityScan, @SpringBootApplication 애노테이션을 사용하는 Spring Boot 애플리케이션에서 특정 문제가 발생할 수도 있다.

### 메인 애플리케이션 클래스의 위치
일반적으로 메인 애플리케이션 클래스는 다른 클래스의 상위에 있는 루트 패키지에 위치시키는 것을 추천한다. @SpringBootApplication 애노테이션은 메인 클래스에 위치시키고, 검색 패키지(현재 패키지부터 scan)를 암시적으로 정의한다. 예를 들어 JPA 애플리케이션을 작성하는 경우에 @SpringBootApplication 애노테이션이 붙은 패키지에 속해 있는 @Entity 항목들을 스캔한다. 루트 패키지를 사용하면 컴포넌트 스캔을 해당 프로젝트에만 허용되게 할 수 있다.
> @SpringBootApplication 애노테이션을 사용하지 않아도 @EnableAutoConfiguration과 @ComponentScan 애노테이션이 해당 동작을 정의하므로 대신 사용할 수 있다.

참고
https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/#using-boot-structuring-your-code
