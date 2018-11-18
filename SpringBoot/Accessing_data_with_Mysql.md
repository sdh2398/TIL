# Accessing data with Mysql

### Create the application.properties file
```
spring.jpa.hibernate.ddl-auto = create
spring.datasource.url = jdbc:mysql://localhost:3306/db_example
spring.datasource.username = springuser
spring.datasource.password = ThePassword
```
spring.jpa.hibernate.ddl-auto는 `none`, `update`, `create`, `create-drop`를 설정할 수 있다.
- `none` : H2나 다른 내장 데이터베이스의 기본 값은 create-drop이지만 Mysql의 기본 값은 none이다. 데이터베이스 구조를 변경하지 않는다.
- `update` : Hibernate가 주어진 Entity 구조에 따라서 데이터베이스를 변경한다.
- `create` : 데이터베이스를 매번 만들지만 닫을 때 삭제하지 않는다.
- `create-drop` : 데이터베이스를 만들고 SessionFactory가 닫힐 때 삭제한다.

처음 시작할 때는 데이터베이스 구조가 아직 없기 때문에 create로 시작하고 프로그램의 요구에 따라서 `update`나 `none`으로 바꿀 수 있다. `update`를 사용하면 데이터베이스 구조가 원하는 데로 바뀐다.

> 제품 상태의 데이터베이스에서는 `none`으로 설정 하고 Spring 애플리케이션에 연결된 Mysql 사용자의 모든 권한을 취소한 다음 오직 `SELECT`, `UPDATE`, `INSERT`, `DELETE`만을 제공하는 것이 좋은 보안 방법이다.

### Create the @Entity 모델
@Entity : Hibernate가 자동으로 테이블로 변환하도록 해주는 클래스이고, Hibernate에게 애노테이션이 달린 클래스의 테이블을 만들도록 한다.
```
@Entity
public class User {
}
```

### Create the repository
UserRepository 인터페이스는 CrudRepository 인터페이스를 상속받아 스프링에 의해서 userRepository라는 이름의 빈으로 구현되고, CRUD를 할 수 있는 메소드를 사용할 수 있다.
```
public interface UserRepository extends CrudRepository<User, Integer> {  
}
```

Gradle이나 Maven의 커맨드라인을 이용해 애플리케이션을 실행시킬 수 있다. 또 다른 방법으로는 필요한 의존성, 클래스, 리소스를 포함하는 단일 실행 가능한 JAR 파일로 빌드하고 실행할 수 있다. 따라서 개발 라이프사이클, 다양한 환경에서 애플리케이션을 쉽게 배포할 수 있다.

참고
https://spring.io/guides/gs/accessing-data-mysql/
