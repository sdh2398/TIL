# Json Web Token(JWT)
JWT는 Json Web Token의 약자로 인증에 필요한 정보들을 암호화 시킨 토큰을 뜻한다. 이렇게 만든 Access Token을 HTTP 헤더에 실어 서버로 보내 인증을 요청한다.

JWT를 만들기 위해서는 3가지가 필요하다.
* Header
    * JWT를 만들 때 사용하는 정보들을 암호화할 방식(alg), 타입(type) 등이 들어간다.
* Payload
    * 서버에서 보낼 데이터가 들어간다.
    * 일반적으로 유저의 고유 ID값, 유효기간이 들어간다.
* Verify Signature
    * Base 64 방식으로 인코딩한 Header, Payload, SECRET KEY를 더한 후 서명된다.

최종적인 결과
* Encoded Header + "." + Encoded Payload + "." + Verify Signature

Header, Payload는 인코딩될 뿐, 따로 암호화되지 않는다. 따라서 JWT 토큰에 유저의 중요한 정보(비밀번호)가 들어가면 누구나 디코딩하여 확인할 수 있어 쉽게 노출될 수 있다.

하지만 Verify Signature는 SECRET KEY를 알지 못하면 복호화 할 수 없다.
A의 사용자가 자신의 토큰의 payload에 있던 자신의 ID를 다른 사용자의 ID로 바꿔서 인코딩한 토큰을 서버에 보냈다고 하더라도, 서버에서는 A사용자의 payload를 기반으로 암호화 되었기 때문에 유효하지 않는 토큰으로 간주하게 된다. 결국 SECRET KEY를 알지 못하는 이상 토큰을 조작할 수 없다.

### JWT를 인증에 사용하기
1. 사용자가 로그인을 한다.
2. 서버에서는 계정정보를 읽어 확인 후, 고유한 ID값을 부여하여 기타 정보와 함께 Payload에 넣는다.
3. JWT의 유효기간을 설정하다.
4. 암호화할 SECRET KEY를 이용해 Access Token을 발급한다.
5. 사용자는 Access Token을 받아 저장한 후, 인증이 필요할 때마다 Http 헤더에 실어 보낸다.
6. 서버에서 JWT의 Verify Signature를 SECRET KEY로 복호화 후, 조작 여부, 유효 기간을 확인한다.
7. 검증이 되면, Payload를 디코딩하여 사용자의 ID에 맞는 데이터를 가져온다.

### JWT의 장점
* 세션/쿠키는 별도의 저장소 관리가 필요하지만, JWT는 발급한 후 검증만 하면 되기 때문에 추가 저장소가 필요 없다.
    * Stateless한 서버를 만들 수 있다는 말이다.
* 확장성이 뛰어나다. 토큰 기반으로 하는 다른 인증 시스템에 접근이 가능하다.

### JWT의 단점
* 이미 발급된 JWT에 대해서는 돌이킬 수 없다.
    * 세션/쿠키의 경우 세션을 지워버리면 되지만, JWT는 유효기간이 완료될 때까지는 계속 사용이 가능하다.
    * Access Token의 유효기간을 짧게 하고 Refresh Token이라는 새로운 토큰을 발급해서 피해를 줄일 수 있다.
* Payload 정보가 제한적이다.
    * Payload는 따로 암호화되지 않기 때문에 디코딩하면 누구나 정보를 확인할 수 있다.
    * 세션/쿠키 방식에서는 유저의 정보가 서버에 저장되기 때문에 안전할 수 있다.
* JWT의 길이
    * 세션/쿠키 방식에 비해 JWT의 길이가 길어서, 인증이 필요한 요청이 많아질 수록 서버의 자원낭비가 발생한다.




참고
https://tansfil.tistory.com/58
