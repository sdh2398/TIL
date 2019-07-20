# Spring Filter, Interceptor, AOP

개발을 하다보면, 공통적으로 처리해야 할 업무들이 있다.
* 로그인 관련 처리
* 권한 체크
* XSS 방어
* 로그
* 페이지 인코딩
* pc와 모바일웹 분기처리

공통업무에 관련된 코드들이 여기저기 있다면 중복된 코드가 많아져서 서버에 부하를 주고, 소스 관리도 되지 않는다.
* 공통 부분은 빼서 따로 관리하는게 좋다.

이러한 공통업무를 프로그램 흐름의 앞, 중간, 뒤에 추가하여 자동으로 처리할 수 있는 방법이 있다.
* Filter
* Interceptor
* AOP

### Filter
요청과 응답을 거른뒤 정제하는 역할

필터는 스프링 컨텍스트 외부에 존재하여 스프링과 무관한 자원에 대해 동작한다.

Servlet Filter는 DispatcherServlet 이전에 실행이 되는데 필터가 동작하도록 지정된 자원의 앞단에서 요청내용을 변경하거나, 여러가지 체크를 수행할 수 있다.

또한 자원의 처리가 끝난 후 응답내용에 대해서도 변경하는 처리를 할 수가 있다.

일반적으로 인코딩 변환 처리, XSS방어 등의 요청에 대한 처리로 사용된다.

### Interceptor
요청에 대한 작업 전/후로 가로채는 역할

Filter와는 다르게 Interceptor는 스프링의 DispatcherServlet이 컨트롤러를 호출하기 전, 후로 끼어들기 때문에 스프링 컨텍스트 내부에서 Controller에 관한 요청과 응답에 대해 처리한다.

스프링의 모든 빈 객체에 접근할 수 있다.

Interceptor는 여러개를 사용할 수 있고 로그인 체크, 권한 체크, 프로그램 실행시간 계산작업 로그확인 등의 업무처리를 할 수 있다.

### AOP
OOP를 보완하기 위해 나온 개념

주로 로깅, 트랜잭션, 에러 처리 등 비즈니스단의 메소드에서 조금 더 세밀하게 조정하고 싶을 때 사용한다.

Interceptor나 Filter와는 달리 메소드 전후의 지점에 자유롭게 설정이 가능하다.

Interceptor와 Filter는 주소를 대상으로 구분해서 걸러내야하는 반면, AOP는 주소, 파라미터, 애노테이션 등 다양한 방법으로 대상을 지정할 수 있다.

AOP의 Advice와 HandlerInterceptor의 가장 큰 차이는 파라미터의 차이다.
* Advice의 경우 JointPoint나 ProceedingJoinPoint 등을 활용해서 호출한다.
* HandlerInterceptor는 Filter와 유사하게 HttpServletRequest, HttpServletResponse를 파라미터로 사용한다.

참고
https://goddaehee.tistory.com/154