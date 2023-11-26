# 개요
- Spring Boot 2에서 Spring Boot 3로 마이그레이션하는 방법에 대해 설명

# 내용
## 목적
- 스프링부트 2 환경의 경우 11월 24일에 EOL 예정, 서비스 정식 오픈 이후에는 대규모 변경 작업이 어렵다는 점을 착안하여 스프링부트 3로 마이그레이션 진행

## 진행
- 순서
  1. 사전 준비
  2. Java 버전을 최소 17 이상으로 업데이트
  3. Spring Boot 버전을 3으로 업데이트
  4. Java EE를 Jakarta EE로 변경
  5. application.yml 혹은 application.properties 수정
  6. 지원이 중단된(deprecated) API 수정

- 사전 준비
  - 가이드 확인
    - [Spring Boot 3 Migration Guide](https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-3.0-Migration-Guide) 
    - [Spring Boot 3.0 Release note](https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-3.0-Release-Notes)
    - [Spring Boot 3.1 Release note](https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-3.1-Release-Notes)
  - 버전이 많이 낮다면, 순차적으로 진행하는 것이 좋음
  - 마이너 버전에도 신규 기능들이 있기 때문에, 확인 필요

- JAVA 버전 업데이트
  - 스프링부트 3에서는 스프링6을 쓰는데, 스프링6가 자바 17부터 지원
  - 명시적으로 자바 버전을 사용하는 부분 수정

- Spring Boot 버전 3로 업데이트
  - 일반적으로 gradle 프로젝트에서 사용하는 플러그인 버전 수정

- Java EE를 Jakarta EE로 변경
  - Java 표준 사양 관리 주체가 JCP에서 Eclipse foundation으로 바뀌면서, 오라클과의 라이선스 이유로 인해 javax가 jakarta 패키지로 변경됨
  - import 문에서 수정 필요
  - IDE의 기능을 사용 후, 한번 더 확인하는 작업을 거치는 것이 편함

- application.properties or application.yml 수정
  - config data의 일부 프로퍼티의 이름이란 뎁수 수정 필요
  - 변경된 프로퍼티 내역
    - 2.7 → 3.0: [Spring Boot 3.0 Configuration Changelog](https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-3.0-Configuration-Changelog)
    - 3.0 → 3.1: [Spring Boot 3.1.0 Configuration Changelog](https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-3.1.0-Configuration-Changelog)
    - IDE의 자동 완성 기능 또는 [spring-boot-properties-migrator](https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-3.0-Migration-Guide#configuration-properties-migration)를 사용하면 편함

- 기타 spring 프로젝트 마이그레이션
  - Spring Cloud
    - Spring Cloud BOM 업데이트
      - [Spring Cloud 2022.0 릴리스 노트](https://github.com/spring-cloud/spring-cloud-release/wiki/Spring-Cloud-2022.0-Release-Notes)
    - 프로퍼티 수정
      - Spring Cloud Gateway: [Spring Cloud Gateway - Appendix A: Common application properties](https://docs.spring.io/spring-cloud-gateway/docs/current/reference/html/appendix.html)
      - Spring Cloud OpenFeign: [Spring Cloud OpenFeign - Appendix A: Common application properties](https://docs.spring.io/spring-cloud-openfeign/docs/current/reference/html/appendix.html)
      - Spring Cloud Vault: [Spring Cloud Vault - Appendix A: Common application properties](https://docs.spring.io/spring-cloud-vault/docs/current/reference/html/#common-application-properties)
    - Spring Cloud Sleuth를 Micrometer Tracing으로 이관
      - 분산 환경에서의 트레이싱 기능의 순환 의존성 문제 해결
      - spring boot 레벨에서 트레이싱 기능 사용 가능
  - Spring Data JPA
    - All-open 설정 수정
    - Hibernate 6.2 변경 사항 파악 및 적용
  - Spring Batch
    - Spring Batch 5 사용
    - 배치 잡 정의 코드 변경
    - 배치 잡 파라미터 전달 방식 개선
    - [Spring Boot 5.0 마이그레이션 가이드](https://github.com/spring-projects/spring-batch/wiki/Spring-Batch-5.0-Migration-Guide)
  - Spring Security
    - Spring Security 6 사용
    - 설정을 한 단계씩 준비하는 것도 좋은 방법
      - Spring Boot를 2.7 버전으로 업데이트하고 Spring Security를 5.8 버전으로 업데이트
      - Spring Security 5.8 버전을 기준으로 6.0 버전으로 업데이트하기 위한 공식 가이드(Preparing for 6.0)를 참고해서 준비
      - Spring Boot 3으로 업데이트한 뒤 공식 가이드(Migrating to 6.0)를 참고해 Spring Security 6.0 버전으로 업데이트
  - 기타(Flyway, Mockito 등)

# 참고문헌
- https://techblog.lycorp.co.jp/ko/how-to-migrate-to-spring-boot-3