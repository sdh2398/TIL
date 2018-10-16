 SELECT의 내부 처리 순서

다음은 num1과 num2의 열을 더해서 10이상이 되는 행을 검색하는 쿼리문이다.
```
select *, num1 + num2 a add from sampleTable
where num1 + num2 >= 10;
```
select문에서 별명을 붙였으니 where에서 add로 지정하면 되지 않을까 생각할 수 있지만, 실제로는 add라는 열이 존재하지 않는다는 에러가 발생한다.

where 에서의 행 선택, select 에서의 열 선택은 데이터베이스 서버 내부에서 where -> select 순서로 처리된다.
표준 SQL에는 내부처리 순서가 따로 정해져 있지 않지만 where 구 -> select 순서로 내부 처리를 하는 데이터베이스가 많다. 따라서 where 구로 행 조건에 일치하는지 아닌지를 먼저 조사한 후에 select에서 지정된 열을 선택해 결과로 반환하는 식으로 처리한다.

별명은 select 구문을 내부 처리할 때 비로소 붙여진다. 즉, where의 처리는 select보다 선행되므로 where에서 사용한 별칭은 아직 내부적으로 지정되지 않은 상태가 되어 에러가 발생하는 것이다.

order by는 서버에서 내부적으로 가장 나중에 처리된다. 즉, select보다 나중에 처리되기 때문에 select에서 지정한 별명을 order by에서도 사용할 수 있다.
```
select *, num1 + num2 as add from sampleTable
order b add desc;
```
결론적으로 select 쿼리의 내부처리 순서는 where -> select(별명을 지정) -> order by 순서이다.
