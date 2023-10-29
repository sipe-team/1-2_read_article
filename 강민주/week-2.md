## 2주차

### [Spring Bean Injection 이야기(feat. 모두가 다 알고 있는 스프링빈, 정말 다 알고 있는가?) | 카카오페이 기술 블로그](https://tech.kakaopay.com/post/martin-dev-honey-tip-2/)

#### 느낀점

개인 블로그에 Spring MVC 시리즈물을 작성하고 있는데, 그 중에 소개한 BeanFactory에 대해 좀 더 자세히 알아보고 싶어 구글링하던 중 카카오페이 테크 블로그를 발견해 선정하였다.

기술적인 부분을 떠나 이 글에서 가장 신선했던 부분은 <<개발자들은 단지 블로그 포스팅 날짜를 보고 최신이라 착각하지만, 실상은 옛날 기술을 답습하곤 한다>>이다. 블로그를 단순히 믿고 바로 적용하기보다는 직접 내부 코드를 까보고 이해하는 것이 중요함을 다시 한 번 리마인드 할 수 있었다.

또한, 스프링에서 빈 주입하는 코드가 DefaultListableBeanFactory의 doResolvedDependency() 메서드에 있다는 것을 알게 되었다. DefaultListableBeanFactory를 자세히 보지 않고 넘어갔는데, 이번 기회에 다시 뜯어볼 수 있었다.

<br>

### [서버에 걸리는 부하, 추측하지 말고 계측하자](https://injae-kim.github.io/dev/2020/07/09/how-to-check-single-server-load-average.html)

#### 느낀점

스터디에서 ‘대규모 서비스를 지탱하는 기술’을 읽었는데

이 포스팅에서 소개된 책 중 하나인 ‘24시간 365일 서버/인프라를 지탱하는 기술’은 읽어보지 못했는데 나중에 스터디에서 한 번 추진해봐야겠다고 생각했다.

또한, 리눅스 커널 코드를 보며 load average가 실제로 어떻게 계산되는지, 원인이 대부분 CPU나 I/O에 있다는 것을 알 수 있었다. 나중에 load average를 직접 계측하고 대응하는 경험을 할 수 있으면 좋겠다.
