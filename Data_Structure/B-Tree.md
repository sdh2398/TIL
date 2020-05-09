# B-Tree
데이터베이스 파일시스템에서 B-Tree를 많이 사용한다.

이진 트리는 자식 노드가 최대 2개인 노드를 말하는 것이라면 B-Tree는 자식 노드의 개수가 2개 이상인 트리를 말한다.
* 노드 내의 데이터가 1개 이상일 수가 있다.

### B-Tree의 성립 조건
* 노드의 데이터수가 n개라면 자식 노드의 개수는 n+1 개이다.
* 노드는 반드시 정렬된 상태여야 한다.
* 노드의 자식노드 데이터들은 노드 데이터를 기준으로 작은 데이터는 왼쪽 서브 트리에 큰 값들은 오른쪽 서브 트리에 이루어져야 한다.
* Root 노드가 자식이 있다면 2개이상의 자식을 가져야 한다.
* Root 노드를 제외한 모든 노드는 적어도 M/2개의 데이터를 갖고 있어야 한다.
    * 3차 B-Tree 까지는 1개의 데이터를 갖고 있어야 하니 고려하지 않아도 되는 조건
    * 4차 부터는 Root 노드를 제외하고 노드가 최소 2개의 데이터를 갖고 있어야 한다.
* Leaf 노드로 가는 경로의 길이는 모두 같아야 한다. 즉, Leaf 노드는 모두 같은 레벨에 존재해야 한다.
* 입력 자료는 중복될 수 없다,

### B-Tree의 탐색
이진트리와 마찬가지로 작은 값은 왼쪽 서브트리, 큰 값은 오른쪽 서브 트리에 이루어져 있기 때문에 탐색 하고자 하는 값을 Root 노드로부터 하향식으로 탐색해 나간다.

### B-Tree의 삽입
차수에 따라 B-Tree 알고리즘이 다르다.
* 초기 삽입시에는 Root 노드를 생성
* Leaf 노드 데이터가 가득 차 있으면 노드를 분리
    * 정렬된 노드를 기준으로 중간값을 부모 노드로 해서 트리를 구성
* 분리한 서브트리가 B-Tree 조건에 맞지 않는다면 부모 노드로 올라가며 Merge 한다.

### B-Tree의 삭제
삭제는 크게 Leaf 노드인 경우와 Leaf 노드가 아닌 경우로 나누어진다.
* Leaf 노드의 데이터를 삭제해도 B-Tree를 유지된다.
    * 그대로 둔다.
* Leaf 노드를 삭제해서 B-Tree 구조가 깨진다.
    * 삭제한 노드의 부모노드로 올라가서 데이터를 가져와 형제노드와 Merge한다.
    * Root 노드까지 올라가며 B-Tree 조건에 맞을 때까지 이 작업을 반복한다.
* Leaf 노드에 위치하지 않는 데이터를 삭제하고 깨지는 경우
    * 노드에서 데이터를 삭제하고 왼쪽 서브트리에서 최대값을 노드에 위치시킨다.
    * 같은 방식으로 부모노드에서 자식노드로 값을 가져오고 형제노드와 Merge하며 B-Tree 조건이 맞을 때까지 반복

참고
* https://hyungjoon6876.github.io/jlog/2018/07/20/btree.html
* https://potatoggg.tistory.com/174