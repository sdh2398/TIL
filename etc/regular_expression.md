# 정규 표현식(regular expression)

정규 표현식은 특정한 규칙을 가진 문자열의 집합을 표현하는 데 사용하는 형식 언어이다. 정규 표현식은 많은 텍스트 편집기와 프로그래밍 언어에서 문자열의 검색과 치환을 위해 지원하고 있다.

정규 표현식의 메타 문자
* `.` : 모든 문자와 일치한다.
* `[]` : 대괄호 사이에 있는 문자들 중 하나와 일치한다.
* `[^]` : 대괄호 사이에 가장 첫 문자로 ^문자가 있으면 이후에 있는 문자들을 제외한 모든 문자와 일치한다.
* `[a-z]` : 대괄호 사이에 문자1-문자2가 존재하면 문자1부터 문자2 사이의 모든 문자와 일치한다. a-z는 a부터 z까지의 모든 소문자와 일치한다.
* `^` : 대괄호 밖에서 사용하면 문자열의 시작과 일치한다.
* `$` : 문자열의 끝과 일치한다.
* `*` : 앞에 존재하는 문자가 0번 이상 반복되는 문자를 찾을 때 사용한다.
* `+` : 앞에 존재하는 문자가 1번 이상 반복되는 문자를 찾을 때 사용한다.
* `?` : 앞에 존재하는 문자가 있을 수도 있고, 없을 수도 있을 때 사용한다.
* `\` : 특수한 메타 문자를 문자열에서 찾고 싶을 떄, 문자 그대로 사용할 수 있도록 반환해준다. 예를 들어 `.`를 찾고 싶으면 `\.`를 사용하고, `?`를 찾고 싶으면 `\?`를 사용한다.

* `\w` : `_`를 포함한 영문자를 일치한다.
* `\W` : `_`를 포함한 영문자를 제외한 문자와 일치한다.
* `\d` : 숫자와 일치한다.
* `\D` : 숫자를 제외한 문자와 일치한다.
* `\s` : 공백 문자와 일치한다(스페이스, 탭 등등..)
* `\S` : 공백 문자를 제외한 문자와 일치한다.

* `{n}` : 앞에 존재하는 문자가 n번 반복되는 문자와 일치한다.
* `{n, m}` : 앞에 존재하는 문자가 n번 이상 m번 이하 반복되는 문자와 일치한다.
* `{n, }` : 앞에 존재하는 문자가 n번 이상 반복되는 문자와 일치한다.

* `()` : ()문자로 그룹을 지정할 수 있으며, 괄호 사이에 존재하는 표현식을 통해 찾은 결과를 묶음으로 처리할 수 있다.
* `(?=)` : 원하는 표현식 전에 있는 문자열 중에 찾고자 하는 문자가 있을 때 사용한다. 예를 들어 `[a-z](?=target)` 이면 target이라는 문자 앞에 있는 소문자를 찾아준다.
* `(?<=)` : 원하는 표현식 이후에 있는 문자열 중에 찾고자 하는 문자가 있을 때 사용한다.