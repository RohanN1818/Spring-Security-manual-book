```java
package org.springframework.security.oauth2.client.registration;

public interface ClientRegistrationRepository {

    ClientRegistration findByRegistrationId(String registrationId);
}
```
Holds the config (client-id, secret, scopes, provider URLs) for each OAuth2 provider
you register (Google, GitHub, etc.) — usually populated from application.yml.
