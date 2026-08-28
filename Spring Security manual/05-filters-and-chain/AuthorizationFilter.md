```java
package org.springframework.security.web.access.intercept;

public class AuthorizationFilter extends GenericFilterBean {

    private final AuthorizationManager<HttpServletRequest> authorizationManager;

    @Override
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) {
        AuthorizationDecision decision = this.authorizationManager.check(this::getAuthentication,
                (HttpServletRequest) request);
        if (decision != null && !decision.isGranted()) {
            throw new AccessDeniedException("Access Denied");
        }
        chain.doFilter(request, response);
    }
}
```
Modern replacement for `FilterSecurityInterceptor` — the last filter, decides allow/deny.
