# Stream Distinct

Java8의 Collection 객체의 stream에서 중복을 제거하고 싶을 때는 distinct()를 사용한다.

distinct는 stream의 원소들을 Object.equals(Object)에 따라서 중복을 제거하는데 처음 나타난 원소가 유지되기 때문에 정렬되어 있지 않으면 안정적이지 않다.

하지만 객체내의 특정 키를 기준으로 distinct()를 이용하여 중복제거를 할 수 없다. 이 때는, Predicate를 리턴하는 메소드를 만들어서 내부 지역변수로 HashMap을 생성하고 리턴하는 Predicate에서 Map을 참조하게 하면 객체내의 특정 키를 기준으로 중복제거를 할 수 있다.

```
class testClass {
  int num;
}

public static <T> Predicate<T> distinctByKey(Function<? super T, Object> keyExtractor) {
  Map<Object, Boolean> map = new HashMap<>();
  return t -> map.putIfAbsent(keyExtractor.apply(t), Boolean.TRUE) == null;
}

list.stream().filter(distinctByKey(t -> t.getNum())).collect(Collectors.toList());
```

filter에서 distinctByKey가 반환해주는 Predicate를 사용하면 된다.

filter에서 계속 distinctByKey를 호출하면 distinctByKey 인스턴스가 계속 생긱는 것 처럼 보여 Map을 공유하지 못하는 것처럼 보일수도 있지만 distinctByKey 메소드는 한번만 실행하고 Predicate를 반환해준다.

람다 표현식은 컴파일러에 의해 static method로 작성되고 BootstrapMethods에서 LambdaMetaFactory.metafactory메소드를 호출하여 static method를 핸들링하는 CallSite를 생성한다. 그렇기 때문에 같은 $Lambda메소드를 사용하게 되고 같은 map을 공유하면서 사용할 수 있게 된다.

[testCode](https://github.com/sdh2398/java-8/blob/master/src/test/StreamDistinctTest.java)

참조
https://medium.com/@circlee7/java8-stream-%ED%8A%B9%EC%A0%95-key-%EC%A4%91%EB%B3%B5%EC%A0%9C%EA%B1%B0-7b10dcede37
https://stackoverflow.com/questions/47387475/how-predicate-maintain-state-in-java-8/47392827#47392827
https://stackoverflow.com/questions/27870136/java-lambda-stream-distinct-on-arbitrary-key/27872086#27872086
https://stackoverflow.com/questions/23699371/java-8-distinct-by-property
https://medium.com/@circlee7/java8-lambda-%EB%9E%8C%EB%8B%A4-%ED%91%9C%ED%98%84%EC%8B%9D%EC%9D%98-%EB%8F%99%EC%9E%91-%EC%9D%B4%ED%95%B4-cf5342eeb5ac
