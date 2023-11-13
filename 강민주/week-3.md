## 3주차

### [Spring WebFlux와 Armeria를 이용하여 Microservice에 필요한 Reactive + RPC 동시에 잡기](https://d2.naver.com/helloworld/6080222)

#### 느낀점

진욱님의 Week2 아티클 ‘LINE 개발자들이 Spring 대신 Armeria를 사용하는 이유’를 보고 Armeria라는 라이브러리에 대해 알아보고 싶어 이번 주차에는 Armeria 관련 포스팅을 읽었다. Spring WebFlux가 비동기 프레임워크라는 것을 알고 있었지만, 실제로 해당 프레임워크를 사용해 프로그래밍을 해 본 경험이 없었다. 이 포스팅을 읽으며 WebFlux의 간단한 예제를 통해 Publisher Object인 Mono와 Flux의 차이점에 대해 알 수 있었고, 왜 Armeria를 사용하면 좋은지에 대해 알 수 있었다.

<br>

### [Armeria를 소개합니다](https://engineering.linecorp.com/ko/blog/introduce-armeria)

#### 느낀점

앞선 포스팅에선 Armeria가 무엇인지, 어떤 장점이 있는지에 대해 개략적으로 알아봤다면 이번 포스팅을 통해서는 Armeria의 3가지 철학에 대해 알 수 있었다. 점진적으로 확장할 수 있고, 여러 기술을 통합할 수 있으며 친근한 커뮤니티를 제공하는 것이다. 여기서 인상깊었던 철학은 통합 철학으로, Decorator라는 추상적 개념을 두어 여러 서비스를 동일한 방식으로 붙일 수 있다는 점이다. 예를 들어, gRPC와 Apache Tomcat을 한꺼번에 작동시킬 수 있다는 것이다.

다만 실제 여러 기술들이 통합된 서버를 구현할 때 코드를 어떻게 구조화하는지 궁금하다. 포스팅의 예시로만 봤을 때는 Server의 빌더 패턴으로 쭉 붙였는데, 그러면 코드의 덩어리가 되지 않을까. 추가로, 나중에 비동기 프로그래밍을 해야 하는 상황이라면 바로 WebFlux로 가는 게 아니라 Armeria도 고려해볼 것 같다.
