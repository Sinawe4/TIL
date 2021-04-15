# IOC(Inversion OF Control) - 제어의 역전
IoC란 Inversion of Control의 약자로 해석하자면 제어의 역전이다.   
: 객체의 생성, 생명주기의 관리까지 모든 객체에 대한 제어권이 바뀌었다는 것을 의미한다.
- 컴포넌트 의존관계 결정 (Component dependency resolution), 설정(configuration) 및 생명주기(lifecycle)를 해결하기 위한 디자인 패턴(Design Pattern)
>어떤 객체가 사용할 객체(의존관계인 객체)를 직접 선언하여 사용하는 것이 아니라,
어떤 방법을 사용하여(ex.생성자 등..)사용하여 주입 받아 사용것 을 IoC의 일부라고 표현 할 수 있다.

**일반적인 제어권**: 자기가 사용할 의존성은 자기가 만들어서 사용
```JAVA
@Service
public class CarService {
	private CarRepository carRepository = new CarRepository();
}
```

### IOC의 장점
- 객체의 **의존성을 역전시켜 객체 간의 결합도를 줄이고 유연한 코드를 작성**할 수 있게 하여 **가독성 및 코드 중복, 유지 보수를 편하게**할 수 있게 한다.

## IOC 분류
### DL(Dependency Lookup) 와 DI(Dependency Injection)
### DL 
: 장소에 저장되어 있는 Bean에 접근하기 위해 컨테이너가 제공하는 API를 이용하여 Bean을 Lookup 하는 것
>의존대상(사용할 객체)을 검색(lookup)을 통해 반환받는 방식  
>--> factory.getBean(id); 내가 찾고자 하는 대상을 검색해서 객체를 확보한다
### DI 
: 각 클래스간의 의존관계를 빈 설정(Bean Definition) 정보를 바탕으로 컨테이너가 자동으로 연결해주는 것
>의존대상(사용할 객체)을 주입을 통해 받는 형식   
>--> Service 계열에서 DAO를 필요로 한다. 즉 의존관계가 있다면  
>Service(DAO) 이것을 의존성을 주입하는 것이다. 
- 1. Setter Injection
- 2. Constructor Injection
- 3. Method Injection
> DL 사용시 컨테이너 종속이 증가하여, 주로 DI를 사용함.

<img width =90% src="https://t1.daumcdn.net/cfile/tistory/99A9A0455C5A74AB20">

## DI(Dependency Injection)를 통한 IoC
```JAVA
@Service
public class CarService {
	
    // CarRepository를 사용은 하지만 만들지는 않는다.
	private CarRepository carRepository;
    /*
    생성자를 통해서 받아온다.
    따라서 의존성을 관리하는 일은 CarService가 하는 일이아니다. 누군가 밖에서 해주는 것이다.
    */
    //생성자를 통한 의존성 주입 
    public CarService(CarRepository carRepository){
    	this.carRepository = carRepository;
    }
}
```
## IoC Container
: Spring Framework는 객체에 대한 생성 및 생명주기를 관리 할 수 있는 기능을 제공한다.

- 객체의 생성을 책임지고, 의존성을 관리
- POJO의 생성, 초기화, 서비스, 소멸에 대한 권환을 가진다
- 개발자들이 직접 POJO를 생성할 수 있지만 컨테이너에게 맡긴다.
### BeanFactory
- Bean을 등록,생성,조회,반환 관리함.
- IoC Container 최상위에 있는 interface
- getBean() 메서드가 정의되어 있다.
- **보통 BeanFactory를 바로 사용하지 않고, 이를 확장한 ApplicationContext를 사용함**
### ApplicationContext
- Bean을 등록,생성,조회,반환 관리하는 기능은 `BeanFactory`와 같다.
- BeanFactory를 상속받는다.
- Spring의 각종 부가 서비스를 추가로 제공한다.  
    리소스 로딩, 이벤트 발생, 다국어 등 추가적인 기능들을 갖고 있다.
    - ResourceLoaderAware's setResourceLoader
    - ApplicationEventPublisherAware's setApllicationEventPublicher
    - MessageSourceAware's setMessageSource
    - ApllicatonContextAware's setApllicationContext
- Spring이 제공하는 ApplicationContext 구현 클래스가 여러 가지 종류가 있다.
<img width = 90% src="https://t1.daumcdn.net/cfile/tistory/9901FF425C5A840432">
## 결론적으로
개발자가 Bean을 직접 만들지 않고 메타데이터(xml, annotation 등..)를 제공하면 프로그램(Spring framework)이 해당 메타데이터를 사용해 Bean객체를 제어 한다.  
즉 IoC Container(문서에는 Spring Bean Container 라고 적성되어있다.) 는 Spring Framework 라고 할 수 있다.  
또한 IoC 컨테이너 안에는 BeanFactory 와 ApplicationContext가 들어가있다. (자세한 차이점은 [BeanFactory](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/beans/factory/BeanFactory.html)와 [ApplicationContext](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/context/ApplicationContext.html)를 참고하자)
