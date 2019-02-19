# Spring Scheduler

Spring에서는 작업을 일정한 주기마다 실행시킬 수 있는 Schdule 기능이 있다.
Spring batch만큼 순차작업이나 실패에 따른 복구등의 많은 기능을 가지고 있지는 않지만, 간략한 설정과 어노테이션만으로 편리하게 설정이 가능한 장점을 가지고 있다.

Spring 스케줄러에는 Spring Quartz를 사용하는 방법과 @Scheduled을 사용하는 방법 두 가지가 있다.
Spring Quartz는 @Autowired를 통한 DI가 적용이 안되서 직접 Bean을 찾아 등록해줘야 하는 번거로움이 있어서 다들 @Scheduled를 사용하는 방법을 추천하는 듯하다.

### @Scheduled
Spring 스케줄 작업을 하기 위해선 Configuration클래스에 @EnableScheduling애노테이션을 붙이면 된다.

```
@Configuration
@EnableScheduling
public class SchedulingConfig {
    ...
}
```

@Scheduled애노테이션을 붙인 메소드는 void타입과 어떤 파라미터도 있으면 안된다.
```
@Scheduled
public void scheduleTask() {
    ...
}
```

## fixedDelay
마지막 실행 시간 이후 다음 실행 시간까지의 기간을 고정시킬 수 있다. 작업은 이전 작업이 완료된 후 설정한 시간만큼 대기한다.
이 옵션은 이전 실행이 완료된 후에 다시 실행 해야 할 경우에 사용하며, 하나의 인스턴스만 실행해야 하거나, 종속 작업의 경우에 유용하다.
```
@Scheduled(fixedDelay = 3000)
public void fixedDelayScheduleTask() {
    ...
}
```

## fixedRate
이전 작업의 완료를 기다리지 않고 실행되도록 한다.
각각의 실행이 독립적일 때 사용하는 옵션이고, 메모리와 스레드 풀의 크기가 초과하지 않을 것 같은 작업에 사용할 시 편하다.
하지만 이전 작업이 빨리 완료되지 않으면 OutOfMemoryException이 발생할 수 있다.
```
@Scheduled(fixedRate = 1000)
public void fixedRateScheduleTask() {
    ...
}
```

## initialDelay
해당 작업이 initialDelay 값 이후에 처음 실행되며, 그 다음부터 fixedDelay값에 따라 실행된다.
이 옵션은 작업을 완료해야 되는 설정이 있을 경우에 사용하면 편리하다.

```
@Scheduled(fixedDelay = 3000, initialDelay = 1000)
public void fixedRateAndInitialDelayScheduleTask() {
    ...
}
```

참고
https://skout90.github.io/2017/07/07/Spring/scheduler/
https://www.baeldung.com/spring-scheduled-tasks
https://docs.spring.io/spring/docs/3.2.x/spring-framework-reference/html/scheduling.html
