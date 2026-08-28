# Request Lifecycle Overview

1. Request comes in
2. `FilterChainProxy` — entry point, delegates to the matching `SecurityFilterChain`
3. `SecurityFilterChain` — ordered list of filters for this app
4. Filters run in order, e.g.:
   - `CsrfFilter`
   - `UsernamePasswordAuthenticationFilter` (or a custom JWT filter)
   - `ExceptionTranslationFilter`
   - `AuthorizationFilter`
5. On success → `AuthenticationManager` → `AuthenticationProvider` → builds `Authentication` → stored in `SecurityContext`
6. If authorized → request reaches the Controller
7. If not → `AuthenticationEntryPoint` / `AccessDeniedHandler`
