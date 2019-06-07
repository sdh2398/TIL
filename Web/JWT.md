# Json Web Token(JWT)
JWT는 Json Web Token의 약자("jot"이라고 읽는다고 한다)로 인증에 필요한 정보들을 암호화 시킨 토큰을 뜻한다. 이렇게 만든 Access Token을 HTTP 헤더에 실어 서버로 보내 인증을 요청한다.

JWT를 만들기 위해서는 3가지가 필요하다.
* Header
    * JWT를 만들 때 사용하는 정보들을 암호화할 방식(alg), 타입(type) 등이 들어간다.
        * 타입은 JWT 등..
        * 방식은 HS256, SHA256, RSA 등..
* Payload
    * 서버에서 보낼 데이터가 들어간다.
        * Regisstered claims
            * 이미 정의된 클레임, 무조건 따라야 하는건 아니지만 권장한다.
            * compact를 위해 3글자로 사용하고 있다(iss, exp, sub, aud ...)
                * iss(issuer) : 토큰 발급자
                * sub(subject) : 토큰 제목
                * aud(audience) : 토큰 대상자
                * exp(expiration) : 토큰의 만료시간
        * public claims
            * JWT를 사용하는 사람들에 의해 정의된 클레임
        * private claims
            * 서버, 모듈간에 정보를 공유하기 위해 만들어진 사용자 정의 클레임
    * 일반적으로 유저의 고유 ID값, 유효기간이 들어간다.
* Verify Signature
    * Base 64 방식으로 인코딩한 Header, Payload, SECRET KEY를 더한 후 서명된다.
    * 메시지가 도중에 변경되지 않았음을 확인하는데 사용한다.

최종적인 결과
* Encoded Header + "." + Encoded Payload + "." + Verify Signature
* 만들어진 JWT는 jwt.io의 Debugger로 decode하여 값을 확인할 수 있다.

Header, Payload는 인코딩될 뿐, 따로 암호화되지 않는다. 따라서 JWT 토큰에 유저의 중요한 정보(비밀번호)가 들어가면 누구나 디코딩하여 확인할 수 있어 쉽게 노출될 수 있다.

하지만 Verify Signature는 SECRET KEY를 알지 못하면 복호화 할 수 없다.

A의 사용자가 자신의 토큰의 payload에 있던 자신의 ID를 다른 사용자의 ID로 바꿔서 인코딩한 토큰을 서버에 보냈다고 하더라도, 서버에서는 A사용자의 payload를 기반으로 암호화 되었기 때문에 유효하지 않는 토큰으로 간주하게 된다. 결국 SECRET KEY를 알지 못하는 이상 토큰을 조작할 수 없다.
> JWT는 SECRET KEY를 모르면 변조는 불가능하지만 누구나 읽을 수 있다.

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
* Security Assertion Markup Language Tokens(SAML)보다 JWT가 크기가 작다.
    * Json은 XML보다 덜 장황하고 복잡하기 때문에 인코딩할 때 XML기반의 SAML보다 크기가 작다.
* JSON parser는 객체에 직접 매핑되기 때문에 대부분의 프로그래밍 언어에서 사용할 수 있다.


### JWT의 단점
* 이미 발급된 JWT에 대해서는 돌이킬 수 없다.
    * 세션/쿠키의 경우 세션을 지워버리면 되지만, JWT는 유효기간이 완료될 때까지는 계속 사용이 가능하다.
    * Access Token의 유효기간을 짧게 하고 Refresh Token이라는 새로운 토큰을 발급해서 피해를 줄일 수 있다.
* Payload 정보가 제한적이다.
    * Payload는 따로 암호화되지 않기 때문에 디코딩하면 누구나 정보를 확인할 수 있다.
    * 세션/쿠키 방식에서는 유저의 정보가 서버에 저장되기 때문에 안전할 수 있다.
* JWT의 길이
    * 세션/쿠키 방식에 비해 JWT의 길이가 길어서, 인증이 필요한 요청이 많아질 수록 서버의 자원낭비가 발생한다.

### JWE, JWS, JWT
JWT 규격에 따르면 "JWT는 claims 집합을 JWS와 (또는) JWE 구조로 인코드한 JSON 객체로 표현된다"라고 되어 있다. 기술적으로는 "JWT"는 서명되지 않은 토큰을 의미하지만 일반적인 상황에서는 JWT는 JWS나 JWS+JWE를 의미한다.

JSON Web Signature(JWS)
* 서명된 JWT를 JWS라고 부른다.
* 서버는 JWT를 JWS체계로 서명해서 signature와 함께 클라이언트로 전송한다.
* JWT가 위조되었거나 변경되지 않았다는 것을 보장한다.
* JWS을 통해 위변조를 확인할 수 있을 뿐 JWT는 근본적으로 암호화되지 않은 문자열이다.
    * 그래서 민감한 정보는 저장하면 안된다.

JSON Web Encryption(JWE)
* JWE체계에서는 내용이 서명없이 암호화된다.
* JWT에 암호화를 통한 기밀성은 부여하지만 JWE는 JWS만큼의 보안성은 제공하지 못한다.

즉, JWS+JWE로 안전한 토큰을 만들 수 있다.



참고
* https://jwt.io
* https://tansfil.tistory.com/58
* https://medium.com/@OutOfBedlam/jwt-%EC%9E%90%EB%B0%94-%EA%B0%80%EC%9D%B4%EB%93%9C-53ccd7b2ba10
* https://github.com/jwtk/jjwt