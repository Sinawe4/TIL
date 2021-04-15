# DAO(Data Access Object)
## Repository package
- DB를사용해 데이터를 조회하거나 조작하는 기능을 전담하도록 만든 Object  
    실제로 DB에 접근하는 객체이다.
    - Persistence Layer(DB에 data를 CRUD하는 계층)이다.
- Service와 DB를 연결하는 고리의 역할 (Spring 구조 참고)
- SQL를 사용(개발자가 직접 코딩)하여 DB에 접근한 후 적절한 CRUD API를 제공한다.
    - JPA 대부분의 기본적인 CRUD method를 제공하고 있다.
    - `extends JpaRepository<User, Long>`
- JPA 사용시 예시
    ```JAVA
    public interface QuestionRepository extends CrudRepository<Question, Long> {}
    ```
### DAO를 왜 사용하는가?
- 알아보기 쉬운 코드
- 비지니스 객체에 대한 코드 복잡성 절감 효과
- 데이터 엑세스에 대한 접근을 레이어 단위로 분리
- 확장성
- 계층형 구조 디자인이 가능  