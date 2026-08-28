```java
package org.springframework.security.web;

public interface AuthenticationEntryPoint {

    void commence(HttpServletRequest request, HttpServletResponse response,
            AuthenticationException authException) throws IOException, ServletException;
}
```
Called by `ExceptionTranslationFilter` when an unauthenticated user hits a protected resource
(e.g. redirect to login page, or return 401 for an API).
