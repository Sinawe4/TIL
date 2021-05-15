# Cross-Origin Resource Sharing(CORS)
## CORS란
> Cross-Origin Resource Sharing(CORS)은 추가적인 HTTP header를 사용해서 애플리케이션이 다른 origin의 리소스에 접근할 수 있도록 하는 메커니즘이다.
  하지만 다른 origin에서 내 리소스에 함부로 접근하지 못하게 하기 위해 사용된다.
## CORS가 필요한 이유
>만약 내가 서비스하고 있지 않은 사이트에서 세션을 요청해서 세션을 획득할 수 있다면 해당 사이트는 악의적으로 내 세션을 탈취하거나 다른 행동을 할 수 있기 떄문에 브라우저에서는 이러한 요청을 막는다.  
 피싱사이트가 대표적인 공격 사례인데 이러한 것을 막고 내가 허용한 origin들만 요청할 수 있도록 하기 위해 필요하다.

## CORS의 동작 원리
> 브라우저가 리소스를 요청할 때 추가적인 헤더에 정보를 담는다. 내 origin은 무엇이고, 어떤 메소드를 사용해서 요청을 할 것이고, 어떤 헤더들을 포함할 것인지를 담아서 서버 전송한다.  
서버는 서버가 응답할 수 있는 origin들을 헤더에 담아서 브라우저에게 보낸후, 브라우저가 이 헤더를 보고 해당 origin에서 요청할 수 있다면 리소스 전송을 허용하고 만약 불가능하다면 에러를 발생시킨다.`
