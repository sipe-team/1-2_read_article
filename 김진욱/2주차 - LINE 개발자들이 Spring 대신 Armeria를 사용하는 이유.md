# 개요
- 레거시 spring 애플리케이션을 armeria로 마이그레이션 하면서 얻었던 인사이트 공유 받기
- 선정이유 - armeria에 대해 간략히나마 알아보기 위함!

# 내용
- 아티클 저자의 마이그레이션 대상 컴포넌트는 라인에서 API 게이트웨이 역할을 맡고 있는 Channel Gateway라는 컴포넌트
- 실제로 내가 개발하고 있는 애플리케이션도 Channel gateway를 사용하고 있음  
<br>

- 기존 Channel Gateway는 Spring MVC로 구성되어 있었는데, 서버의 네트워크를 톰캣으로 처리하고, 업스트림 통신은 Apache HTTPClient를 사용하여 동기 방식 통신 구성
  - 장애로 인해 응답 지연 시간이 길어졌을 때, 해당 장애가 전체 서버 시스템을 마비시키는 경우가 많았음
  - 장애가 발생한 업스트림의 응답을 기다리면서 대기하다가, 톰캣 모든 스레드가 특정 업스트림의 응답을 기다리게 되면서 요청 마비 발생
- 우회 정책을 활용해 보기도 했으나, 리소스 관리 측면에서 그리 좋지 않은 선택이라고 판단, Armeria로 해결해 보고자 시도  
<br>

- 마이그레이션 과정
  - Quick-win
    - Spring boot 애플리케이션에 Armeria의 클라이언트만 추가로 도입하여 사용하는 구조
    - Armeria의 WebClient를 Bean으로 정의하고, 필요한 서비스 레이어에서 클라이언트 주입하여 사용
    - 다양한 레질리언시 기능이 포함된 클라이언트 사용 가능
  - Must-have
    - 기존 톰캣의 네트워크 레이어를 모두 Armeria로 교체하는 구성, 서버의 네트워크 레이어까지 모두 Armeria가 담당
    - Armeria Tomcat 사용
    - gRPC나 Thrift같은 RPC 프로토콜을 비동기로 추가 가능
  - Final-goal
    - Armeria만 사용하는 구성
    - 라우터 레벨, 인터셉터와 필터 등을 모두 Armeria의 데코레이터로 대체하고, 컨트롤러도 AnnotatedService로 대체하는 구성
    - 전체 라이프사이클을 armeria로 비동기적이고 리액티브하게 구성 가능  
<br>

- 마이그레이션 과정 챌린지
  - 기존 블로킹 코드 파악 필요
  - ThreadlLocal에 의존하는 방식의 요청 컨텍스트 관리가 불가능
    - RequestContextHooks 사용
- 마이그레이션 후 성능 변화
  - 고성능이 필요한 API는 Armeria만 사용하도록 구현하고, 그 외 기존 레거시 API는 Tomcat을 사용하도록 설정
  - 지연 시간이 약 25% 감소


# 참고자료
- https://engineering.linecorp.com/ko/blog/hello-armeria-bye-spring