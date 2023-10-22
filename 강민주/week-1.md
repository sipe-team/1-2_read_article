## 1주차

### [Amazon RDS Proxy 를 이용한 스푼라디오 서비스 무중단 변경 | Amazon Web Services](https://aws.amazon.com/ko/blogs/tech/non-disruptive-change-of-spoonradio-service-using-amazonrdsproxy/)

#### 느낀 점

AWS SAA 자격증을 준비하면서 RDS Proxy에 대해 공부했었다. RDS 인스턴스나 Aurora DB 클러스터에 앞단에 위치해 커넥션 관리, 장애 조치 등을 효율적으로 할 수 있게 해주는 서비스라고 생각했다. 그러나 이번 포스팅을 읽으며 Spec Down/Up 시에도 서비스의 중단을 최소화하기 위해 사용될 수 있음을 알 수 있었다.

또한, RDS Proxy에 대한 다른 사실도 알 수 있었는데 아래와 같다.

- IAM 인증을 기반으로 한 RDS Proxy는 인증을 위해 토큰이 사용된다.
- AWS에서 권장하는 아키텍처 패턴은 Lambda + RDS Proxy이다.

<br>

### [Set up highly available PgBouncer and HAProxy with Amazon Aurora PostgreSQL readers](https://aws.amazon.com/ko/blogs/database/set-up-highly-available-pgbouncer-and-haproxy-with-amazon-aurora-postgresql-readers/)

#### 요약

Aurora를 사용해도 (1) SQL의 복잡성과 (2) Reader Enpoint의 라운드 로빈 방식으로 인해 Reader Node의 모든 리소스를 균등하게 배분할 수 없다는 것이다. RDS Proxy를 사용하면 해결할 수 있지만, 커스터마이징을 위해 PgBouncer를 사용하는 기업이 있고, 이를 HAProxy와 결합하여 앞선 문제를 효과적으로 해결할 수 있는 방안을 제시한다.

#### 느낀 점

앞의 포스팅을 읽으며 PgBouncer를 처음 알게 되었고, 관련 글들을 찾다 AWS 블로그 포스팅으로 정하게 되었다. PostgreSQL에 초점이 맞춰진 포스팅이라 지금 당장은 활용할 수 없지만(PostgreSQL 사용해본 적 없음, 사내 기술 스택 아님) 추후에 사용하게 된다면 커넥션 관리 시 두 가지 옵션(PgBouncer, RDS Proxy)에서 고민해볼 수 있을 것 같다.

이번 포스팅을 통해 알게 된 사실은 아래와 같다.

- Aurora Reader Endpoint는 Round-Robin 방식으로 작동하며, 의미 있는 로드밸런싱 값을 얻기 위해 최소 0.5초의 간격을 가지고 DB 세션들이 접속해야 한다. ([Aurora MySQL 밸런싱이 왜 안되지, 뭐가 문제지?](https://techblog.lotteon.com/aurora-mysql-dbms-balancing-%EC%B5%9C%EC%A0%81%ED%99%94-e6aa4a78e932))
- PgBouncer는 커넥션을 관리해주긴 하지만 페일오버와 multi-host 설정을 지원하지 않기 때문에 HAProxy와 결합해 사용하는 솔루션을 제시했다.
