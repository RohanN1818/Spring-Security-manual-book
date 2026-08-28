```java
package org.springframework.security.config.annotation.authentication.builders;

public class AuthenticationManagerBuilder
        extends AbstractConfiguredSecurityBuilder<AuthenticationManager, AuthenticationManagerBuilder> {

    public AuthenticationManagerBuilder userDetailsService(UserDetailsService userDetailsService) { ... }

    public DaoAuthenticationConfigurer<AuthenticationManagerBuilder, UserDetailsService> ...
}
```
Used to wire your custom `UserDetailsService` + `PasswordEncoder` into a `DaoAuthenticationProvider`
under the hood, if you're not just using the auto-configured one.
