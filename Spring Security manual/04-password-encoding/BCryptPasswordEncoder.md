```java
package org.springframework.security.crypto.bcrypt;

public class BCryptPasswordEncoder implements PasswordEncoder {

    private final int strength;

    public BCryptPasswordEncoder() {
        this(-1);
    }

    @Override
    public String encode(CharSequence rawPassword) {
        return BCrypt.hashpw(rawPassword.toString(), getSalt());
    }

    @Override
    public boolean matches(CharSequence rawPassword, String encodedPassword) {
        return BCrypt.checkpw(rawPassword.toString(), encodedPassword);
    }
}
```
