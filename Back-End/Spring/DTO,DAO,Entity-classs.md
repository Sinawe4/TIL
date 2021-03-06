# Spring 구조 (DTO,DAO,Entity, Controller, Service)
## 전체구조
<img width=90% src="https://gmlwjd9405.github.io/images/spring-framework/spring-package-flow.png">
<img width=90% src="https://t1.daumcdn.net/cfile/tistory/996CA6455B90B6CC4E">

## 기본 동작 순서
Request -> DispatcherServlet -> HandlerMapping -> Controller -> Service -> DAO -> DB  
-> DAO -> Service -> Controller -> DispatcherServlet -> ViewResolver -> View -> Response
- 1. 클라이언트가 Request 요청을 하면 DispatcherServlet이 요청을 가로챕니다.  
이때 DispatcherServlet이 모든 요청을 가로채는건 아니고 web.xml에 <url-pattern>에 등록된 내용만 가로챕니다.
- 2. DispatcherServlet이 가로챈 요청을 HandlerMapping에게 보내 해당 요청을 처리할 수 있는 Controller를 찾습니다.
- 3. 실제 로직 처리 (Controller -> Service -> DAO -> DB -> DAO -> Service -> Controller)
- 4. 로직 처리 후 ViewResolver를 통해 view 화면을 찾습니다.
- 5. View화면을 최종 클라이언트에게 전송합니다.


## DAO(Data Access Object)
repository package
:DB를사용해 데이터를 조회하거나 조작하는 기능을 전담하도록 만든 Object  
실제로 DB에 접근하는 객체이다.
Ser