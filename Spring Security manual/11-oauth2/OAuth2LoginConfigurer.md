```java
http.oauth2Login(oauth2 -> oauth2
    .loginPage("/login")
    .userInfoEndpoint(userInfo -> userInfo
        .userService(customOAuth2UserService)
    )
);
```
Fill in as you actually build an OAuth2 login flow — this folder is a placeholder for now.
