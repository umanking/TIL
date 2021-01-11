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



