# Rollun permission

Для авторизации используется два разных протокола в зависимости от клиента. Если клиент - пользователь, тогда 
используется [OAuth 2.0](https://oauth.net/2/), если клиент - сервис, используется
[Basic access authentication](https://en.wikipedia.org/wiki/Basic_access_authentication).
Для реализации аутентификации на стороне сервиса в обеих случаях используеться
[zend-permissions-acl](https://github.com/zendframework/zend-permissions-acl).

Для аутентификации через `Basic access authentication` всем сервисам изначально дается один логин и пароль, и `ACL` по 
умолчанию запрещает доступ.
