
# client

新建项目，依赖：`Lombok, Reactive Web`

```java
@Bean
WebClient client() {
    return WebClient.create("http://localhost:8080/movies");
}

@Bean
CommandLineRunner demo(WebClient client) {
    return strings -> {
        client.get()
                .uri("")
                .exchange()
                .flatMapMany(clientResponse -> clientResponse.bodyToFlux(Movie.class))
                .filter(movie -> movie.getTitle().equalsIgnoreCase("A"))
                .subscribe(movie -> client.get()
                        .uri("/{id}/events", movie.getId())
                        .exchange()
                        .flatMapMany(clientResponse -> clientResponse.bodyToFlux(MovieEvent.class))
                        .subscribe(System.out::println));
    };
}
```
# spring security 5

依赖：
- spring-security-webflux
- spring-security-core

有问题
```java
@Bean
ReactiveAuthenticationManager ..() {
    reutnr new UserDetailsRespsontoryAuthenticationManager();
}
@Bean
WebFilter security() {
    http = HttpSecurity.http();
    http.authenticationmanager()
    return htttp.build();
}
```

# Test
```
curl http://localhost:8080/movies

-u username/password
-v

```