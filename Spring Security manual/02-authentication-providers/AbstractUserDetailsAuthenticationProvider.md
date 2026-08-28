```java
package org.springframework.security.authentication.dao;

public abstract class AbstractUserDetailsAuthenticationProvider
        implements AuthenticationProvider, InitializingBean, MessageSourceAware {

    protected abstract void additionalAuthenticationChecks(UserDetails userDetails,
            UsernamePasswordAuthenticationToken authentication) throws AuthenticationException;

    protected abstract UserDetails retrieveUser(String username,
            UsernamePasswordAuthenticationToken authentication) throws AuthenticationException;

    @Override
    public Authentication authenticate(Authentication authentication) throws AuthenticationException {
        String username = determineUsername(authentication);

        UserDetails user = retrieveUser(username, (UsernamePasswordAuthenticationToken) authentication);

        preAuthenticationChecks.check(user);
        additionalAuthenticationChecks(user, (UsernamePasswordAuthenticationToken) authentication);
        postAuthenticationChecks.check(user);

        return createSuccessAuthentication(user, authentication, user);
    }

    @Override
    public boolean supports(Class<?> authentication) {
        return UsernamePasswordAuthenticationToken.class.isAssignableFrom(authentication);
    }
}
```

Handles the shared plumbing (account status checks, building the final `Authentication`) and
delegates the two auth-mechanism-specific steps to subclasses like `DaoAuthenticationProvider`.
