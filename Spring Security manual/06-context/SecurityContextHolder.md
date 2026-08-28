```java
package org.springframework.security.core.context;

public class SecurityContextHolder {

    public static final String MODE_THREADLOCAL = "MODE_THREADLOCAL";

    public static SecurityContext getContext() {
        return SecurityContextHolder.strategy.getContext();
    }

    public static void setContext(SecurityContext context) {
        SecurityContextHolder.strategy.setContext(context);
    }
}
```
Static holder — thread-local by default, so `SecurityContextHolder.getContext().getAuthentication()`
works from anywhere in the request thread (e.g. inside a Controller) without passing it around.
