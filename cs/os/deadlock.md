# 교착상태
프로세스는 실행을 위해 여러 자원을 필요로 한다. 그런데 어떤 자원은 갖고 있으나 다른 자원을 갖지 못할 경우 대기 상태에 들어가서 기다려야 한다.
* 자원은 한정되어 있는데 여러 프로세스가 같이 동작하는 상황이여서 발생하는 문제
* 운영체제가 이러한 자원을 잘 할당해주지 못하면 식사하는 철학자의 문제와 같이 교착상태에 빠질 수 있다.
> 교착상태 : 모든 프로세스가 자원을 가지려고 대기하는 상태

### 교착상태가 일어나는 필요조건
* 상호배타(mutual exclusion)
    * 동기화를 만족시키기 위한 조건
    * 하나의 프로세스가 자원을 사용할 경우 다른 프로세스는 그 자원을 사용할 수 없다.
* 보유 및 대기(hold and wait)
    * 프로세스가 자원을 가지고 있으면서 다른 자원이 오기를 기다리고 있는 것
* 비선점(no preemption)
    * 임의의 프로세스가 자원을 할당 받은 상태에서 다른 프로세스는 이 자원을 뺏어서 사용할 수 없는 형태
* 환형대기(circular wait)
    * 선형이 아니고 원형을 이루게 되어 첫 번째 프로세스와 마지막 프로세스의 자원할당이 겹치게 되어 모든 프로세스가 기다리는 형태

교착상태가 발생하는 원인은 바로 자원이다. 프로세스가 메모리에서 동작할 때 자원에 대한 요청을 운영체제에 전달하게 된다. 운영체제는 이러한 요청을 받아 누구도 자원을 사용하고 있지 않을 경우 자원을 할당 해준다. 그 후 프로세스가 자원을 다 사용하고 나면 반납을 하게 되는 형태를 가진다.

### 교착상태를 처리하는 방법에는 크게 4가지 방식이 있다.

#### 교착상태 방지 방식은 교착상태 4가지 필요조건 중 한 가지 이상을 불만족 시키는 방법

상호배타를 불만족하게 하는 방법
* 하나의 프로세스가 자원을 사용하고 있을 때 다른 프로세스도 자원을 사용가능하게 만드는 방식
* 하지만 동기화의 문제를 만들 수 있어 원척적으로 불가능한 방식
* 교착상태를 없애려다가 더 큰 문제를 발생시킬 수도 있다.

보유 및 대기를 불만족 시키기
* 자원을 가지고 있으면 다른 자원을 기다리지 않게 처리하는 방식
* 일부 자원만 잡고 있는 경우를 없애는 것이다.
* 프로세스는 모든 자원을 가지고 있거나 아니면 자원을 아예 가지고 있지 않는 상태로만 존재하게 만드는 것
* 이런 경우 자원 활용률이 매우 저하되고 더 심각하게는 starvation을 만들 수 있다.

비선점을 불만족 시키는 것
* 선점으로 만들어 주는 것이다.
* 자원이 할당되어 있다고 하더라도 다른 프로세스가 자원을 뺏어올 수 있게 하는 것
* 이런 경우 프로세스를 처리할 때 문제가 발생할 확률이 더 높아진다.
* 프린터라는 자원이라면 프린터에 출력되는 내용이 섞이게 될 것이다.
* 원천적으로 불가능

환형대기를 깨는 방법
* 자원에 번호를 부여하여 번호 오름차순으로 자원을 요청하는 방식
* 교착상태를 방지하는 가장 좋은 방법

#### 교착상태 회피는 운영체제가 자원을 나누어 주는 과정에 대한 문제를 고려하는 방식
운영체제가 자원을 나누어 주는 과정에 대한 문제를 고려하는 방식
* 자원을 어떻게 잘 할당하여 줄 것인가에 대한 방식을 생각하는 것
* 교착상태라고 하는 것은 자원 요청에 대한 잘못된 승인으로 해석한다.
* 자원을 할당해 주었을 때 프로세스들이 교착상태에 빠지지 않도록 운영체제가 잘 나누어 주어야 한다.

#### 교착상태 검출 및 복구 방법
교착상태가 일어나는 것을 허용하고 주기적인 검사를 통해 교착상태 발생 시 복구를 하는 방식
* 검사에 대해서는 계산이나 메모리 사용과 같은 추가적인 부담이 필요
* 복구에 대해서는 프로세스를 일부 강제 종료하거나 자원을 선점하여 일부 프로세스에게 할당하는 방식

#### 교착상태 무시
말 그대로 교착상태가 발생하는 것에 준비를 하지 않는 것
* 교착상태는 실제로 잘 일어나지 않는다.
* 필요조건인 4가지의 조건이 모두 만족하더라도 실제로 교착상태를 잘 일어나지 않는다.
* 만약 일어난다면 모두 꺼버리고 재시동을 하는 방법으로 교착상태를 벗어난다.

참고
* https://copycode.tistory.com/78?category=740133