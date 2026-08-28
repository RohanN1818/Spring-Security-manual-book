```java
package org.springframework.security.web.csrf;

public final class CsrfFilter extends OncePerRequestFilter {
    // Validates the CSRF token on state-changing requests (POST/PUT/DELETE)
    // against the token stored in session/cookie.
}
```
