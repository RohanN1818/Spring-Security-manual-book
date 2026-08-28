```java
package org.springframework.security.web.context;

public interface SecurityContextRepository {

    SecurityContext loadContext(HttpRequestResponseHolder requestResponseHolder);

    void saveContext(SecurityContext context, HttpServletRequest request, HttpServletResponse response);

    boolean containsContext(HttpServletRequest request);
}
```
Persists the `SecurityContext` across requests (e.g. `HttpSessionSecurityContextRepository`
stores it in the HTTP session).
