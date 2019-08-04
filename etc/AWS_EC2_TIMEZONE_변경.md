# AWS EC2 인스턴스 Timezone 변경

리눅스를 새로 설치하고 시간대(TIMEZONE)을 맞추지 않으면, 리눅스의 date가 미국 태평양 시간인 PST로 표시된다. 즉, 캘리포니아 현지 시간으로 표시된다. 이럴 경우 한국 표준 시간인 KST로 변경을 해주어야 한다.

```
$ date
2019. 08. 04. (일) 11:01:14 UTC

$ sudo rm /etc/localtime

$ sudo ln -s /usr/share/zoneinfo/Asia/Seoul /etc/localtime

$ date
2019. 08. 04. (일) 20:13:47 KST
```

> ln은 Link의 약어로서 리눅스 파일시스템에서 링크파일을 만드는 명령어이다. -s옵션을 사용시 심볼릭 링크파일을 생성

참고
- https://ora-sysdba.tistory.com/entry/Cloud-Computing-Amazon-EC2-%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4%EC%9D%98-TIMEZONE-%EB%B3%80%EA%B2%BD
- https://webdir.tistory.com/148