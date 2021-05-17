# Tomcat
## Tomcat 구성
### Tomcat을 구성하는 큰 단위로는 3가지가 있다.

>- **Coyote (HTTP Component)** : Tomcat에 TCP를 통한 프로토콜 지원
>- **Catalina (Servlet Container)** : Java Servlet을 호스팅하는 환경
>- **Jasper (JSP Engine)** : 실제 JSP 페이지의 요청을 처리하는 Servlet  

3가지의 구성요소는 다음과 같이 동작한다.
1. HTTP 요청을 Coyote에서 받아서 Catalina로 전달한다.
2. 그러면 Catalina (Servlet Container)에서 전달받은 HTTP 요청을 처리할 웹 어플리케이션 (Context)를 찾고, WEB-INF/web.xml 파일 내용을 참조하여 요청을 전달한다.
3. 요청된 Servlet을 통해 생성된 jsp 파일들이 호출될 때, Jasper (JSP Engine)이 Validation Check / Compile 등을 수행한다.

## Tomcat 구조
<img src="https://media.vlpt.us/images/hyunjae-lee/post/38096013-50e4-40d3-91ac-4f3aea4b399b/image.png">  

- **Tomcat** 은 Java로 작성된 Program이기 때문에 JVM (Java Virtual Machine) 위에서 동작한다.
- **하나의 JVM** 에서 **하나의 Tomcat Instance (Server)가 하나의 Process** 로써 동작한다.
- **하나의 Server** 에는 **여러 개의 Service** 가 존재할 수 있다.
- 각각의 **Service는 1개의 Engine 과 여러 개의 Connector** 로 구성된다.
- **Engine** 은 Catalina Servlet Engine이라고도 불리며, 정의된 Connector로 들어온 요청을 하위에 있는 해당 Host에게 전달해주는 역할을 수행합니다.
- **하나의 Engine** 에는 **여러 개의 Host** 가 존재할 수 있다.
- Host는 가상호스트 이름을 나타내며, 호스트 이름이 곧 url에 매핑된다.
- **하나의 Host** 에는 **여러 개의 Context** 가 존재할 수 있다.
- Context는 하나의 Web Application을 나타내며 주로 *.war 파일의 형태로 배포가 된다.  

    Tomcat Server가 요청을 받으면, Catalina (Tomcat Engine)가 요청에 맞는 Context (Context path)를 찾고, Context는 자신이 설정된 어플리케이션의 deployment descriptor file (web.xml)을 기반으로 전달받은 요청을 서블릿에게 전달하여 처리되도록 한다.

>즉, 클라이언트 HTTP request > Catalina > Context > Servlet > 클라이언트 response 순으로 처리된다.

## Tomcat의 동작 원리
<img src = "https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbsWRgV%2FbtqCLcRPOh4%2FFkmkpG9zxVwYsR5MO2sobK%2Fimg.png">

1. Http Request를 Servlet Container에 전송
2. Servlet Container는 HttpServletRequest, HttpServletResponse 두 객체를 생성
3. 사용자가 요청한 URL을 분석해 어느 서블릿에 대한 요청인지 탐색
4. 만약 해당 서블릿이 한 번도 실행된 적 없거나, 현재 메모리에 생성된 인스턴스가 없다면 새로 인스턴스를 생성하고 init() 메소드 를 실행하여 초기화한 뒤 스레드를 하나 생성
5. 이미 인스턴스가 존재할 경우에는 스레드만 하나 생성 (각 서블릿 인스턴스는 서블릿 컨테이너 당 하나만 존재하기 때문)
6. 컨테이너는 서블릿 service() 메소드를 호출하며, POST, GET 여부에 따라 doGet() 또는 doPost()를 호출
7. 실행된 메소드는 동적인 페이지를 생성한 후 HttpServletResponse 객체에 응답을 보냄
8. 응답이 완료되면 HttpServletRequest, HttpServletResponse 두 객체를 소멸