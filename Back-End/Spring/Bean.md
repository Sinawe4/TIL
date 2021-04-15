# Bean
: Spring IOC(Invertion Of Control) 컨테이너가 관리하는 JAVA 객체  
- Spring에서 POJO(plain, old java object)를 ‘Beans’라고 부른다.
- Beans는 애플리케이션의 핵심을 이루는 객체
- Spring IoC(Inversion of Control) 컨테이너에 의해 인스턴스화, 관리, 생성된다.  
> new 연산자로 어떤 객체를 생성했을 때 그 객체는 빈이 아님.  
 ApplicationContext.getBean()으로 얻어질 수 있는 객체가 빈이다.   
즉 Spring에서의 빈은 ApplicationContext가 알고있는 객체, 즉       ApplicationContext가 만들어서 그 안에 담고있는 객체를 의미한다.

## Bean Socpe
- 스프링은 기본적으로 모든 bean을 singleton으로 생성하여 관리한다.
    - 구체적으로는 애플리케이션 구동 시 JVM 안에서 스프링이 bean마다 하나의 객체를 생성하는 것을 의미한다.
    - 그래서 우리는 스프링을 통해서 bean을 제공받으면 언제나 주입받은 bean은 동일한 객체라는 가정하에서 개발을 한다.
    > Singleton으로 생성한 빈을 여러곳에서 공유하여 사용한다, 그 공유한 빈들은 모두 동일한 객체다.
- request, session, global session의 Scope는 일반 Spring 어플리케이션이 아닌, Spring MVC Web Application에서만 사용된다.

<img width=90% src ="https://gmlwjd9405.github.io/images/spring-framework/spring-bean-scope.png">

## Singleton
- singleton’ bean은 Spring 컨테이너에서 한 번 생성되며, 컨테이너가 사라질때 Bean도 사라진다.
- 생성된 하나의 인스턴스는 single beans cache에 저장되고, 해당 bean에 대한 요청과
    참조가 있으면 캐시된 객체를 반환한다.
    - 즉, 하나만 생성되기 때문에 동일한 것을 참조한다.
- 기본적으로 모든 bean은 scope이 명시적으로 지정되지 않으면 singleton이다.
- XML 설정  
    `<bean id="..." class="..." scope="singleton"></bean>`
- annotation 설정  
    대상 클래스에 `@Scope("singletone")`

<img width=90% src ="https://gmlwjd9405.github.io/images/spring-framework/spring-bean-singleton.png">

## Prototype
- prototype’ bean은 모든 요청에서 새로운 객체를 생성하는 것을 의미한다.
    - 즉, prototype bean은 의존성 관계의 bean에 주입 될 때 새로운 객체가 생성되어 주입된다.
    - 정상적인 방식으로 gc에 의해 bean이 제거된다.
    >그냥 매번 Bean이 새로 생긴다고 생각하면 편하다.
- xml 설정
`<bean id="..." class="..." scope="prototype"></bean>`
- annotation 설정
대상 클래스에 `@Scope("prototype")`

<img width=90% src ="https://gmlwjd9405.github.io/images/spring-framework/spring-bean-prototype.png">

## Bean 등록 방법
### XML (Spring)
: applicationContext.xml이라는 파일을 src/main/resources 폴더에 추가시킨 후 bean을 등록한다.
> Java 코드를 이용한 Context 설정이 나오기 전 사용하던 방법이다.
- class(필수): 정규화된 자바 클래스 이름
- id: bean의 고유 식별자
- scope: 객체의 범위 (sigleton, prototype)
- constructor-arg: 생성 시 생성자에 전달할 인수
- property: 생성 시 bean setter에 전달할 인수
- init method와 destroy method
```XML
<!-- A simple bean definition -->
<bean id="..." class="..."></bean>

<!-- A bean definition with scope-->
<bean id="..." class="..." scope="singleton"></bean>

<!-- A bean definition with property -->
<bean id="..." class="...">
	<property name="message" value="Hello World!"/>
</bean>

<!-- A bean definition with initialization method -->
<bean id="..." class="..." init-method="..."></bean>
```
## Java Configuration
: @Configuration이라는 Annotation을 이용하여 XML 대신 Java로 Bean을 생성할 수 있다.
```JAVA
@Configuration
public class ApplicationConfig {
    @Bean
    public Car car(Engine e) {
    	Car c = new Car();
    	c.setEngine(e);
    	return c;
    }
	
    @Bean
    public Engine engine() {
    	return new Engine();
    }
}
```
1. 위 코드처럼 class에 @Configuration을 달고
2. Bean으로 사용할 객체를 반환하는 메소드를 만들고
3. @Bean이라는 어노테이션을 달면 반환된 객체가 Bean Container에 등록된다.
```JAVA
public class ApplicationContextExam03 {
    public static void main(String[] args) {
	    // 클래스를 매개변수로 넣는다.
	    ApplicationContext ac = new AnnotationConfigApplicationContext(ApplicationConfig.class);
		
	    Car car = ac.getBean(Car.class);
	    car.run();
    }
}
```
##  @ComponentScan
: Config 클래스에 @Configuration과 @ComponentScan을 같이 등록하면, 패키지 내의 @Bean, @Component , @Controller, @Service, @Repository로 등록된 클래스를 Classpath Scanning 타임에 Bean Container에 등록시켜 준다.
### 등록방법
@Configuration을 이용하여 Bean 설정 파일(XML 파일을 대체하는)임을 알려주고, @ComponentScan을 이용해 빈으로 등록되기 위한 annotaction이 부여된 클래스들을 자동으로 IoC컨테이너에 등록한다.  
&nbsp;  
`ApplicationConfig`
```JAVA
@Configuration
@ComponentScan
public class ApplicationConfig {}
```
`Application`
```
public class Application {
    public static void main(String[] args) {
        ApplicationContext context = new AnnotationConfigApplicationContext(ApplicationConfig.class);
    }
}
```
Annotaion을 기반으로 Bean들을 등록하기 위해서는 AnnotaionConfigApplicationContext를 이용해야 한다.
그리하여 AnnotationConfigApplicationContext의 매개변수로 Bean설정 클래스인 ApplicationConfig를 넘겨주었다.
### 범위
- `basePackages`의 경우 괄호안에 직접 패키지경로를 직접 적어주어 스캔할 위치를 지정할 수 있다
```JAVA
@Configuration
@ComponentScan(basePackages = "com.mins.spring")
public class ApplicationConfig {}
```
이 경우 **typesafe하지 않아** 조금만 철자가 잘못되더라도 scan을 못하는 오류가 나타날 수 있다.
- `basePackageClasses` 의 경우에는 괄호안에 적힌 Class가 위치한 곳에서부터 모든 어노테이션이 부여된 Class를 bean으로 등록해준다.
```JAVA
@Configuration
@ComponentScan(basePackageClasses = Application.class)
public class ApplicationConfig {}
```
class를 통해 기입하기 때문에 훨씬 **Typesafe한 방법이다.**

