# VM Arguments, Program Arguments

### VM Arguments
VM Arguments는 Java Virtual Machine(JVM)의 행동의 변화시키거 무언가를 지시하도록 하는 값이다. 예를 들어 -Xmx256M 값을 넣으면 Java의 힙 사이즈를 256MB로 올릴 수 있다.

다음과 같이 사용할 수 있다.
```
java -jar -Dspring.profiles.active=prod application.jar
```
-D다음에 값을 넣으면 된다.

### Program Arguments
Program Arguments는 애플리케이션에 전달되는 인수이며 애플리케이션이 실행될 때 사용하는 구체적인 값을 지정할 수 있다.
이 값은 main메소드의 파라미터를 통해 사용할 수 있다.

다음과 같이 사용할 수 있다.

```
java -jar application.jar --spring.profiles.active=prod
```
-- 다음에 값을 넣으면 된다.

참고
https://help.eclipse.org/mars/index.jsp?topic=%2Forg.eclipse.pde.doc.user%2Fguide%2Ftools%2Flaunchers%2Farguments.htm
https://stackoverflow.com/questions/31038250/setting-active-profile-and-config-location-from-command-line-in-spring-boot/37439625#37439625
