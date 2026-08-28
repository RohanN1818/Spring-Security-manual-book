```java
package org.springframework.security.crypto.password;

public class DelegatingPasswordEncoder implements PasswordEncoder {

    private final String idForEncode;
    private final Map<String, PasswordEncoder> idToPasswordEncoder;

    // encoded passwords are stored as "{bcrypt}$2a$10$..." — the prefix tells
    // this class which PasswordEncoder to delegate matches() to.
}
```
Lets you support multiple encoding algorithms at once (e.g. migrate from one to another over time).
