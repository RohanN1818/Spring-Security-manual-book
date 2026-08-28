```java
package org.springframework.security.access;

public class AccessDeniedException extends RuntimeException {
    public AccessDeniedException(String msg) {
        super(msg);
    }
}
```
Thrown by `AuthorizationFilter`/`AuthorizationManager` when an authenticated user lacks permission.
