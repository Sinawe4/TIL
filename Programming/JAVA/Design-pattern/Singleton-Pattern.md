# Singleton Pattern
- Singleton 패턴을 사용하는 클래스는, 생성자가 여러차례 호출되더라도 **실제로 생성되는 객체는 하나** 이다.
    - 그 후 호출 된 생성자는 최초 생성자가 생성한 객체를 리턴한다.
### Singleton 패턴을 사용하는 이유
- 만약 우리가 만들었던 DI 컨테이너에서 요청을 할때마다 새로운 객체를 생성한다면, 요청이 많은 사이트에서는 **메모리 낭비가 심하기 때문이다.**

## Singleton 패턴 구현
### 평범한 DI 컨테이너
<img width = 90% src ="https://images.velog.io/images/jaeeunxo1/post/f1209e7c-1e52-4804-989e-9e49477d4cce/image.png">

1. 객체를 생성하면 매번 새로운 객체가 생성된다.
2. 많은 객체를 생성해야 하는 서비스(ex 배달어플, 카카오택시)에서는 메모리 낭비가 많아진다.
### Singleton 패턴 구현
<img width = 90% src ="https://images.velog.io/images/jaeeunxo1/post/2974a719-1c63-46b2-83b3-f71cbba33ccc/image.png">
<img width = 90% src ="https://images.velog.io/images/jaeeunxo1/post/d9063832-6e17-4d7f-8470-ce01b770f31a/image.png">

1. static 객체를 통해서 해당 객체를 1개만 생성할 수 있도록 지정한다.
2. static 메소드를 통해서 외부에서 생성할 수 있도록 제한한다.
3. new 연산자를 통해서 객체를 만드는 것을 private 생성자를 통해서 제한한다.

## Singleton 패턴 문제점
- 전역성을 띄면서 다른 객체와 공동으로 사용할때만 효율적이다
- 싱글톤으로 만든 객체의 역할이 복잡해지면 해당 싱글톤 객체를 사용하는 다른 객체간의 결함도가 높아진다.
>즉, OCP(Open-Close Principle)에 위반된다.
- 싱글톤 객체를 수정할 경우 싱글톤 객체를 사용하는 곳에서 사이드 이팩트 발생 확률이 존재한다.
- 멀티 쓰래드환경에서 동기화 처리 문제가 일어날 수 있다.