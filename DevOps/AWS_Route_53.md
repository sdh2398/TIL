# AWS Route 53

Route 53이란 AWS에서 제공하는 DNS이다.
> DNS 기능 외에도 여러가지 기능을 제공한다.

일반DNS와 다른 점은 Route 53 에서 네임서버를 할당 받은 후 도메인등록 대힝기관 사이트에 접속해 네임서버 정보를 등록해야 한다.

* aws의 route 53에 들어가서 호스트 영역을 생성을 누른다.
* 도메인 네임에 외부에서 구입한 도메인 이름을 적어준다.
* 호스트 영역을 생성하면 NS, SOA 레코드가 자동으로 생성된다.
* 네임서버(NS)를 도메인등록 대행기관 사이트에 접속해 네임서버를 등록한다.

Route 53의 비용
* Hosted Zone의 개수만큼 0.5$ (25개의 Hosted Zone 까지)
* 1,000,000 쿼리당 0.4$ (10억 쿼리 까지)

Route 53의 장점
* GUI를 제공한다.
* 네임서버 자체안정성이 높아진다.
* 글로벌 서비스가 가능해진다.

참고
* https://brunch.co.kr/@topasvga/85
