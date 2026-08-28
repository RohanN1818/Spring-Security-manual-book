```java
package org.springframework.security.authorization;

public interface AuthorizationManager<T> {

    default void verify(Supplier<Authentication> authentication, T object) {
        AuthorizationDecision decision = check(authentication, object);
        if (decision != null && !decision.isGranted()) {
            throw new AccessDeniedException("Access Denied");
        }
    }

    AuthorizationDecision check(Supplier<Authentication> authentication, T object);
}
```
Modern replacement for `AccessDecisionManager` — decides grant/deny for a request or method call.
