# DTO(Data Transfer Object)
##  : Entity 클래스는 실제 DataBase의 테이블과 1 : 1로 매핑 되는 클래스로, DB의 테이블내에 존재하는 컬럼만을 속성(필드)으로 가져야 한다.  
> Entity 클래스는 상속을 받거나 구현체여서는 안되며, 테이블내에 존재하지 않는 컬럼을 가져서도 안된다.
### Domain Package
- 실제 DB 테이블과 매칭될 클래스
    - @Entity, @Column, @Id 등 사용
- 최대한 외부에서 Entity 클래스의 getter method를 사용하지 않도록 해당 클래스 안에서 필요한 로직 method을 구현
## Entity class 와 DTO class 를 분리해서 관리해야 하는 이유
- View Layer 와 DB Layer의 역활을 철저히 하기위해
- Entity 클래스는 실제 테이블과 매핑되어 만일 변경되게 되면 여러 다른 클래스에 영향을 끼치고, DTO 클래스는 View와 통신하며 자주 변경되므로 분리 해주어야 한다.