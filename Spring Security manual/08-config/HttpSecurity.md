```java
package org.springframework.security.config.annotation.web.builders;

public final class HttpSecurity extends AbstractConfiguredSecurityBuilder<DefaultSecurityFilterChain, HttpSecurity>
        implements SecurityBuilder<DefaultSecurityFilterChain>, HttpSecurityBuilder<HttpSecurity> {
    // Fluent builder: .csrf(), .cors(), .authorizeHttpRequests(), .formLogin(),
    // .httpBasic(), .sessionManagement(), etc. — each adds/configures a filter.
}
```
