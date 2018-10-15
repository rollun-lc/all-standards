
RSR-1: Базовые стандарты оформления библиотек
=================================================

Данный раздел описывает каким образом должны быть оформлены библиотеки в rollun-com. 
Эти правила и рекомендации должны придерживаться все разработчики библиотек для rollun-com.
Раздел также полезен новым сотрудникам и пользователям, так как им будет легче ориентироваться в проекте, 
зная структуру и правила оформление.

Ключевыми словами «НЕОБХОДИМО» («MUST»), «НЕДОПУСТИМО» («MUST NOT»), «ТРЕБУЕТСЯ» («REQUIRED»), 
«НУЖНО» («SHALL»), «НЕ ПОЗВОЛЯЕТСЯ» («SHALL NOT»), «СЛЕДУЕТ» («SHOULD»), «НЕ СЛЕДУЕТ» («SHOULD NOT»), 
«РЕКОМЕНДУЕТСЯ» («RECOMMENDED»), «ВОЗМОЖНО» («MAY») и «НЕОБЯЗАТЕЛЬНЫЙ» («OPTIONAL») в этом документе 
для интерпретации, как описано в [RFC 2119](http://www.ietf.org/rfc/rfc2119.txt) 
([перевод на русский](http://rfc.com.ru/rfc2119.htm)).


### 1 Структура директорий и обязательные файли

Учитывая, определены в этом разделе, требования к оформлению библиотеки можно сформулировать общие правила 
для структурирование директорий, а также указать обязательные файлы.

##### 1.1 Структура файлов/директорий в корневой директории

* Временные файлы НЕОБХОДИМО хранить в `data` директории.
* Исполняемые файлы НЕОБХОДИМО хранить в `bin` директории.
* НЕОБХОДИМЫЕ директории: `src`, `example`, `public`, `config`.
* Другие директорий кроме выше указанных НЕ РЕКОМЕНДУЮТСЯ.
* НЕОБХОДИМЫЕ файлы: `.gitignore`, `composer.json`, `README.md`, `LICENSE.md`, `.env`, `phpcs.xml`.

##### 1.2 Структура файлов/директорий в `public` директории

* В данной директории НЕОБХОДИМО, чтобы находился файл `index.php`, 
который являеться точкой входа в приложение через http(s).
* `index.php` файл НЕДОПУСТИМО использовать кроме как для запуска [примеров](#4-examples).
* Стили, шрифты, изображения и js-скрипты, если таковы имеються НЕОБХОДИМО размещать в папках 
`css`, `fonts`, `img` и `js` соответсвенно.

Пример:

```
┌── .
├── ..
├── config/
│   ├── config.php
│   └── container.php
├── example
├── public/
│   ├── css/
│   ├── fonts/
│   ├── img/
│   ├── js/
│   └── index.php
├── src/
├── .env
├── .gitignore
├── composer.json
├── composer.lock
├── LICENSE.md
├── phpcs.xml
└── README.md
```


### 2. Документация и лицензия

Правила оформления документации к библиотеке.

##### 2.1 Язык

* СЛЕДУЕТ использовать русский язык для оформления документации. 
* Собственные слова и слова которые более понятны на английском языке РЕКОМЕНДУЕТСЯ писать на английском.

Пример слов которые стоит писать на английском: `batch`, `ConfigProvider`, `callback` (более понятно чем `колбэк`)

##### 2.2 Лицензия

* СЛЕДУЕТ импользовать [MIT](https://opensource.org/licenses/MIT) лицензию.
* В `LICENSE.md` СЛЕДУЕТ хранить всю документацию о лицензии.

##### 2.3 Документирование изменений

* РЕКОМЕНДУЕТЬСЯ документировать ключевые и полезные для пользователей изменения в библиотеке.
* Все изменения РЕКОМЕНДУЕТСЯ хранить в `CHANGELOG.md`.

##### 2.4 README.md и полная документация

* В `README.md` ТРЕБУЕТСЯ описывать короткую информацию о библиотеке, ссылку на полну документацию, ссылку на issues.
* Для создания полной документации к библиотеке НЕОБХОДИМО использовать [mkdocs](https://www.mkdocs.org/).
* Для хранения полной документации РЕКОМЕНДУЕТЬСЯ использовать [GitHub Pages](https://pages.github.com/).
* Файлы конфигурации mkdocs проекта нужна хранить в репозитории (! имя репозитория) в папку с названием библиотеки.

Пример файлов конфигурации mkdocs:

```
┌── .
├── ..
├── docs/
│   └── index.md
└── mkdocs.yml
```

* Исходные mkdocs файлы (готовый build) СЛЕДУЕТ хранить в корне проекта в ветке `gh-pages`.

Пример файлов докуметации в ветке `gh-pages`:

```
┌── .
├── ..
├── css/
├── fonts/
├── img/
├── js/
├── search/
├── 404.html
├── index.html
└── sitemap.xml
```


### 3. Container

* Для управления зависимостями НЕОБХОДИМО использовать `container`.
* В качестве `container` НЕОБХОДИМО использовать реализации
 [Psr\Container\ContainerInterface](https://github.com/php-fig/container/blob/master/src/ContainerInterface.php).
* В библеотеках в качестве `container` РЕКОМЕНДУЕТЬСЯ использовать.
[ServiceManager](https://github.com/zendframework/zend-servicemanager).
* ServiceManager НЕДОПУСТИМО использовать кроме как для тестирование и для написания примеров работы библиотеки.
* Все файлы конфигурации для `ServiceManager` НЕОБХОДИМО хранить в `config/autoload` директории 
и подключать их в `config/config.php`.
* Для конфигурирование `ServiceManager` СЛЕДУЕТ использовать библиотеку
[zendframework/zend-config-aggregator](https://github.com/zendframework/zend-config-aggregator)
* Сам `ServiceManager` НЕОБХОДИМО получать из файла `config/container.php`.

##### 3.1 Переменные окружения

* Рабочеее состояние окружение ТРЕБУЕТСЯ определять переменной `APP_ENV`.
* Для обозначение `development`, `production`, `testing` окружений НЕОБХОДИМО использовать `dev`, `prod`, `test` значения.
* НЕ РЕКОМЕНДУЕТСЯ иметь значения `APP_ENV`, кроме как: `dev`, `prod`, `test`.
* `debug` режим ТРЕБУЕТСЯ определять переменной `APP_DEBUG`.
* НЕДОПУСТИМО иметь значения `APP_DEBUG`, кроме как: `true`, `false`.
* Переменные `APP_ENV` и `APP_DEBUG` ТРЕБУЕТСЯ определять как переменные окружения 
([environment variable](https://en.wikipedia.org/wiki/Environment_variable)).
* Переменные `APP_ENV` и `APP_DEBUG` по-умолчанию НЕОБХОДИМО хранить в файле `.env` в корне проекта.
* Для подгрузки переменных окружения в библиотеке СЛЕДУЕТ использовать библиотеку 
[symfony/dotenv](https://github.com/symfony/dotenv)

##### 3.2 Configs

* Конфигурационный ключ наивысшего уровня для абстрактной 'абстрактной фабрики' (AbstractFactoryAbstract) НЕОБХОДИМО, 
чтобы задавался константой `KEY` 
этой абстрактной фабрики.
* Все ключи по которым абстрактная фабрика будет забирать конфиги НЕОБХОДИМО, чтобы хранились в константах этой
абстрактной фабрики, поддерживали `psr-1` и иметь префикс `KEY_`.

Пример абстрактной 'абстрактной фабрики':

```php
<?php

namespace Module\Factory;

use Zend\ServiceManager\Factory\AbstractFactoryInterface;
use Interop\Container\ContainerInterface;

class SomeAbstractFactoryAbstract implements AbstractFactoryInterface
{    
    const KEY = 'keyExample';
    
    const KEY_SOME_DATA_STORE = 'someDataStore';
    
    public function canCreate(ContainerInterface $container, $requestedName){
        return $container->get('config')[self::KEY][static::class];
    }
}
```

Пример файла абстрактной фабрики:

```php
<?php

namespace Module\Factory;

use Zend\ServiceManager\Factory\AbstractFactoryInterface;
use Interop\Container\ContainerInterface;

class SomeAbstractFactory extends SomeAbstractFactoryAbstract
{    
    const KEY_CLASS = 'class';
    
    const KEY_SOME_DATA_STORE = 'someDataStore';

    public function __invoke(ContainerInterface $container, $requestedName, array $options = null) {
        $serviceConfig = $container->get('config')[self::KEY][self::class];
        
        // Don't forget to check if these key exist
        $class = $container->get($serviceConfig[self::KEY_CLASS]);
        $dataStore = $container->get($serviceConfig[self::KEY_SOME_DATA_STORE]);
        
        return $class($dataStore);
    }
}
```

Пример файла конфигурации:

```php
<?php

use Module\Factory\SomeAbstractFactory;

return [
    SomeAbstractFactory::KEY => [
        SomeAbstractFactory::KEY_CLASS  => 'Module\\SomeClass',
        SomeAbstractFactory::KEY_SOME_DATA_STORE  => 'Module\\DataStore\\SomeDataStoreClass',
    ],
];
```


### 4. Examples

* В библиотеки РЕКОМЕНДУЕТСЯ иметь файлы примеров работы основного функционала.
* Все файлы примеров НЕОБХОДИМО хранить а `example` директории.
* НЕОБХОДИМО иметь возможность запустить каждый файл с примером.
* Доступ ко все файлам примеров НЕОБХОДИМО предоставить только через `public/index.php`.
* Логику подключения файла с примером РЕКОМЕНДУЕТЬСЯ размещать только в `public/index.php`.
* Рассширение файлов примеров ТРЕБУЕТЬСЯ только `.php`.


### 5. Версионирование
Для указания версий НЕОБХОДИМО использовать [SemVer](https://semver.org/lang/ru/).

##### TL;DR
Номер версии выглядит селдующим образом: `МАЖОРНАЯ.МИНОРНАЯ.ПАТЧ`. При внесении изменений следует увеличивать:
* `МАЖОРНУЮ` версию, когда сделаны обратно несовместимые изменения API.
* `МИНОРНУЮ` версию, когда вы добавляете новую функциональность, не нарушая обратной совместимости.
* `ПАТЧ` версию, когда вы делаете обратно совместимые исправления.

Примеры **правильного** версионирования:
* 1.19.8
* 5.0.4
* 2.2.115

Примеры **неправильного** версионирования
* v1.2 (префикс 'v' запрещён)
* 3.5a (любые буквенные значения запрещены)

### 6. Оформления кода

* Для проверки оформления кода НЕОБХОДИМО использовать [squizlabs/PHP_CodeSniffer](https://github.com/squizlabs/PHP_CodeSniffer).
* Правила для оформления кода НЕОБХОДИМО хранить в файле `phpcs.xml` корневой директории.
* Всем разработчикам библиотеки НЕОБХОДИМО следовать правилам описанным в `phpcs.xml`.


### Тестирование

* НЕОБХОДИМО чтобы все тесты находились в `test` директории корневой лиректории.
* Для `unit` тестрирование РЕКОМЕНДУЕТЬСЯ использовать [phpunit/phpunit](https://github.com/sebastianbergmann/phpunit).


### 8. Config providers

Правила создание и хранение конфигурационных файлов ([config providers](https://docs.zendframework.com/zend-config-aggregator/config-providers/)).

* РЕКОМЕНДУЕТСЯ добавлять ConfigProvider к каждному созданому модулю.
* НЕОБХОДИМО, чтобы ConfigProvider был invokable объэктом и был назван `ConfigProvider.php`.
* НЕОБХОДИМО, чтобы ConfigProvider находился в корне _src_ директории соотвествующего модуля.
* НЕОБХОДИМО, чтобы модуль имел только один ConfigProvider.
* НЕОБХОДИМО добавлять информацию о каждном созданом ConfigProvider в `composer.json` в раздел _config-provider_.

Пример `ConfigProvider.php`:

```php
<?php
namespace Module;

class ConfigProvider 
{
    public function __invoke() {
        return [
            'abstract_factories' => [
                //...
            ],
            'aliases' => [
                //...
            ]
        ];
    }
}

```

Пример раздела в `composer.json`:

```
"extra": {
    "zf": {
        "config-provider": [
            "Module\\ConfigProvider"
        ]
    }
}
```






