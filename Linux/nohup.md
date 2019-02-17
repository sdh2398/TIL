# nohup

.jar파일을 실행시킬 때 `java -jar jarfile.jar`를 통해서 .jar파일을실행시킨다.

단순히 .jar파일을 실행시키면 터미널을 종료시킬 때 프로그램도 같이 종료되게 된다. 종료되지 않기 위해서는 리눅스 상에서 데몬형태로 백그라운드에서 실행시켜야 터미널을 종료해도 같이 종료되지 않는다.

### nohup으로 실행시키기
nohup은 no hangup의 뜻이고, 리눅스 상에서 데몬형태로 실행시키는 명령어이다. 이 때 실행시키는 파일은 실행파일권한이 755이상으로 되어 있어야 한다.
nohup으로 실행시킬 때 백그라운드로 실행시키기 위해서는 명령어 뒤에 &를 붙이면 되고 nohup으로 실행시키면 nohup.log라는 로그 파일이 생성된다.

```
$ nohup 파일이름
$ nohup 파일이름 & // 백그라운드로 실행
```

### nohup으로 실행된 프로세르 종료하기
```
$ ps -ef | grep 파일명
$ kill -9 PID 번호
```

### nohup 프로세스 로그 보기
백그라운드로 실행된 프로젝트의 로그를 보고 싶은 경우가 있을 수 있다.
이 때 tail명령어에 -f옵션을 주고 nohup.out파일을 출력시켜주면 로그가 추가될때마다 계속해서 출력해준다.
```
$ tail -f nohup.out
```

참고
https://jasontody.tistory.com/113
https://klero.tistory.com/entry/nohup-%EB%AA%85%EB%A0%B9%EC%96%B4%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80
https://www.computerhope.com/unix/unohup.htm
https://github.com/sdh2398/TIL/blob/master/Linux/tail.md
