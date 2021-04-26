# Gradle 이란?
> Ant와 Maven의 장점을 모아모아 2012년 출시  
> Android OS의 빌드 도구로 채택 됨
- Ant처럼 유연한 범용 빌드 도구 
- Maven을 사용할 수 있는 변환 가능 컨벤션 프레임 워크 
- 멀티 프로젝트에 사용하기 좋음 
- Apache Ivy에 기반한 강력한 의존성 관리
- Maven과 Ivy 레파지토리 완전 지원 
- 원격 저장소나, pom, ivy 파일 없이 연결되는 의존성 관리 지원
- 그루비 문법 사용
- 빌드를 설명하는 풍부한 도메인 모델

## Maven VS Gradle
> Maven에는 gradle과 비교 문서가 없지만, gradle에는 비교문서가 존재.
> Gradle이 시기적으로 늦게 나온만큼 사용성, 성능 등 비교적 뛰어난 스펙을 가지고있다.  
> [Gradle이 Maven보다 좋은점](https://kwonnam.pe.kr/wiki/gradle/from_maven)
- Build라는 동적인 요소를 XML로 정의하기에는 어려운 부분이 많다.
    - 설정 내용이 길어지고 가독성 떨어짐
    - 의존관계가 복잡한 프로젝트 설정하기에 부적절
    - 상속구조를 이용한 멀티 모듈 구현
    - 특정 설정을 소수의 모듈에서 공유하기 위해서는 부모 프로젝트를 생성하여 상속하게 해야 함 (상속의 단점 생김)
- Gradle은 Groovy를 사용하기 때문에, 동적인 빌드는 Groovy 스크립트로 플러그인을 호출하거나 직접 코드를 짜면 된다.
    - Configuration Injection 방식을 사용해서 공통 모듈을 상속해서 사용하는 단점을 커버했다.
    - 설정 주입 시 프로젝트의 조건을 체크할 수 있어서 프로젝트별로 주입되는 설정을 다르게 할 수 있다.

## 적용방법
> Intellij 기준  

- [다운로드](https://gradle.org/releases/)페이지에서 원하는 버전을 다운 받습니다.
- C:\ 에 Gradle 디렉토리를 만들고 그 디렉토리에 다운받은 압축파일을 풀어줍니다.
- 변수 이름에 GRADLE_HOME
    - 변수 값에 C:\Gradle\gradle-7.0 입력
    - 시스템 변수 중 Path 를 선택해서 편집 -> 새로 만들기 %GRADLE_HOME%\bin 추가합니다.
- 명령 프롬프트를 실행해서 gradle -v 입력후 버전 확인
- Intellij 에서 Settings -> Build, Execution, Deployment -> Build Tools -> Gradle -> Gradle user home에 설치경로 지정 -> Generate *.iml files for modules imported from Gradle 체크
- 완료!