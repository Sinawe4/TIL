# Di(Dependency Injection, 의존성 주입)
## Di란?
### 말 그대로 의존성을 주입시켜주는것.
> 객체를 직접 생성하는 게 아니라 외부에서 생선한 후 주입을 시켜주는 방식.
<img width=90% src="https://t1.daumcdn.net/cfile/tistory/21373937580AEF9B37">

- **일반적인 방법**  
A객체가 B와 C객체를 new() 연산자를 통해 직접 생성하여 사용하는 방법.
- **DI를 사용한 방법**  
외부에서 생선 된 객체를 setter()나 생성자를 통해 사용하는 방법.

## Spring에서 사용하는 DI
<img width=90% src="https://t1.daumcdn.net/cfile/tistory/22535642580C4AF12C">

**Spring 에서는 Bean 컨테이너가 자동으로 DI를 해준다.**  
> 스프링에서 객체는 Bean이라고 하는데, Bean 컨트롤러가 개발자를 대신하여, Bean 을 생성 / 관리 / 제거한다.

## Spring에서 DI의 방법.
### 1. 생성자 주입
    @Component  
    public class SampleController {  
        @Autowired  
        private SampleRepository sampleRepository;  
    }

생성자에 @Autowired 애노테이션을 붙여 의존성을 받을 수 있다.
### 2.필드 주입
    @Component  
    public class SampleController {  
        @Autowired  
        private SampleRepository sampleRepository;  
    }
변수 선언부에 @Autowired 애노테이션을 붙인다.
### 3.Setter 주입
    @Component  
    public class SampleController {  
        private SampleRepository sampleRepository;  

        @Autowired  
        public void setSampleRepository(SampleRepository sampleRepository) {  
            this.sampleRepository = sampleRepository;  
        }  
    }
Setter 메소드에 @Autowired 애노테이션을 붙인다.  
이 세개의 코드는 모두 동일하게 SampleController에 SampleRepository를 주입한다.

## 의존성 주입 애노테이션
### 1. @Autowired
> @Autowired는 주입하려고 하는 객체의 타입이 일치하는 객체를 자동으로 주입한다.

### 2. @Resouce
>@Resource는 주입하려고 하는 객체의 이름(id)이 일치하는 객체를 자동으로 주입한다.

### 3. @Inject
> @Inject는 @Autowired와 유사하게 주입하려고 하는 객체의 타입이 일치하는 객체를 자동으로 주입한다.