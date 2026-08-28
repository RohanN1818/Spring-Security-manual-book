```java
package org.springframework.security.authentication;

public class ProviderManager implements AuthenticationManager, MessageSourceAware, InitializingBean {

    private List<AuthenticationProvider> providers = Collections.emptyList();

    private AuthenticationManager parent;

    @Override
    public Authentication authenticate(Authentication authentication) throws AuthenticationException {
        Class<? extends Authentication> toTest = authentication.getClass();
        AuthenticationException lastException = null;
        Authentication result = null;

        for (AuthenticationProvider provider : getProviders()) {
            if (!provider.supports(toTest)) {
                continue;
            }
            try {
                result = provider.authenticate(authentication);
                if (result != null) {
                    copyDetails(authentication, result);
                    break;
                }
            } catch (AuthenticationException ex) {
                lastException = ex;
            }
        }

        if (result == null && parent != null) {
            result = parent.authenticate(authentication);
        }

        if (result != null) {
            return result;
        }

        throw (lastException != null) ? lastException
                : new ProviderNotFoundException("No AuthenticationProvider found");
    }
}
```

The default `AuthenticationManager` implementation — loops through registered `AuthenticationProvider`s,
asks `supports()`, delegates to the first one that can handle the `Authentication` type.
