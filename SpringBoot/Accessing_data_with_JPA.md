### Accessing Data with JPA

### Define a sample entity
```
@Entity
public class Customer {
    @Id
    @GeneratedValue(strategy=GenerationType.AUTO)
    private Long id;
    private String firstName;
    private String lastName;

    protected Customer() {}

    public Customer(String firstName, String lastName) {
      this.firstName = firstName;
      this.lastName = lastName;
    }
}
```

디폴트 생성자는 오직 JPA를 위해서만 존재하고, 직접 사용할 일이 없기 때문에 protected로 지정한다. 다른 생성자는 Customer 인스턴스를 데이터베이스에 저장하는데 사용한다.

@Entity애노테이션이 달린 클래스는 JPA entity라는 것을 가리킨다. @Table애노테이션이 없으면 클래스 이름과 같은 Customer 테이블로 가정하고 매핑한다.

@Id애노테이션은 JPA가 오브젝트의 Id로 인식하도록 하고, @GeneratedValue는 Id가 자동으로 생성됨을 나타낸다.

아무 애노테이션도 달려 있지 않으면 같은 이름의 컬럼과 매핑된다.

### Create simple queries
Spring Data JPA는 JPA를 이용하여 관계형 데이터베이스에 데이터를 저장하는데 중점을 둔다. 가장 강력한 기능은 런타임 때 repository 인터페이스로부터 repository를 자동으로 구현하는 것이다.
```
public interface CustomerRepository extends CrudRepository<Customer, Long> {
  List<Customer> findByLastName(String lastName);
}
```

상속받는 CrudRepository의 제네릭 파라미터로 Entity와 Id의 타입을 지정해주면 된다. 상속받은 CustomerRepository는 Customer 엔티티의 저장, 삭제, 검색을 포함하는 Customer의 퍼시스턴스를 사용하기 위한 몇가지 메소드를 상속받는다.

Spring Data JPA는 findByLastName()과 같이 간단하게 메소드 시그니처를 정의함으로써 다른 쿼리 메소드를 정의할 수도 있다.

전형적인 자바 애플리케이션은 CustomerRepository를 구현하는 클래스를 작성해야 한다. 그러나 이것은 Spring Data JPA를 더 강력하게 만드는 이유이다. repository 인터페이스를 구현할 필요가 없고 Spring Data JPA가 애플리케이션을 실행할 때 즉석에서 구현을 생성한다.

참고 https://spring.io/guides/gs/accessing-data-jpa/
