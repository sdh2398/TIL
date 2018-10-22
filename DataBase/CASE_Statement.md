# CASE 문

RDBMS에 준비된 함수를 사용해 데이터를 특정 형태로 반환하는 경우도 있지만, 임의의 조건에 따라 독자적으로 변환처리를 지정해 데이터를 변환할 수도 있다. 이 때 CASE 문을 이용할 수 있다.

```
CASE
WHEN 조건식1 THEN 식1
  [WHEN 조건식2 THEN 식2 ...]
  [ELSE 식3]
END
```

RDBMS에서 사용자 정의 함수를 작성해서 해결할 수도 있지만 간단한 처리의 경우에는 사용자 정의 함수를 작성하지 않고도 CASE 문으로 처리하는게 편리하다. 예를 들어 NULL 값은 어떤 값과 연산하더라도 NULL로 간주하는데 0으로 간주하고 계산하고 싶은 경우이다.

먼저 WHEN 절에는 참과 거짓을 반환하는 조건식을 기술한다. 해당 조건을 만족하여 참이 되는 경우에 THEN 절에 기술한 식이 처리된다.

```
SELECT a,
CASE
  WHEN a IS NULL 0
  ELSE a
END
FROM sample_table;
```
a의 열 값이 NULL일 때 WHEN a IS NULL은 참이 되므로 CASE 문은 THEN 절의 0값을 반환한다. NULL이 아닌 경우에는 a 열의 값을 반환한다.

숫자로 이루어진 코드를 알아보기 더 쉽게 문자열로 변환하고 싶은 경우에도 CASE 문을 많이 사용한다. 예를 들어 '1은 남자, 2는 여자'로 변환하는 경우이다.
```
WHEN a = 1 THEN '남자'
WHEN a = 2 THEN '여자'
```

### '검색 CASE'와 '단순 CASE'
 CASE문은 '검색 CASE'와 '단순 CASE'의 두 개의 구문으로 나눌 수 있다.
 검색 CASE는 'CASE WHEN 조건식 THEN 식 ...'이고, 단순 CASE는 'CASE 식 WHEN 식 THEN 식 ...' 구문이다. 단순 CASE에서는 CASE뒤에 식을 기술하고 WHEN 뒤에 조건식이 아닌 식(값)을 기술한다.

```
CASE 식1
  WHEN 식2 THEN 식3
  [WHEN 식4 THEN 식5 ...]
  [ELSE 식6]
END
```

식1의 값이 WHEN의 식2의 값과 동일한지 비교하고, 값이 같다면 식3의 값이 CASE문의 결괏값이 된다.

성별 문자열을 디코딩 하는 것을 '검색 CASE'와 '단순 CASE'로 살펴보면 다음과 같다.
##### 검색 CASE
```
SELECT a,
CASE
  WHEN a = 1 THEN '남자'
  WHEN a = 2 THEN '여자'
  ELSE '미지정'
END
FROM sample_table;
```

##### 단순 CASE
```
SELECT a,
CASE a
  WHEN 1 THEN '남자'
  WHEN 2 THEN '여자'
  ELSE '미지정'
END
FROM sample_table;
```
CASE문은 어디에나 사용할 수 있다. WHERE 구에서 조건식의 일부로 사용될 수도 있고 ORDER BY 구나 SELECT 구에서도 사용할 수 있다.

ELSE를 생략하면 ELSE NULL이 된다. 상정한 것 이외의 데이터가 들어오는 경우도 많다. 대응하는 WHEN이 하나도 없으면 ELSE 절이 사용된다. 이 때 ELSE를 생략하면 상정한 것 이외의 데이터가 왔을 때 NULL이 반환된다. 따라서 ELSE를 생략하지 않는 편이 좋다.

데이터가 NULL인 경우를 고려해 WHEN NULL THEN '데이터 없음'과 같이 지정해도 문법적으로는 문제가 없지만 정상적으로 처리되지 않는다. WHEN에는 조건식이 들어가므로 a = NULL와 같이 '='연산자로 NULL값과 같은지 아닌지 비교할 수 없다. 결국 ELSE값이 결괏값이 된다.
```
CASE a
  WHEN 1 THEN '남자'
  WHEN 2 THEN '여자'
  WHEN NULL THEN '데이터 없음'
  ELSE '미지정'
END
```

그렇기 때문에 NULL 값인지 아닌지를 판정하기 위해서는 IS NULL을 사용한다. 다만 단순 CASE 문은 특성상 = 연산자로 비교하는 만큼, NULL 값인지를 판정하려면 검색 CASE 문을 사용해야 한다.
```
CASE
  WHEN a = 1 THEN '남자'
  WHEN a = 2 THEN '여자'
  WHEN a IS NULL THEN '데이터 없음'
  ELSE '미지정'
END
