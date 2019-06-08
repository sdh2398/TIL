# OAuth

OAuth는 외부서비스의 인증 및 권한부여를 관리하는 범용적인 프로토콜이다.
> 권한 : 사용자의 권한에 따라 접근할 수 있는 데이터가 다르도록 설정이 가능하다.

> 프로토콜 : 특정한 프로그램을 지칭하는게 아니라 일종의 규격이다. Facebook, Google, Naver 등은 OAuth라는 규격에 맞춰 인증 및 권한을 대행관리 해준다.

OAuth는 세션/쿠키, 토큰 기반의 인증 방식을 완전히 대체하는게 아니다. OAuth를 사용하더라도 세션/쿠키 방식이나 토큰을 활용해 인증을 거쳐야 한다.

### OAuth2.0
현재 대다수가 사용하고 있는 OAuth는 2.0 버전이다.

2007년에 처음으로 OAuth 1.0의 초안이 발표되었고, 점점 커져가는 네트워크 시장에서 한계가 나타나기 시작해 2012년 OAuth 2.0을 새롭게 제시하였다.

OAuth2.0에서 크게 바뀐 점은 다음과 같다.
* 모바일 어플리케이션에서도 사용이 용이해졌다.
* 반드시 HTTPS를 사용하기에 보안이 강화되었다.
* Access Token의 만료기간이 생겼다.

OAuth2.0의 인증 방식은 크게 4가지이다.
* Authorization Code Grant
* Implicit Grant
* Resource Owner Password Credentials Grant
* Client Credentials Grant

각 인증 방식에는 장단점이 존재한다.

### OAuth2.0의 동작 순서
1. Resource Owner(사용자)가 Client(우리 서버)에게 인증 요청을 한다.
2. Client는 Authorzation Request를 통해 Resource Owner에게 인증할 수단(OAuth를 제공해주는 곳의 url)을 보낸다.
3. Resource Owner는 해당 Request를 통해 인증을 진행하고 인증을 완료했다는 신호로 Authorization Grant를 url에 실어 Client에게 보낸다.
4. Client는 해당 권한 증서(Authorization Grant)를 Authorization Server에 보낸다.
5. Authorization Server는 권한증서를 확인 후, 유저가 맞다면 Client에게 Access Token, Refresh Token, 그리고 유저의 프로필 정보(id 포함) 등을 발급해준다.
6. Client는 해당 Access Token을 DB에 저장하거나 Resource Owner에게 넘긴다.
7. Resource Owner가 Resource Server(OAuth를 관리하는 서버(Facebook, Google, Naver 등))에 자원이 필요하다면 Client는 Access Token을 담아서 Resource Server에 요청한다.
8. Resource Server는 Access Token이 유효한지 확인 후, Client에게 자원을 보낸다.
9. 만일 Access Token이 만료됐거나 위조되었다면, Client는 Authorization Server에 Refresh Token을 보내 Access Token을 재발급 받는다.
10. 그 후 다시 Resource Server에 자원을 요청한다.
11. 만인 Refresh Token도 만료되었을 경우, Resource Owner는 새로운 Authorization Grant를 Client에게 넘겨야 한다(다시 로그인 해야 된다는 말이다).

참고
* https://tansfil.tistory.com/60?category=255594
* http://blog.weirdx.io/post/39955