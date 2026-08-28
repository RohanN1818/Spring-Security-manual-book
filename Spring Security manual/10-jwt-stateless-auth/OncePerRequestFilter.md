```java
package org.springframework.web.filter;

public abstract class OncePerRequestFilter extends GenericFilterBean {

    protected abstract void doFilterInternal(HttpServletRequest request, HttpServletResponse response,
            FilterChain filterChain) throws ServletException, IOException;
}
```
Guarantees the filter's logic runs exactly once per request (Spring's own base class,
not Spring Security's) — the standard base for custom auth filters like JWT.
