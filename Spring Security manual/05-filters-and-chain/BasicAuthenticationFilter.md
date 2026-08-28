```java
package org.springframework.security.web.authentication.www;

public class BasicAuthenticationFilter extends OncePerRequestFilter {
    // Parses the "Authorization: Basic <base64>" header,
    // decodes username:password, authenticates via AuthenticationManager.
}
```
