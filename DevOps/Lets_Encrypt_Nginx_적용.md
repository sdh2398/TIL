# Let's Encrypt에 Nginx 적용하기

SSL/TLS 인증서는 웹 사이트를 운영하면서 거의 필수적인 요소이다.
* 클라이언트와 서버간의 통신이 발생할 때 전송되는 모든 패킷 데이터를 암호화하여 감청이나 식별을 어렵게하여 보안에 있어 강력한 역할을 한다.
* 웹 사이트 인증서는 대표적인 인증 기관(CA)에서 발급해준다.
* 대부분의 인증서 발급은 무료가 아니기 때문에 매년 새로운 인증서를 갱신함으로서 시간과 비용이 많이 든다.
* 이러한 가격적인 부담을 줄이고 인증서 발급의 복잡한 절차를 줄이고자 등장한게 Let’s Encrypt라는 비영리 기관이다.

### Let’s Encrypt의 장점
* 인증 절차가 단순화 되어있어 발급 대기 시간이 없어 빠르게 인증서를 적용할 수 있다.
* TLS 인증서 발급이 가능하며 와일드 카드 인증서를 지원한다.
* 발급을 위한 정보는 발급자 이메일만 요구된다.
* 만료된 인증서 갱신을 자동화 할 수 있다.
* 무료다.

Let’s Encrypt는 퍼블릭 도메인이 할당된 서버에서만 발급이 가능하다.
* 테스트용 서버이거나 공개 서버가 아닌경우 인증서 발급과 설치에 어려움이 있다.

인증서 유효기간은 90일이므로 지속적인 갱신 과정이 필요하다.
* 자동화할 수 있고, Let’s Encrypt에서도 자동화에 대한 규제를 하지 않는다.

Let’s Encrypt 인증서 사용시 주의 사항
* 인증서로 인해 발생한 피해는 보상 받을 수 없다.
* 일부 오래된 운영체제나 브라우저에서 인증서로 인한 올바르지 않은 동작이 발생할 수 있다.

### Amazon Linux에서 사용
Amazon Linux에서는 Certbot을 공식적으로 지원하지는 않지만 다운로드가 가능하고 설치하면 제대로 작동한다.

EPEL(Extra Packages for Enterprise Lunux) 7 리포지토리 패키지를 다운로드한다.
* Certbot에 필요한 종속성을 공급하는데 사용한다.

홈 디렉토리에서 EPEL을 다운로드한다.
```
$ sudo wget -r --no-parent -A 'epel-release-*.rpm' http://dl.fedoraproject.org/pub/epel/7/x86_64/Packages/e/
```

리포지토리 패키지를 설치한다.
```
$ sudo rpm -Uvh dl.fedoraproject.org/pub/epel/7/x86_64/Packages/e/epel-release-*.rpm
```

EPEL을 활성화한다.
```
$ sudo yum-config-manager --enable epel*
```

EPEL이 활성화되었는지 확인
```
$ sudo yum repolist all
```

### Certbot 설치

Let’s Encrypt 인증서를 설치하기 위해서는 Certbot이라는 커맨드라인 도구를 사용한다.
```
$ sudo yum install certbot
```

이후 각각의 웹서비스에 맞는 플러그인을 설치
```
$ sudo yum install python2-certbot-nginx
```

이렇게 했는데 잘 안되서 그냥 certbot-auto를 다운받아서 진행했다.
```
$ wget https://dl.eff.org/certbot-auto
$ chmod a+x certbot-auto
$ sudo ./certbot-auto
```

### 발급 과정
인증서를 발급하는 방법은 주로 webroot, Standalone, DNS의 3가지 방식이 있다.

webroot
* 실제 웹 디렉토리 내에 인증서의 유효성을 확인할 수 있는 파일을 업로드하여 인증서를 발급하는 방법
* 한 번의 명령에 하나의 도메인 인증서만 발급받을 수 있다.

Standalone
* 일시적으로 호스트 내의 웹 서비스를 빌려 인증서 유효성을 확인하는 방법
* 여러 도메인을 발급받을 수 있으나 이 방법을 사용하면 인증서가 발급되는 동안 운영 중인 웹 서비스가 잠시 중단될 것이다.

DNS
* 도메인을 쿼리하여 나타나는 TXT 레코드에서 인증서 유효성을 확인하는 방법
* 해당 도메인의 DNS를 관리/수정할 수 있는 조건이 되어야 한다.

인증 기관(CA)이 발급할 서버에 방문하여 인증서와 동일한 도메인인지 확인하는 과정이 진행된다. 이러한 과정에 ACME 프로토콜을 사용하여 CA와 서버 간의 유효성 검증을 시도한다. 따라서 투명성을 위해 인증 도중 서버의 IP와 트랜잭션 내역이 인증 기관에 기록되게 된다.

### Certbot 명령어
Certbot의 기본적인 명령어
```
sudo certbot —nginx --standalone -d example.com certonly
```
* -apache / -nginx : 웹 서비스 이름을 옵션값으로 붙여주어 해당 웹 서비스에 맞는 발급 과정을 진행
* --standalone / --webroot : 인증서 발급 방식, 세가지 방식을 직접 선택할 경우 --manual, DNS 방식의 경우 --preferred-challenges dns
* -d [도메인 이름] : 여러 도메인을 사용하는 경우 계속 -d옵션을 붙이거나 콤마(,)로 구분하여 입력하면 된다.
* certonly : 원래는 인증서 발급 시 웹 서비스의 설정 파일을 편집해준다(직접 수정하는게 안전), certonly값을 붙이면 설정 파일에 인증서 관련 내용을 임의로 수정하지 않는다.

Standalone 방식이 제일 간편하고 빨라서 이걸로 진행

Standalone방식은 웹 서비스를 임시로 빌리기 때문에 현재 구동되고 있는 웹 서비스를 잠시 중지해야 한다.
```
sudo service nginx stop
```
* 80포트를 사용하기 때문

### 웹 서비스에 반영
인증서가 생성되면 인증서 파일은 다음 경로에 저장된다.
```
/etc/letsencrypt/live/[신청한 인증서의 도메인명].com
```

### Nginx 설정
Nginx 설정 파일 내용은 다음과 같다.
```
server {
    listen 443 ssl http2;
    listen [::]:443 ssl http2;
    server_name example.com www.example.com;
    root /usr/share/nginx/html;
    include /etc/nginx/example.com.conf.d/*.conf;
}
```

443 포트로 listen 하고 있는 server 블록 내에 다음과 같은 내용을 붙여넣는다.
```
* 인증서 경로 올바른지 확인 필요
ssl_certificate /etc/letsencrypt/live/example.com/fullchain.pem; # managed by Certbot
ssl_certificate_key /etc/letsencrypt/live/example.com/privkey.pem; # managed by Certbot
include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot
ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; # managed by Certbot
```

이제 중지했었던 웹 서비스를 다시 시작
```
sudo service nginx start
```

참고
* https://jootc.com/p/201901062488
* https://codechacha.com/ko/letsencrypt-using-nginx-certbot/
* https://docs.aws.amazon.com/ko_kr/AWSEC2/latest/UserGuide/SSL-on-amazon-linux-2.html
