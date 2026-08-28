```java
package org.springframework.security.core.userdetails;

public class User implements UserDetails, CredentialsContainer {

    private final String username;
    private String password;
    private final Set<GrantedAuthority> authorities;
    private final boolean accountNonExpired;
    private final boolean accountNonLocked;
    private final boolean credentialsNonExpired;
    private final boolean enabled;

    public User(String username, String password, Collection<? extends GrantedAuthority> authorities) {
        this(username, password, true, true, true, true, authorities);
    }
}
```
Default `UserDetails` implementation. Usually built via `User.builder()`.
