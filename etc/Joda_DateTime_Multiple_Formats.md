# Joda DateTime Multple Formats

기본적인 Joda DateTime을 원하는 format으로 사용하기 위해서는 다음과 같이 DateTimeFormat의 forPattern으로 원하는 format을 지정해서 사용하면 된다.
>원하는 format의 symbol을 확인하고 싶은 경우 [DataTimeFormat](https://www.joda.org/joda-time/apidocs/org/joda/time/format/DateTimeFormat.html) 를 확인
```
String timeStr = "2018-09-01";
DateTimeFormatter formatter = DateTimeFormat.forPattern("yyyy-MM-dd");
DateTime dateTime = DateTime.parse(timeStr, formatter);
```

하지만 입력으로 하나의 format으로 들어오지 않고 여러개의 format으로 입력이 들어오는 경우가 있다. 만약 입력된 포맷과 패턴이 맞지 않으면 java.lang.IllegalArgumentException예외가 발생한다. 물론 예외가 발생한 뒤 try-catch문에서 위의 예외가 발생했을 때 다른 패턴으로 사용할 수 있겠지만, 그것은 try-catch의 용도에 맞지 않는다.
이러한 상황에서는 DateTimeFormatterBuilder의 append 메소드를 사용하면 된다.
```
DateTimepParser[] parsers = {
  DateTimeFormat.forPattern("yyyy-MM-dd").getParser(),
  DateTimeFormat.forPattern("yyyy-MM-dd HH:mm:ss").getParser()
};
DateTimeFormatter formatter = new DateTimeFormatterBuilder().append(null, parsers).toFormatter();

DateTime dateTime1 = formatter.parseDateTime("2018-09-01");
DateTime dateTime2 = formatter.parseDateTime("2018-09-01 12:30:00");
```
DateTimeParser의 첫 번째 parser부터 선택되서 실패하면 다음 parser로 넘어가고 모두 성공하지 못하면 가장 비슷한 format이 있었던 파서의 위치가 반환된다.
참조 : [DataTimeFormatterBuilder.append()](http://joda-time.sourceforge.net/apidocs/org/joda/time/format/DateTimeFormatterBuilder.html#append%28org.joda.time.format.DateTimePrinter,%20org.joda.time.format.DateTimeParser%5B%5D%29)
