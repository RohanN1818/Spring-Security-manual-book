```java
package org.springframework.security.web;

public class FilterChainProxy extends GenericFilterBean {

    private List<SecurityFilterChain> filterChains;

    @Override
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) {
        List<Filter> filters = getFilters((HttpServletRequest) request);
        if (filters == null || filters.isEmpty()) {
            chain.doFilter(request, response);
            return;
        }
        VirtualFilterChain vfc = new VirtualFilterChain(chain, filters);
        vfc.doFilter(request, response);
    }
}
```
The actual servlet Filter registered with the container. Picks the right `SecurityFilterChain`
for the request URL and runs its filters in order.
