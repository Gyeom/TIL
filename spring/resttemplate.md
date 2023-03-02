# RestTemplate

RestTemplate은 Spring에서 제공하는 HTTP 클라이언트 라이브러리입니다. 다음은 RestTemplate을 사용하여 B서비스를 호출하는 코드 예시입니다.

```java
public class BServiceClient {
    private final RestTemplate restTemplate;

    public BServiceClient(RestTemplate restTemplate) {
        this.restTemplate = restTemplate;
    }

    public <T, R> R callBService(String url, HttpMethod method, T request, Class<R> responseType) {
        HttpHeaders headers = new HttpHeaders();
        headers.setContentType(MediaType.APPLICATION_JSON);

        HttpEntity<Object> httpEntity = new HttpEntity<>(request, headers);

        ResponseEntity<T> responseEntity = restTemplate.exchange(url, method, httpEntity, responseType);

        return responseEntity.getBody();
    }
}
```

위 코드에서 callBService 메서드는 다음과 같은 매개변수를 받습니다.

- url: B서비스의 URL
- method: HTTP 메서드 (GET, POST, PUT, DELETE 등)
- request: 요청 바디
- responseType: 응답 타입
- responseType은 제네릭으로 선언되어 있으므로, 사용할 때 실제 응답 타입을 명시해주면 됩니다.

다음은 위 코드를 활용하여 동기식과 비동기식으로 B서비스를 호출하는 코드 예시입니다.

### 동기식 호출
``` java
BServiceClient bServiceClient = new BServiceClient(new RestTemplate());

MyResponse response = bServiceClient.callBService("http://b-service-url", HttpMethod.GET, null, MyResponse.class);
```

### 비동기식 호출
```java
BServiceClient bServiceClient = new BServiceClient(new RestTemplate());

CompletableFuture<MyResponse> future = CompletableFuture.supplyAsync(() -> bServiceClient.callBService("http://b-service-url", HttpMethod.GET, null, MyResponse.class));

MyResponse response = future.get();
```
