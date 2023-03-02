# WebClient

WebClient는 Spring 5부터 도입된 non-blocking HTTP 클라이언트 라이브러리로, 비동기식으로 HTTP 요청을 처리할 수 있습니다. WebClient를 사용하여 B서비스를 호출하는 코드 예시는 다음과 같습니다.

```java
public class BServiceClient {
    private final WebClient webClient;

    public BServiceClient(WebClient webClient) {
        this.webClient = webClient;
    }

    public <T, R> Mono<R> callBService(String url, HttpMethod method, T request, Class<R> responseType) {
        return webClient.method(method)
                .uri(url)
                .contentType(MediaType.APPLICATION_JSON)
                .bodyValue(request)
                .retrieve()
                .bodyToMono(responseType);
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

```java
BServiceClient bServiceClient = new BServiceClient(WebClient.create());

MyResponse response = bServiceClient.callBService("http://b-service-url", HttpMethod.GET, null, MyResponse.class).block();
```

### 비동기식 호출
``` java
BServiceClient bServiceClient = new BServiceClient(WebClient.create());

Mono<MyResponse> responseMono = bServiceClient.callBService("http://b-service-url", HttpMethod.GET, null, MyResponse.class);

responseMono.subscribe(response -> {
    // 처리할 로직
});
```
비동기식 호출의 경우 Mono를 반환하기 때문에 subscribe 메서드를 사용하여 처리할 로직을 등록합니다. 
처리할 로직은 responseMono.subscribe 메서드 안에서 작성합니다. 이 때, subscribe 메서드는 비동기식으로 실행되기 때문에 처리할 로직이 별도의 쓰레드에서 실행됩니다.

또한, Mono의 subscribe 메서드는 반환값이 없기 때문에, 비동기식으로 처리된 결과를 반환하기 위해서는 Mono의 block 메서드를 사용하여 결과를 블록킹하는 방법이 있습니다. 하지만, 이 방법은 blocking I/O를 유발하기 때문에, 가능하면 사용하지 않는 것이 좋습니다. 대신, 비동기식으로 처리된 결과를 다른 비동기식 메서드에게 전달하는 방법을 고려해보는 것이 좋습니다.
