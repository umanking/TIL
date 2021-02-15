

https://docs.spring.io/spring-framework/docs/5.0.6.RELEASE/spring-framework-reference/core.html#spring-core

심심해서 읽는 Spring Framework Documentaion …… 

- ioc는 aop의 기술에 매우 근접해있다. 
- spring에는 자체 aop를 포함하고, 이는 자바 EE에서의 AOP의 80% 커버한다. 



## IoC container

- 컨테이너가 빈을 만들때, Injection 한다.

> service locator pattern?
>
> 

- BeanFactory 인터페이스가 고급 설정 메커니즘을 제공하고, 어떤 타입의 오브젝트도 매니징할수 있다. 
- ApplicationContext는 BeanFactory의 sub-interface 인데, Spring AOP의 특징들과 쉽게 통합할수 있다. 
- 이 챕터에서는 ApplicationContext가 완전 독점적으로 Spring Ioc container를 설명한다.
- 빈? Spring Ioc Conatiner에서 관리되는 Object들을 빈이라고 부른다. 빈들은 configuration metadata에 반영이 된다. (컨테이너에 의해서)

