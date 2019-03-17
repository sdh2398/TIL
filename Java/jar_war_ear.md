# jar, war, ear

jar, war, ear와 같은 압축방식들은 압축의 해제없이 JDK에서 각 파일들을 접근하여 사용할 수 있도록 설계되어 있다. java jar tool을 이용하여 압축된 파일들을 의미하고, 각 파일들은 다른 목적을 가지고 사용된다.

각 파일이 담고 있는 규모를 따지면 class < jar < war < ear 이라고 볼 수 있다.

### jar (java archive)
* 라이브러리, 리소스, property 파일들을 포함한다.
* JDK에서 제공하는 Java Archive Tool을 이용하여 jar 파일에 대한 작업을 할 수 있다.
* 하나의 application 기능이 가능하도록 java 파일을 압축하고 지원한다.

### war (web archive)
* war로 올리면 was가 압축을 해제하여 배포해준다. jar cvf 파일명으로 생성한다.
* web application을 지원하기 위한 압축방식으로 jsp, servlet, gif, html, jar 등을 지원한다.
* 단독으로 실행이 안되고 서버 컨테이너(was)에 의해 실행되어야하므로 배포디스크립터가 담겨 있다.(web.xml)

### ear (enterprise archive)
* 하나의 application 단위를 넘어서 실제 서버에서 배포하기 위한 단위를 의미한다.
* jar와 war를 묶어서 각각의 기능을 지원한다.
    * jar는 애플리케이션 레벨(business layer)
    * war는 웹 애플리케이션 레벨(web layer)

참고
https://mkil.tistory.com/409
http://codebm.blogspot.com/2016/04/java-jar-war-ear.html
https://bbchu.tistory.com/22
