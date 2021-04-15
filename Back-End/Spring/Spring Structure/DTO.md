# DTO(Data Transfer Object)
##  : DTO(Data Transfer Object)는 데이터 전송(이동) 객체라는 의미를 가지고 있다. DTO는 주로 비동기 처리를 할 때 사용한다.
- **계층간 데이터 교환을 위한 객체(Java Beans)** 이다.  
- **DB의 데이터를 Service나 Controller 등으로 보낼 때 사용하는 객체**  
- **DB의 데이터가 Presentation Logic Tier(다층 구조)로 넘어올때는 DTO로 변환되어 오고가는 것**이다.  
- 로직을 갖고 있지 않는 순수한 데이터 객체이며, getter/setter 메서드만을 갖는다.    
- Request와 Response용 DTO는 View를 위한 클래스
    - 자주 변경이 필요한 클래스
    - Presentation Model
    - Controller Layer에서 Response DTO 형태로 Client에 전달한다.  
- **참고** VO(Value Object) vs DTO  
    - VO는 DTO와 동일한 개념이지만 read only 속성을 갖는다.  
    - VO는 특정한 비즈니스 값을 담는 객체이고, DTO는 Layer간의 통신 용도로 오고가는 객체를 말한다.