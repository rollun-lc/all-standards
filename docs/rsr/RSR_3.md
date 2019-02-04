
RSR-3: Базовые стандарты оформления сервисов
============================================

**Этот стандарт является расширением RSR-1 стандарта**.

Данный раздел описывает каким образом должны быть оформлены сервисы (микросервисы в контексте архитектури)
и другие приложения (далее сервисы) в rollun-com. 
Эти правила и рекомендации должны придерживаться все разработчики сервисов для rollun-com.

Ключевыми словами «НЕОБХОДИМО» («MUST»), «НЕДОПУСТИМО» («MUST NOT»), «ТРЕБУЕТСЯ» («REQUIRED»), 
«НУЖНО» («SHALL»), «НЕ ПОЗВОЛЯЕТСЯ» («SHALL NOT»), «СЛЕДУЕТ» («SHOULD»), «НЕ СЛЕДУЕТ» («SHOULD NOT»), 
«РЕКОМЕНДУЕТСЯ» («RECOMMENDED»), «ВОЗМОЖНО» («MAY») и «НЕОБЯЗАТЕЛЬНЫЙ» («OPTIONAL») в этом документе 
для интерпретации, как описано в [RFC 2119](http://www.ietf.org/rfc/rfc2119.txt) 
([перевод на русский](http://rfc.com.ru/rfc2119.htm)).


##### 1. Переменные окружения

* Для определения сервиса (по сути его названия) НЕОБХОДИМО использовать переменную окружения `SERVICE_NAME`.
* Для опредиления конкретной копии сервиса (pod) НЕОБХОДИМО использовать переменную окружения `POD_NAME`.
* Переменные окружения спицифичны для конкретного сервиса НЕОБХОДИМО описовать а документации к сервису
 в пункте **ПЕРЕМЕННИЕ ОКРУЖЕНИЯ**.
 
(более детально [тут](https://github.com/rollun-com/all-standards/blob/master/docs/rsr/RSR_1.md#31-%D0%BF%D0%B5%D1%80%D0%B5%D0%BC%D0%B5%D0%BD%D0%BD%D1%8B%D0%B5-%D0%BE%D0%BA%D1%80%D1%83%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F))

Пример `.env` файла:
    
```
SERVICE_NAME=rockycart
POD_NAME=rockycart-asc098uqfpi

EBAY_HOST=ebay.com
EBAY_USER=admin
EBAY_PASSWORD=password

APP_ENV=app
APP_DEBUG=true

DB_NAME=app_db
DB_PORT=3306
DB_HOST=app.com
DB_USER=admin
DB_PASS=p@ssw0rd
DB_SETUP=charset=utf8

DB_NAME=app_duplicate_db
DB_PORT=3306
DB_HOST=app.com
DB_USER=root
DB_PASS=
DB_SETUP=charset=latin
```
