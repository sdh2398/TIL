# Spring Data Jpa에서 InnoDB 테이블 생성하기

Spring Data Jpa의 ddl-auto를 create로 설정해서
 만들어진 테이블에 인덱스를 추가할려고 하니 다음과 같은 오류가 발생했다.
```
ERROR 1071 (42000): Specified key was too long; max key length is 1000 bytes
```

### 발생 원인
 발생 원인은 추가하려는 인덱스의 컬럼 길이가 1000bytes를 넘었다는 것
* utf-8은 한글자당 3~4bytes를 사용
    * utf8mb3 : 3bytes
    * utf8mb4 : 4bytes
* varchar(255)는 255 * 3 = 765bytes

InnoDB엔진을 사용하는 테이블은 최대 3072bytes까지 허용

MYISAM엔진을 사용하는 테이블은 1000bytes까지 허용

Spring Data Jpa를 이용할 때 dialect를 설정하지 않고 사용할 경우에는 default engine으로 MYISAM을 사용하도록 되어 있어 varchar(255)의 컬럼 2개로 인덱스를 만드니 오류가 발생이 된 것이다.

``` java
public MySQLDialect() {
         super();

         String storageEngine = Environment.getProperties().getProperty( Environment.STORAGE_ENGINE );
         if(storageEngine == null) {
             storageEngine = System.getProperty( Environment.STORAGE_ENGINE );
         }
         if(storageEngine == null) {
             this.storageEngine = getDefaultMySQLStorageEngine();
         }
         else if( "innodb".equals( storageEngine.toLowerCase() ) ) {
             this.storageEngine = InnoDBStorageEngine.INSTANCE;
         }
         else if( "myisam".equals( storageEngine.toLowerCase() ) ) {
             this.storageEngine = MyISAMStorageEngine.INSTANCE;
         }
        ...
}

protected MySQLStorageEngine getDefaultMySQLStorageEngine() {
         return MyISAMStorageEngine.INSTANCE;
}
```
> String STORAGE_ENGINE = "hibernate.dialect.storage_engine";

STORAGE_ENGINE이 null일 경우에 MYISAMStorageEngine를 반환하고 있다.

### 해결
```
spring.jpa.database-platform=org.hibernate.dialect.MySQL5InnoDBDialect
```
위와 같이 설정을 하면 Spring Data Jpa가 만들어준 테이블이 InnoDB로 생성된다고 해서 MySQL5InnoDBDialect에 찾아서 들어가보니 @Deprecated가 되어 있고 다음과 같이 설정을 하라고 적혀있다.
```
hibernate.dialect.storage_engine = innodb
```

또 다른 방법은 MySQL55Dialect보다 오래된 모든 Dialects는 MYISAM 스토리지 엔진을 사용하지만 MYSQL55Dialect부터는 InnoDB 스토리지 엔진이 기본적으로 사용된다고 하니 다음과 같이 설정을 해도 InnoDB로 사용을 할 수 있다.
```
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL55Dialect
```

``` java
public class MySQL55Dialect extends MySQL5Dialect {

     @Override
     protected MySQLStorageEngine getDefaultMySQLStorageEngine() {
         return InnoDBStorageEngine.INSTANCE;
     }
}
```
MySQL55Dialect를 들어가보면 getDefaultMySQLStorageEngine을 오버라이드해서 InnoDBSotrageEngine을 반환하는 걸 볼 수 있다.

### 참고
- https://stackoverflow.com/questions/16568128/max-size-of-unique-index-in-mysql
- https://stackoverflow.com/questions/1459265/hibernate-create-mysql-innodb-tables-instead-of-myisam
- https://in.relation.to/2017/02/20/mysql-dialect-refactoring/
- http://stackz.ru/en/1459265/hibernate-create-mysql-innodb-tables-instead-of-myisam
