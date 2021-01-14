# RxJava Programming

## 개념 

- push 방식: 이벤트를 발생시켜서 알려주는것
  - RTC(real time communication )
  - 소켓프로그래밍
  - spring application event 
  - smartphone push message 
- pull 방식: 데이터가 변경된 것부분이 있는지 요청

## 미리 알아야할것 

- Observavble: 데이터 소스
- Operators: 데이터 소스를 처리하는 함수
- Scheduler: 스레드 관리자 
- Subscriber: Observable이 발행하는 데이터를 구독하는 구독자
- functional programming: RxJava 에서 제공하는 연산자(Operator)함수를 사용함 



## 흐름

- 데이터를 발행하고 .. subscribeOn(스케쥴러)
- 데이터를 가공하고
- 데이터를 구독해서 결과를 처리한다.  .. obersveOn(스케줄러)



## Reactive Stream

- 리액티브 프로그래밍 라이브러리 표준사양
- 리액티브 프로그래밍에 대한 인터페이스만 제공
- 4개의 구성요소
  - Publisher: 데이터를 생성, 통지
  - Subscriber: 통지된 데이터를 전달받아서 처리
  - Subscription: 전달받은 데이터의 개수를 요청, 구독을 해지한다. (request, cancel)
  - Processor: publisher, subscriber 기능이 모두 있음



![스크린샷 2021-01-11 오전 9 56 52](https://user-images.githubusercontent.com/28615416/104140187-79c45380-53f3-11eb-90d3-a484f85aa306.png)



## Cold & Hot publisher

- cold: 소비자가 구독할때마다 생산자는 처음부터 새로 통지함 
- hot: 소비자의 수와 상관없이 데이터 한번만 통지
  - 소비자는 발행된 데이터를 구독한 시점부터 전달받는다. 



## 생산자 

- flowable : reactive streams 인터페이스를 구현함 
- observable: reacitve streams 인터페이스를 구현하지 않음 

> 배압? flowable 에서 데이터를 통지하는 속도가 subscriber에서 통지된 데이터를 전달받아 처리하는 속도보다 빠를때 밸런스를 맞추기 위해서 데이터 통지량을 제어하는 기능을 말함 



#### 배압전략 

RxJava에서는 Backpressure stretegy 를 통해서 flowable 이 통지대기중인 데이터를 어떻게 다룰지에 대한 배압전략을 제공한다. 

- buffer 전략
  - drop_latest: 버퍼가 가득 찬 시점에 버퍼내 가장 최근에 버퍼로 들어온 데이터 drop 한다.
  - drop_oldest: 가장 먼저(오래전에) 버퍼로 들어온 데이터를 drop한다.
  - drop: 모두 채워진 상태면, 이후에 생성되는 데이터를 버리고, 버퍼가 비워지는 시점에 drop 되지 않은 데이터부터 다시 버퍼에 담는다. 
- latest 전략 
  - 버퍼에 데이터가 모두 채워진 상태가 되면 버퍼가 비워질때까지 통지된 데이터는 버퍼 밖에서 대기하며 버퍼가 비워지는 시점에 가장 나중에(최근에) 통지된 데이터부터 버퍼에 담는다.



## Single 

- 데이터 1건만 통지하거나 에러를 통지한다. 
- 데이터 통지 자체가 완료를 의미하기 때문에 완료를 통지하지 않는다. 
- onNext, onComplet가 없으며 이둘을 합한 onSuccess를 제공함



## Completable 

- 데이터 생산자이지만 데이터를 1건도 통지하지 않고 -> 완료또는 에러를 통지한다. 
- 데이터 통지의 역할 대신에 Completable 내에서 특정 작업을 수행한후, 해당 처리가 끝났음을 통지하는 역할을 한다. 



# 잠깐, 자바8 짚고 넘어가기

### 함수형 인터페이스

- 단 하나의 추상메서드만 가지고 있는 인터페이스(예외: 디폴트 메서드는 포함할수 있음)
- 함수형 인터페이스 메서드를 람다 표현식으로 작성해서 다른 메서드의 파라미터로 전달할 수 있다. 
- 즉, 람다 표현식 전체를 해당 함수형 인터페이스를 구현한 클래스의 인스턴스로 취급한다. 

### 람다 표현식

- 람다 표현식은 함수형 인터페이스를 구현한 클래스 즉, 익명 클래스의 메서드를 단순화한 표현식

### 함수 디스크립터

- 함수형 인터페이스의 추상메서드를 설명해 놓은 시그니처를 함수 디스크립터라고 한다. 

- java.util.function 패키지로 다양한 새로운 함수형 인터페이스를 지원한다. 

  - | 함수형 인터페이스 | 함수 디스크립터 |
    | ----------------- | --------------- |
    | Predicate<T>      | T -> boolean    |
    | Consumer<T>       | T -> void       |
    | Function<T,R>     | T-> R           |
    | Supplier<T>       | () -> T         |



