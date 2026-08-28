```java
package org.springframework.security.provisioning;

public class JdbcUserDetailsManager extends JdbcDaoImpl implements UserDetailsManager, GroupManager {
    // Loads users/authorities from a relational DB via JdbcTemplate,
    // using default SQL queries you can override.
}
```
