# Transaction Isolation Level

### Read Uncommitted
Read Uncommitted는 서로 다른 트랜잭션에서 commit되지 않은 데이터를 읽어 올 수 있는 level이다. commit되지 않는 데이터를 읽어 오고 난 뒤 해당 트랜잭션이 rollback이 된다면 결국 존재해서는 안 될 데이터를 읽어오게 되어 버린다.

Read Uncommitted level에서는 세 가지 현상이 모두 발생할 수 있다.
* 아직 commit 되지 않은 신뢰할 수 없는 데이터를 읽어 올 수 있다(dirty read).
* 한 트랜잭션에서 동일한 select 쿼리의 결과가 다르다(non-repeatable read).
* 이전의 select 쿼리의 결과에 없던 row가 생긴다(phantom read).

### Read Committed
Read Committed는 다른 트랜잭션에서 commit 된 데이터만 읽어 올 수 있는 level이다.

Read Committed level에는 두 가지 현상이 모두 발생할 수 있다.
* 한 트랜잭션에서 동일한 select 쿼리의 결과가 다르다(non-repeatable read).
* 이전의 select 쿼리의 결과에 없던 row가 생긴다(phantom read).

### Repeatable Read
Repeatable read는 Mysql InnoDB의 기본 isolation level이다. 

Mysql의 Repeatable Read와 Read Committed level에서는 한 트랜잭션에서 select 쿼리로 데이터를 읽어 올 때 테이블에 lock을 걸지 않고, 해당 시점의 데이터 상태를 의미하는 snapshot를 구축하여 데이터를 읽어온다.

Read Committed는 각각의 select 쿼리를 호출할 때 해당 시점의 최신 snapshot을 구축하여 데이터를 읽어 오기 때문에, 한 트랜잭션이지만 select 쿼리의 결과가 다를 수 있다.

Repeatable Read는 한 트랜잭션에서 처음 데이터를 읽어올 때 구축한 shapshot에서 모두 데이터를 읽어온다. 따라서 select 쿼리를 호출 할 때마다 결과들이 항상 처음과 동일 했던 것이고, 이로 인해 non-repeatable read와 phantom read도 발생하지 않는다.

Repeatable Read에서 흥미로운 점은 한 트랜잭션의 select결과는 항상 동일하지만, 다른 트랜잭션에서 건드린 row에 대한 update, delete의 결과는 출력 될 수 있다. 다른 트랜잭션에서 새로 추가한 row를 update한다고 하면 select 쿼리에는 없던 row지만 변경이 되었다는 문구가 출력되고 다시 select 쿼리를 실행해보면 최신의 snapshot에서 데이터를 읽어와서 보여준다.

### Serializable
Repeatable Read가 동시성과 안정성의 균형을 가장 잘 갖춘 isolation level였다면, Serializable은 동시성을 상당 부분 포기하고 안정성에 큰 비중을 둔 isolation level이다. Serializable은 한 트랜잭션 안에서 단순 select 쿼리를 사용하더라도, 모두 select ... for share으로 변환한다.
> select ... for share은 읽어온 row들에 shared lock(read lock)을 거는 쿼리이다.
> shared lock은 다른 트랜잭션이 lock된 데이터를 읽을 수는 있지만 쓰기를 금지하는 lock이다.

서로 다른 트랜잭션에서 shared lock이 걸려있기 때문에 데이터는 읽어 올 수 있지만 update나 insert 쿼리로는 해당 row의 lock이 풀리기 전까지 수정이나 추가할 수 없다. 만약 수정이나 추가를 하면 결과가 바로 출력되지 않고 정해진 시간만큼 대기 하다가 timeout이 되면 에러메세지를 띄워줄 것이다. 

참고
https://jupiny.com/2018/11/30/mysql-transaction-isolation-levels/
