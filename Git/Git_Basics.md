# Git 기초

Git과 Subversion같은 것들의 가장 큰 차이점은 데이터를 다루는 방법이다. 대부분의 시스템은 각 파일의 변화를 시간순으로 관리하면서 파일들의 집합을 관리한다.
Git은 데이터를 파일 시스템 스냅샷의 연속으로 취급하고 크기가 아주 작다. Git은 커밋하거나 프로젝트의 상태를 저장할 때마다 파일이 존재하는 그 순간을 중요하게 여겨서 파일이 달라지지 않았으면 Git의 성능을 위해서 파일을 새로 저장하지 않고 이전 상태의 파일에 대한 링크만 저장하여 데이터를 스냅샷의 스트림처럼 취급한다.

### 거의 모든 명령들을 로컬에서 실행할 수 있다.
Git의 거의 모든 명령들이 로컬 파일과 데이터만 사용하기 때문에 네트워크에 있는 다른 컴퓨터는 필요 없다. 네트워크의 속도에 영향을 받는 CVCS에 비하면 Git은 프로젝트의 모든 히스토리가 로컬 디스크에 있기 때문에 모든 명령이 순식간에 실행되어 매우 빠르다.
즉, 오프라인 상태이거나 네트워크에 접속하고 있지 않아도 커밋을 하며 막힘없이 일을 할 수 있다.

### Git의 무결성
Git은 데이터를 저장하기 전에 항상 체크섬을 구하고, 그 체크섬으로 데이터를 관리한다. 그래서 체크섬을 이해하는 Git 없이는 어떠한 파일이나 디렉토리도 변경할 수 없다. 체크섬은 Git에서 사용하는 가장 기본적인(Atomic) 데이터 단위이자 Git의 기본 철학이다.  
Git은 SHA-1 해시를 사용하여 체크섬을 만든다. 이 체크섬은 40자 길이의 16진수 문자열이다. 파일의 내용이나 디렉토리 구조를 이용하여 체크섬을 구하기 때문에 파일을 이름으로 저장하지 않고 해당 파일의 해시로 저장한다.

### Git의 세 가지 상태
Git은 파일을 Committed, Modified, Staged 세 가지 상태로 관리한다.
- Committed : 데이터가 로컬 데이터베이스에 안전하게 저장됐다는 것을 의미한다. Git 디렉토리에 있는 파일들의 상태이다.
- Modified : 수정한 파일을 아직 로컬 데이터베이스에 커밋하지 않은 것을 말한다. Checkout 하고 나서 수정했지만, 아직 Staging Area에 추가하지 않은 상태이다.
- Staged : 현재 수정한 파일을 곧 커밋할 것이라고 표시한 상태를 의미한다. 파일을 수정하고 Staging Area에 추가한 상태이다.

이 세 가지 상태는 Git 프로젝트의 Git 디렉토리, 워킹 디렉토리, Staging Area 세 가지 단계와 연결되어 있다.

<img src="..\img\Git\areas.png">

Git 디렉토리는 Git이 프로젝트의 메타데이터와 객체 데이터베이스를 저장하는 곳을 말한다. 이 Git 디렉토리는 다른 컴퓨터에 있는 저장소를 Clone할 때 만들어진다.

워킹 디렉토리는 프로젝트의 특정 버전을 Checkout 한 것이다. Git 디렉토리는 지금 작업하는 디스크에 있고 그 디렉토리 안에 압축된 데이터베이스에서 파일을 가져와 워킹 디렉토리를 만든다.

Staging Area는 Git 디렉토리에 있다. 단순한 파일이고 곧 커밋할 파일에 대한 정보를 저장한다. Git에는 기술용어로는 "Index"라고 하지만, "Staging Area"라는 용어를 써도 상관 없다.

Git으로 하는 일을 다음과 같다.
1. 워킹 디렉토리에서 파일을 수정한다.
2. Staing Area에 파일을 Stage 해서 커밋할 스냅샷을 만든다. 모든 파일을 추가할 수도 있고 선택적으로 파일을 추가해서 스냅샷을 만들 수도 있다.
3. Staging Area에 있는 파일들을 커밋해서 Git 디렉토리에 영구적인 스냅샷으로 저장한다.

참고 https://git-scm.com/book/ko/v2/%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0-Git-%EA%B8%B0%EC%B4%88
