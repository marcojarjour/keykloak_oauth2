# the stack

As far as i am aware of, all is setup as described in the documentation, and it works on oauth2-proxy:v7.2.1 but not on v7.3.0 and i could pin point it to the [commit](https://github.com/oauth2-proxy/oauth2-proxy/commit/967051314e5d84cb389aa33ca8e0ff624b43c7eb#diff-b71552ec575796fdd334177b615e4c32eb4fcad92385b4fb808d6fb477744548)

* keycloak
  * http://localhost:8080
  * testclient setuped liked described in the [docs](https://oauth2-proxy.github.io/oauth2-proxy/docs/configuration/oauth_provider#keycloak-auth-provider)
  * testuser `test` with the password `test`
  * admin user `admin` with the password `change_me`
* oauth2-proxy
  * https://localhost:4190
  * setup with `keycloak-oidc`
  * TLS with self signed certificates
* upstream (httpbin)

## howto reproduce

1. start the stack with `docker-compose up -d`
2. open https://localhost:4190 in a private window
3. login with user `test` and password `test`
4. after login open https://localhost:4190/oauth2/userinfo
5. the user field is empty
6. close the private window
7. switch to v7.2.1 with `git checkout works`
8. and repeat the steps 1-4
9. now you see a username
