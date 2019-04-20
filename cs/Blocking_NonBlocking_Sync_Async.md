# Blocking, NonBlocking, Synchronous, Asynchronous

Blocking-Sync가 비슷하고, NonBlocking-Async가 비슷하다.

### 블록킹(Blocking)과 논블록킹(NonBlocking)

블록킹
* 자신의 수행결과가 끝날 때까지 제어권을 갖고 있다.
* 호출되는 함수가 바로 리턴하지 않는다.

논블록킹
* 자신이 호출되었을 때 제어권을 자신을 호출한 쪽으로 넘긴다.
* 자신을 호출한 쪽에서 다른 일을 할 수 있도록 하는 것을 의미
* 호출되는 함수가 바로 리턴한다.

### 동기(Synchronous)와 비동기(Asynchronous)
동기
* 어떤 객체 또는 함수 내부에서 다른 함수를 호출했을 때 이 함수의 결과를 호출한 쪽에서 처리하면 동기
* 호출한 함수 쪽에서 신경을 쓴다.

비동기
* 어떤 객체 또는 함수 내부에서 다른 함수를 호출했을 때 이 함수의 결과를 호출한 쪽에서 처리하지 않으면 비동기
* 호출된 함수가 신경을 쓴다.

Blocking-Sync가 비슷하고, NonBlocking-Async가 비슷하지만 두 그룹은 관심사가 다르다.
Blocking-Sync는 막거나 기다리거나 하는 둥 비효율적으로 동작하고, NonBlocking-Async는 막지도 않고 완료되면 알아서 처리하는 등 효율적으로 동작하는 느낌이 든다.

### NonBlocking-Synchronous
NonBlocking-Sync는 호출되는 함수를 바로 리턴하고, 호출하는 함수는 작업 완료 여부를 계속 신경을 쓰면서 처리를 하는 것이다. 신경을 쓴다는 것은 처리가 완료되기를 기다리거나 지속적으로 물어보는 두 가지가 있는데, NonBlocking 함수를 호출했다면 기다릴 필요는 없고 지속적으로 물어보면 된다.

즉, NonBlocking 함수를 호출 후 바로 리턴받아서 다른 작업을 할 수 있지만, 작업이 완료되지 않았기 때문에 지속적으로 완료 여부를 문의한다.

### Blocking-Async
Blocking-Async는 호출되는 함수가 바로 리턴하지 않고, 호출하는 함수는 작업 완료 여부를 신경쓰지 않는다. Blocking되어 대기하는 상황에서 작업이 끝날 때까지 기다렸다가 결과를 받아서 처리하는 Blocking-Sync방식과 성능적으로 거의 차이가 나지 않는 것처럼 보인다.

Blocking-Async는 별로 이득되는게 없어서 굳이 이 방식을 사용하지는 않지만, NonBlocking-Async를 의도하다가 blocking으로 동작하는 것이 포함되어 있다면 의도와는 다르게 Blocking-Async로 동작하는 경우가 있다고 한다.

참고
https://homoefficio.github.io/2017/02/19/Blocking-NonBlocking-Synchronous-Asynchronous/
https://victorydntmd.tistory.com/8
