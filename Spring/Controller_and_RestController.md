# @Controller와 @RestController

일반적인 Spring MVC 컨트롤러와 RESTful 웹 서비스 컨트롤러의 주요 차이점은 HTTP 응답 바디가 생성되는 방식이다. 일반적인 MVC 컨트롤러는 View 기술을 사용하지만, RESTful 웹 서비스 컨트롤러는 객체를 반환하면 된다. 객체 데이터는 JSON/XML 형식의 HTTP 응답에 직접 작성한다.

@Controller는 전통적인 스프링 컨트롤러에서 오랜기간 사용되었다. @RestController는 스프링 4.0에서 소개되었고 RESTful한 웹 서비스를 만드는 것을 간단히 하기 위해 소개되었다. @Controller와 @ResponseBody를 합한 애노테이션이고, 컨트롤러 클래스에서 @ResponseBody 애노테이션이 필요한 요청 처리 메소드에 애노테이션을 달 필요가 없어졌다.

### Spring MVC @Controller
@Controller는 단순히 @Component의 특수한 애노테이션이고 구현 클래스가 클래스패스를 스캔할 때 자동으로 감지되도록 한다. 또, 일반적으로 요청 처리 메소드에 사용되는 @RequestMapping 애노테이션과 함께 사용한다.
```
@Controller
@RequestMapping("user")
public class UserController {
  @GetMapping("/{id}")
  public @ResponseBody User getUser(@PathVariable int id) {
    return userService.get(id);
  }
}
```
요청 처리 메소드는 @ResponseBody 애노테이션을 달아주어 자동적으로 HttpResponse 오브젝트로 리턴하도록 직렬화 해준다.

### Spring MVC @RestController
@RestController는 Controller의 특별한 버전이다. @Controller와 @ResponseBody 애노테이션이 포함되어 있어 Controller 구현이 간단해졌다.
```
@RestController
@RequestMapping("user")
public class UserController {
  @GetMapping("/{id}")
  public User getUser(@PathVariable int id) {
    return userService.get(id);
  }
}
```
컨트롤러에 @RestController를 붙임으로써 @ResponseBody가 없어도 요청 처리 메소드들은 자동으로 HttpResponse객체로 직렬화 되어 반환된다.
