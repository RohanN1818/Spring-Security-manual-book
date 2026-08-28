```java
package org.springframework.security.crypto.factory;

public class PasswordEncoderFactories {

    public static PasswordEncoder createDelegatingPasswordEncoder() {
        String encodingId = "bcrypt";
        Map<String, PasswordEncoder> encoders = new HashMap<>();
        encoders.put(encodingId, new BCryptPasswordEncoder());
        encoders.put("pbkdf2", Pbkdf2PasswordEncoder.defaultsForSpringSecurity_v5_8());
        encoders.put("scrypt", SCryptPasswordEncoder.defaultsForSpringSecurity_v5_8());
        // ... more
        return new DelegatingPasswordEncoder(encodingId, encoders);
    }
}
```
This is what `DaoAuthenticationProvider`'s default `passwordEncoder` field points to.
