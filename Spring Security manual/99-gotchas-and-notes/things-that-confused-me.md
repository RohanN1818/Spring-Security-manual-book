# Things that confused me (and then clicked)

- `DaoAuthenticationProvider` doesn't say `implements AuthenticationProvider` directly —
  it's implemented one level up, in `AbstractUserDetailsAuthenticationProvider`. Java interface
  implementation is inherited, so it still counts.
