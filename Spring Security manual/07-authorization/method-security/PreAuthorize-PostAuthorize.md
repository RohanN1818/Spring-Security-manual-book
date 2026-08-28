```java
// Example usage on a service method:

@PreAuthorize("hasRole('ADMIN')")
public void deleteUser(Long id) { ... }

@PostAuthorize("returnObject.owner == authentication.name")
public Document getDocument(Long id) { ... }
```
Enabled via `@EnableMethodSecurity`. Evaluated by `MethodSecurityExpressionHandler`
using SpEL expressions.
