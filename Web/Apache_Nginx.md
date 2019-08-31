웹 서버는 HTTP 프로토콜을 통해 읽힐 수 있는 문서를 처리 하며 일반적으로 웹 어플리케이션의 앞단에 배치되곤 한다.
* 동적인 리소스는 WAS에게 처리하도록 하고 정적인 리소스를 보다 효율적으로 처리하기 위한 방법일수도 있다.

### Apache
Client에서 요청을 받으면 MPM(Multi Processing Module)이라는 방식으로 처리를 한다. 대표적으로는 Prefork와 Worker방식이 있다.

#### Prefork MPM
실행중인 프로세스를 복제하여 처리한다.
* 각 프로세스는 한번에 한 연결만 처리하고 요청량이 많아질수록 프로세스는 증가하지만 복제시 메모리영역까지 복제되어 동작하므로 프로세스간 메모리 공유가 없어 안정적이다.

#### Worker MPM
Prefork 동작방식이 1개의 프로세스가 1개의 스레드로 처리가 되었다면 Worker 동작방식은 1개의 프로세스가 각각 여러 쓰레드를 사용하게 된다.
* 쓰레드간 메모리를 공유하며 Prefork방식보다 메모리를 덜 사용하는 장점이 있다.

### Nginx
Nginx의 가장 유명한 특징은 Event Driven 방식을 꼽을 수 있다.

#### Event Driven
요청이 들어오면 어떤 동작을 해야하는지만 알려주고 다른요청을 처리하는 방식
* 프로세스를 fork하거나 쓰레드를 사용하는 아파치와는 달리 CPU와 관계없이 모든 IO들을 전부 Event Listener로 미루기 때문에 흐름이 끊기지 않고 응답이 빠르게 진행되어 1개의 프로세스로 더 빠른 작업이 가능하게 될 수 있다.
* 메모리적인 측면에서 Nginx가 System Resource를 적게 처리한다는 장점이 있다고 한다.

참고
* https://taetaetae.github.io/2018/06/27/apache-vs-nginx/
* http://old.zope.org/Members/ike/Apache2/osx/configure_html
* https://www.nginx.com/blog/inside-nginx-how-we-designed-for-performance-scale
