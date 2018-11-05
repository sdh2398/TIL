# mysqldump

mysqldump는 논리적 백업을 수행하여 원본 데이터베이스 객체의 정의 및 테이블을 재생성 할 수 있 SQL문 세트를 생성하는 것이다. option을 통해 여러가지 설정을 할 수 있다.
```
mysqldump [option] > dump.sql
```

- `--skip-add-drop-table` : create table문 전에 drop table문을 추가하지 않도록 할 수 있다.
- `--no-create-info` : create table문을 작성하지 않아 테이블을 다시 만들지 않도록 할 수 있다.
- `--replace` : insert문 대신 replace문으로 작성되게 할 수 있다.
- `--extended-insert=false` : insert문을 하나의 row로 하지 않고 mutiple row로 만들 수 있다.
나머지 옵션은 [mysqldump](https://dev.mysql.com/doc/refman/8.0/en/mysqldump.html) 참고

```
mysqldump -uroot -p --skip-add-drop-table --no-create-info --replace databasename tablename > dump.sql
```

### source
dump한 SQL 스크립트 파일을 읽어와서 실행시키거나 query문을 새로 작성하고 실행시키기 위해서는 source명령어를 사용한다.
```
mysql> source ~/Documents/dump.sql
```
mysql에 접속하여 source명령어와 sql파일 위치를 적으면 된다.
```
mysql> source dump.sql
```
만약 mysql을 접속한 위치와 파일이 있는 위치가 같다면 source와 sql 파일명을 적으면 된다.
