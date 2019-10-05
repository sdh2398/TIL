# Thread

스레드 구현은 Thread 클래스를 상속받는 방법과 Runnable 인터페이스를 구현하는 방법 두 가지가 있다.
* 기본적으로 Thread 클래스는 Runnable 인터페이스를 구별하는 것이기 때문에 어느 것을 사용해도 거의 차이가 없다.

Runnable 인터페이스를 구현하면 원하는 기능을 추가할 수 있다.
* 해당 클래스를 수행할 때 별도의 스레드 객체를 생성해야되는 단점이 있다.
* 자바는 다중 상속을 인정하지 않아서 상속받을 클래스가 있다면 Runnable 인터페이스를 구현해야 한다.

### Runnable 인터페이스 구현
``` java
public class RunnableImpl implements Runnable {
    public void run() {
        ...
    }
}
```

### Thread 클래스를 확장해서 구현
``` java
public class ThreadExtends extends Tread {
    public void run() {
        ...
    }
}
```

### Thread 실행하기
``` java
public class RunThreads {
    public static void main(String []args) {
        RunnableImpl ri = new RunnableImpl();
        ThreaExtends te = new ThreadExtends();
        new Thread(ri).start();
        te.start();
    }
}
```

### sleep(), wait(), join()
현재 진행 중인 스레드를 대기하도록 하기 위해서는 sleep(), wait(), join() 세 가지 메서드를 사용하는 방법이 있다.

sleep()
* 명시된 시간만큼 해당 스레드를 대기시킨다.

wait()
* Object 클래스에 선언되어 있으므로 어떤 클래스에서도 사용할 수 있다.
* 명시된 시간만큼 해당 스레드를 대기시킨다.
* sleep() 메서드와 다른 점은, 아무 매개변수를 지정하지 않으면 notift()나 notiftAll() 메서드가 호출될 때까지 대기한다.

join()
* 명시된 시간만큼 해당 스레드가 죽기를 기다린다.
* 아무런 매개변수를 지정하지 않으면 죽을때까지 계속 대기한다.

### interrupt(), notify(), notifyAll()

interrupt()
* 스레드를 대기하도록 만드는 3개의 메서드를 모두 멈출 수 있는 유일한 메서드이다.
* interrupt() 메서드가 호출되면 중지된 스레드에는 InterruptedException이 발생한다.

interrupt() 메서드를 호출하여 특정 메서드를 중지시키려고 한다고 해서 항상 메서드가 멈추는 것은 아니다.
* 해당 스레드가 block된 상태에서만 작동한다.
* 해당 스레드가 while(true)와 같은 block된 상태가 아니면 메서드가 멈추지 않는다.


notify(), notifyAll()
* 둘 다 wait(0 메서드를 멈추기 위한 메서드다.
* 이 두 메서드는 Object 클래스에 정의되어 있는데, wait() 메서드가 호출된 후 대기 상태로 바뀐 스레드를 깨운다.
* notify() 메서드는 객체의 모니터와 관련있는 단일 스레드를 깨운다.
* notifyAll() 메서드는 객체의 모니터와 관련 있는 모든 스레드를 깨운다.

출저
* 자바 성능 튜닝 이야기