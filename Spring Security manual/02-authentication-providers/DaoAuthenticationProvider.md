```java
package org.springframework.security.authentication.dao;

public class DaoAuthenticationProvider extends AbstractUserDetailsAuthenticationProvider {

    private static final String USER_NOT_FOUND_PASSWORD = "userNotFoundPassword";

    private Supplier<PasswordEncoder> passwordEncoder =
            SingletonSupplier.of(PasswordEncoderFactories::createDelegatingPasswordEncoder);

    private volatile String userNotFoundEncodedPassword;

    private final UserDetailsService userDetailsService;

    private UserDetailsPasswordService userDetailsPasswordService = UserDetailsPasswordService.NOOP;

    private CompromisedPasswordChecker compromisedPasswordChecker;

    public DaoAuthenticationProvider(UserDetailsService userDetailsService) {
        this.userDetailsService = userDetailsService;
    }

    @Override
    protected void additionalAuthenticationChecks(UserDetails userDetails,
            UsernamePasswordAuthenticationToken authentication) throws AuthenticationException {
        if (authentication.getCredentials() == null) {
            throw new BadCredentialsException("Bad credentials");
        }
        String presentedPassword = authentication.getCredentials().toString();
        if (!this.passwordEncoder.get().matches(presentedPassword, userDetails.getPassword())) {
            throw new BadCredentialsException("Bad credentials");
        }
    }

    @Override
    protected final UserDetails retrieveUser(String username,
            UsernamePasswordAuthenticationToken authentication) throws AuthenticationException {
        prepareTimingAttackProtection();
        try {
            UserDetails loadedUser = this.userDetailsService.loadUserByUsername(username);
            if (loadedUser == null) {
                throw new InternalAuthenticationServiceException(
                        "UserDetailsService returned null, which is an interface contract violation");
            }
            return loadedUser;
        } catch (UsernameNotFoundException ex) {
            mitigateAgainstTimingAttack(authentication);
            throw ex;
        }
    }
}
```

- Uses `UserDetailsService` to load the user by username from the DB
- Uses `PasswordEncoder` (e.g. BCrypt) to compare raw password vs stored hash in `additionalAuthenticationChecks`
- `USER_NOT_FOUND_PASSWORD` / `mitigateAgainstTimingAttack` exist to make lookups take the same
  time whether the user exists or not, so an attacker can't fingerprint valid usernames from timing (SEC-2056)
