```java
package org.springframework.security.provisioning;

public class InMemoryUserDetailsManager implements UserDetailsManager, UserDetailsPasswordService {

    private final Map<String, MutableUserDetails> users = new HashMap<>();

    @Override
    public UserDetails loadUserByUsername(String username) {
        UserDetails user = users.get(username.toLowerCase());
        if (user == null) {
            throw new UsernameNotFoundException(username);
        }
        return new User(user.getUsername(), user.getPassword(), user.getAuthorities());
    }
}
```
In-memory `UserDetailsService` — good for demos/tests, not real DB-backed apps.
