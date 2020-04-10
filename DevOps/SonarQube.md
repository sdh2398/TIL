# 소스 정적 분석 도구 SonarQube

프로그램 정적 분석
* 프로그램의 실제 실행 없이 코드를 분석하는 것
* 다양한 도구들이 존재하지만 쉬운 플러그인 설치를 통해 다양한 기능을 제공하는 SonarQube가 보편적으로 사용되는 듯함

소나큐브
* 소나큐브는 코드를 분석하여 중복, 테스트 커버리지, 코드 복잡도, 버그, 보안 취약성 등을 리포팅 해준다.
* IDE, 빌드 도구, CI와 도구와 통합하여 사용할 수 있다.

소나큐브 데모 사이트
* https://sonarcloud.io/projects
* https://next.sonarqube.com/sonarqube/projects

소나큐브 설치
* 공식 홈페이지 가서 직접 다운로드 
    * http://www.sonarqube.org/
* 도커를 이용해서 사용할 수도 있다.
    * 도커 허브에서 소나큐브 이미지 다운받고 실행시키면 된다.
    * https://hub.docker.com/_/sonarqube/

소나큐브를 설치하고 실행시키면 localhost:9000으로 소나큐브 어드민 페이지로 접속이 가능하다.
* 기본적인 관리자 계정은 id : admin / password : admin 으로 되어 있다.

Maven으로 소나큐브 분석 시작하기
* SonarQube Runner를 수동으로 다운로드 할 필요없이 Maven의 goal로 소나큐브 분석을 실행할 수 있다.
* Maven build에는 소나큐브가 프로젝트를 분석하는데 필요한 많은 정보를 가지고 있어서 수동 설정의 필요성이 크게 감소

Maven의 Setting.xml 파일에 소나큐브 서버 설정을 추가
* Maven 설치 디렉토리 : $MAVEN_HOME/conf/settings.xml
* 사용자 홈 디렉토리 : ~/.m2/settings.xml
* 둘 중 아무곳에나 추가하면 된다.

``` xml
<settings>
    <pluginGroups>
        <pluginGroup>org.sonarsource.scanner.maven</pluginGroup>
    </pluginGroups>
    <profiles>
        <profile>
            <id>sonar</id>
            <activation>
                <activeByDefault>true</activeByDefault>
            </activation>
            <properties>
                <!-- Optional URL to server. Default value is http://localhost:9000 -->
                <sonar.host.url>
                  http://myserver:9000
                </sonar.host.url>
            </properties>
        </profile>
     </profiles>
</settings>
```

소나 큐브 분석을 하려고 하는 프로젝트 디렉토리(pom.xml이 존재하는 곳)에서 Maven goal을 실행시킨다.
```
mav sonar:sonar
```

오류 없이 성공되었다면 소나큐브 서버에서 해당 프로젝트가 분석된 것을 확인 할 수 있다.
* http://localhost:9000

참고
* https://docs.sonarqube.org/latest/analysis/scan/sonarscanner-for-maven/
* https://confluence.curvc.com/pages/viewpage.action?pageId=6160780
* https://medium.com/@SlackBeck/java-%EA%B0%9C%EB%B0%9C%EC%9E%90%EB%A5%BC-%EC%9C%84%ED%95%9C-maven-sonarqube-docker%EB%A1%9C-%EC%8B%9C%EC%9E%91%ED%95%98%EB%8A%94-%EC%BD%94%EB%93%9C-%EC%A0%95%EC%A0%81-%EB%B6%84%EC%84%9D-1d6a33f27dc
