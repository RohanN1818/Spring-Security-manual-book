```java
package org.springframework.security.authentication;

public class BadCredentialsException extends AuthenticationException {
    public BadCredentialsException(String msg) {
        super(msg);
    }
}
```
Thrown by `DaoAuthenticationProvider` when the password doesn't match.
