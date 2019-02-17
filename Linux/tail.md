# tail

tail 명령어는 파일 내용의 끝 부분만 출력하는 명령어이다.

### 옵션
- -f : 파일 변경을 감시해서 내용이 추가될 때마다 실시간으로 출력해준다.
- -F : -f옵션과 동일하나 특정 시간이 지나고 파일명이 변경되었을 때 새로운 파일을 열어 계속해서 보여준다(명령을 다시 실행시킬 필요가 없음).
- -n : 출력하는 줄 수를 지정할 수 있다(기본값으로는 10).
- -r : 역순으로 출력한다. -f옵션과는 같이 사용할 수 없다.

참고
https://jupiny.com/2017/07/09/linux-command-1-grep-less-head-tail/
https://johngrib.github.io/wiki/tail/
https://windfree.tistory.com/40
https://www.computerhope.com/unix/utail.htm
