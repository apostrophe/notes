
- Maven Plugins
  - Surefire - unit tests
  - Failsafe - integration tests 
  - xolstice - protobuf
  - jacoco - runtime agent for tests, allows basic reporting

```java
@Slf4j
log.info("from columnpreset endpoint: [{}]", name);
```
**HTTP Response Codes**
200 OK
201 Created
202 Accepted

301 Moved Permantently
302 Found (Move Temporarily)

400 Bad Request
401 Unauthorized
403 Forbidden
404 Not Found
405 Method Not Allowd

500 Internal Server Error
502 Bad Gateway
503 Service Unavailable

https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status


### Spring Security
https://docs.spring.io/spring-security/reference/index.html

**FilterChains**
1. The `FilterChain` is where filters are registered in a servlet container.
2. Spring's `DelegatingFilterProxy` is used to register filters into the serlet container as `Filter`s, but then the actual implementation is a bean within the `DelegatingFilterProxy` instance that contains the filter implementation.
3. `FilterChainProxy` is a specialized `Filter` for spring security  
4. `FilterChainProxy` uses `SecurityFilterChain`, which contains an ordered list of security-specific filters managed within Spring Security.

```
Filter
DelegatingFilterProxy
    - FilterChainProxy ----- SecurityFilterChain
Filter
Filter
Servlet
```
- https://docs.spring.io/spring-security/reference/servlet/architecture.html
- depending on the url of a request
  - the container creates a FilterChain consisting of
    - exactly one servlet mapped to the request's url
    - 0 or more Filter instances
    - order of filters is important

- creating a `FilterChain`:
    - the `@Configuration` annotation flags this class as something the spring framework should scan in it's building on the application context, where it will create and store all beans
    - by plancing the `@Bean` annotation above the `filterChain` method it's telling spring to create a bean with the name/id of `filterChain` and of type `SecurityFilterChain`
    - the code within the method is a way to configure the authentication (I asked copilot for more examples of this type of configuration, and will list them below)
    - a breakdown of the code:
        - copilot describes `HttpSecurity`[1] as "a fluent builder provided by Spring Security [that can be used] to declare rules that are assembled into a filter chain when .build() is called.
        - 
        - [1] this is actually a bean that's creating automatically(?) within spring that is injected into this method using autowiring(?)
        - the first rule established with `HttpSecurity` is that every request that comes through must be authenticated
            - it must be that if `auth.anyRequest().authenticated()` is false, it must continue through to the next section?
        ```java
        .authorizeHttpRequests(auth -> auth.anyRequest().authenticated())
        ```
        - the next rule indicates what happens next after 
        ```java
        .formLogin(form -> form
            .loginPage("/login")
            .permitAll()
        )
        ```

        ```java
        ```
        ```java
        ```
        ```java
        ```
```java
import org.springframework.security.config.annotation.web.builders.HttpSecurity;

@Configuration
public class SecurityConfig {

    @Bean
    SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
        http
            .authorizeHttpRequests(auth -> auth.anyRequest().authenticated())
            .formLogin(form -> form
                .loginPage("/login")
                .permitAll()
            )
            .logout(logout -> logout
                .logoutUrl("/logout")
                .logoutSuccessUrl("/login?logout")
                .permitAll()
            );
        return http.build();
    }
}
```

the full request flow,per copilot
```
Browser: GET /some-protected-page
  → FilterChainProxy checks SecurityFilterChain
  → No authenticated session → redirect to GET /login

Browser: POST /login (username + password + CSRF token)
  → UsernamePasswordAuthenticationFilter intercepts
  → Calls AuthenticationManager → UserDetailsService
  → On success: creates SecurityContext, stores in HTTP session
  → Redirects to the originally requested URL

Browser: GET /some-protected-page (now with valid session)
  → SecurityContextPersistenceFilter restores SecurityContext from session
  → .anyRequest().authenticated() passes ✓
  → Controller handles request normally
```
- question: is the filterChain method's code, sepcifically the .loginPage("/login"),  dictating where the POST of /login should go? no, the filterChain method is only dictating which pages require which type of restrictions


**Examples of authentication configuration**






- questions/further investigations
  - What are best practices around Exceptions -- when to throw them vs capture them? 
  - Review checked vs unchecked, and how Spring handles these differently.



intellij vm options stored: ~/Library/Application\ Support/JetBrains/IntelliJIdea2025.3/idea.vmoptions