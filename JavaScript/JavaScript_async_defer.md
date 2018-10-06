# JavaScript async vs defer

자바스크립트는 상호작용 가능한 웹페이지 작성을 가능하게 한다. 정적인 HTML을 동적으로 조작할 수 있는 유일한 방법은 JavaScript를 사용하는 것이다.

HTML은 웹페이지의 content와 structure을 담당하고 있다. JavaScript는 정적인 HTML에 동적인 기능을 부여하는 것이다. 즉, HTML과 JavaScript는 역할이 다르므로 서로 다른 파일로 작성을 하는 것이 바람직하다.

웹 브라우저는 HTML을 랜더링하는 과정에서 css와 javascript를 만나면 동기적으로 처리한다. 동기적으로 처리하기 때문에 화면의 랜더링 속도에 많은 영향을 준다.

css의 경우는 화면을 랜더링할 때 필요한 정보들을 가지고 있으므로 해당 내용을 출력하기 전에 해석되는 것이 당연히 유리하다.
javascript의 경우 대부분 화면 출력과 관련되기 보다 기능적 처리에 관련된 경우가 많다. 웹앱 등의 경우 출력과 직접적인 관련이 있을 수도 있으나 이것도 기본적인 화면이 모두 출력된 이후에 처리되는 것이 웹 페이지를 빠르게 랜더링하는데 유리하기 때문에 처리를 지연하는 것이 좋다. 이러한 이유들로 대부분의 css는 <head> 영역에 javascript는 </body> 바로 앞에 선언하는 것을 추천한다. 이 방법 외에도 <script>에는 async 속성과 defer 속성을 사용하는 방법이 있다.

### 일반적인 경우
기본적으로 인라인 <script 코드의 경우 즉시 해석되고 실행될 수 있지만 그렇지 않은 경우는 해당 파일을 가져올 때까지 HTML 문서의 파싱을 중단한다. 그렇게 때문에 HTML이 화면에 출력되는 시간이 길어진다.
<center><img src="..\img\JavaScript\Normal-Execution.jpg"></center>

### async 속성이 추가된 경우
async 속성은 브라우저에 스크립트 파일이 비동기적으로 실행될 수 있음을 나타내기 위해 사용된다. HTML 구문 분석기는 스크립트 태그에 도달한 지점에 스크립트를 가져오고 실행하기 위해 일시 중지할 필요가 없다. 따라서 웹페이지 파싱과 외부 스크립트 파일의 다운로드가 동시에 진행되고, 스크립트는 다운로드 완료 직후 실행된다. 그러므로 순서가 중요한 스크립트들에 async를 사용할 때는 유의해야한다.
```
<script async src="script.js">
```
이 속성은 외부에 위치한 스크립트 파일에서만 사용할 수 있다. 외부 스크립트에 이 속성이 있으면 HTML 문서가 여전히 파싱되는 동안 파일을 다운로드 할 수 있으며 다운로드가 완료되면 스크립트가 실행될 수 있도록 파싱이 일시 중지된다.
<center><img src="..\img\JavaScript\Async-Execution.jpg"></center>

### defer 속성이 추가된 경우
defer 속성은 HTML 파싱이 완전히 완료되면 스크립트 파일을 실행하도록 브라우저에 지시한다.
```
<script defer src="script.js">
```
비동기적으로 로드된 스크립트와 마찬가지로, HTML 파싱이 실행되는 동안 파일을 다운로드 할 수 있다. 그러나 스크립트는 HTML 파싱이 완료되기 전에 다운로드가 완료되더라도 실행되지 않고 파싱이 모두 끝나면 실행된다. 또한, async와는 다르게 호출된 순서대로 실행된다.
<center><img src="..\img\JavaScript\Defer-Execution.jpg"></center>

##### 언제 사용을 해야 하는가?
- 스크립트가 모듈식이고 어떤 스크립트에도 의존을 하지 않는다면 async를 사용
- 스크립트가 다른 스크립트에 의존하거나 의존당하면 defer을 사용
- 스크립트가 작고 비동기 스크립트에 의존하는 경우 비동기 스크립트 위에 속성이 없는 인라인 스크립트를 사용

참조
[script의 async와 defer 속성](https://blog.asamaru.net/2017/05/04/script-async-defer/)
[Asynchronous and Deferred JavaScript](https://w3reign.com/asynchronous-and-deferred-javascript/)
