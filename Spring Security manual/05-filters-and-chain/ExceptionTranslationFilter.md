```java
package org.springframework.security.web.access;

public class ExceptionTranslationFilter extends GenericFilterBean {
    // Catches AuthenticationException / AccessDeniedException thrown further
    // down the chain and routes to AuthenticationEntryPoint / AccessDeniedHandler.
}
```
