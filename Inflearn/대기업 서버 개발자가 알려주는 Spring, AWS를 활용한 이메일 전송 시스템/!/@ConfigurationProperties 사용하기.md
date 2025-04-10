
강의에서는 application.yml에서 `@Value(${...secretKey})`를 활용했는데
뭔가 좀더 안전하게 할 수 있는 방법을 생각하다가
JVM -D 를 사용하는 방법을 생각해봤다.

`@Configuration` -> `@ConfigurationProperties`로 바꿔주고

`@EnableConfigurationProperties(SESConfig.class)`
- `@ConfigurationProperties`를 작성한 클래스를 추가해주어야 한다.

setter도 가능하지만 생성자로써 작성하였고

-D..secret-key 를 전달했다.

-D..access-key -D..scret-key 이런식으로 쉼표를 사용해서 여러개를 입력하는게 아니라 그냥 하나하나 입력하는 식으로 전달해야 한다.

제일 좋은 방법이라고 생각된건

OS의 환경변수로 등록하고 yml에서 ${..}로 불러오는 방법이지 않을까 싶다