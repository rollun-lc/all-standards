
RSR-1: Базовые стандарты оформления rollun-com библиотек
=================================================

Данный раздел описывает каким образом должны быть оформлены библиотеки в rollun-com. 
Эти правила и рекомендации должны придерживаться все разработчики библиотек для rollun-com.
Раздел также полезен новым сотрудникам и пользователям, так как им будет легче ориентироваться в проекте, 
зная структуру и правила оформление.

Ключевыми словами «НЕОБХОДИМО» («MUST»), «НЕДОПУСТИМО» («MUST NOT»), «ТРЕБУЕТСЯ» («REQUIRED»), 
«НУЖНО» («SHALL»), «НЕ ПОЗВОЛЯЕТЬСЯ» («SHALL NOT»), «СЛЕДУЕТ» («SHOULD»), «НЕ СЛЕДУЕТ» («SHOULD NOT»), 
«РЕКОМЕНДУЕТСЯ» («RECOMMENDED»), «ВОЗМОЖНО» («MAY») и «НЕОБЯЗАТЕЛЬНЫЙ» («OPTIONAL») в этом документе 
для интерпретации, как описано в [RFC 2119](http://www.ietf.org/rfc/rfc2119.txt) 
([перевод на русский](http://rfc.com.ru/rfc2119.htm)).


### 1 Структура директорий и обязательные файли

Учитывая, определены в этом разделе, требования к оформлению библиотеки можно сформулировать общие правила 
для структурирование директорий, а также указать обязательные файлы.

##### 1.1 Структура файлов/директорий в корневой директории

* НЕОБХОДИМЫЕ директории: `src`, `test`, `example`, `public`, `config`.
* НЕОБХОДИМЫЕ файлы: `.gitignore`, `composer.json`, `README.md`, `CHANGELOG.md`, `LICENSE.md`, `.env`.
* Другие директорий кроме выше указанных НЕДОПУСТИМЫ.

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
└── test/
    └── autoload.php

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
* Для хранения полной документации НЕОБХОДИМО использовать [GitHub Pages](https://pages.github.com/).
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

* Для управления зависимостями проекта нужно использовать `container`.
* В библеотеках в качестве `container` НЕОБХОДИМО использовать только 
[ServiceManager](https://github.com/zendframework/zend-servicemanager).
* ServiceManager НЕДОПУСТИМО использовать кроме как для тестирование и для написания примеров работы библиотеки.
* Все файлы конфигурации для `ServiceManager` НЕОБХОДИМО хранить в `config/autoload` директории 
и подключать их в `config/config.php`.
* Для конфигурирование `ServiceManager` СЛЕДУЕТ использовать библиотеку
[zendframework/zend-config-aggregator](https://github.com/zendframework/zend-config-aggregator)
* Сам `ServiceManager` НЕОБХОДИМО получать из файла `config/container.php`.

##### 3.1 Переменные окружения

* Рабочеее состояние окружение ТРЕБУЕТСЯ определять переменной `APP_ENV`.
* НЕДОПУСТИМО иметь значения `APP_ENV`, кроме как: `dev`, `prod`.
* `debug` режим ТРЕБУЕТСЯ определять переменной `APP_DEBUG`.
* НЕДОПУСТИМО иметь значения `APP_DEBUG`, кроме как: `true`, `false`.
* Переменные `APP_ENV` и `APP_DEBUG` ТРЕБУЕТСЯ определять как переменные окружения 
([environment variable](https://en.wikipedia.org/wiki/Environment_variable)).
* Переменные `APP_ENV` и `APP_DEBUG` по-умолчанию НЕОБХОДИМО хранить в файле `.env` в корне проекта.
* Для подгрузки переменных окружения в библиотеке СЛЕДУЕТ использовать библиотеку 
[symfony/dotenv](https://github.com/symfony/dotenv)

##### 3.2 Configs

* Конфигурационный ключ наивысшего уровня для абстрактной фабрики НЕОБХОДИМО, чтобы задавался константой `KEY` 
этой абстрактной фабрики.
* Все ключи по которым абстрактная фабрика будет забирать конфиги НЕОБХОДИМО, чтобы хранились в константах этой
абстрактной фабрики, поддерживали `psr-1` и иметь префикс `KEY_`.

Пример файла абстрактной фабрики:

```php
<?php

namespace Module\Factory;

use Zend\ServiceManager\Factory\AbstractFactoryInterface;
use Interop\Container\ContainerInterface;

class SomeAbstractFactory implements AbstractFactoryInterface
{
    const KEY = self::class;
    
    const KEY_CLASS = 'class';
    
    const KEY_SOME_DATA_STORE = 'someDataStore';
    
    public function canCreate(ContainerInterface $container, $requestedName){
        // TODO: Implement canCreate() method.
    }

    public function __invoke(ContainerInterface $container, $requestedName, array $options = null) {
        $serviceConfig = $container->get('config');
        
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
* Логику подключения файла с примером НЕОБХОДИМО размещать только в `public/index.php`.
* Рассширение файлов примеров ТРЕБУЕТЬСЯ только `.php`.


### 5. Версионирование

* Название версии НЕОБХОДИМО указывать трема (3) целыми числами разделенными точкой.
* В названии версии НЕДОПУСТИМО указывать что либо кроме трех чисел разделенных точкой.
* Целыми числами НЕОБХОДИМО указывать мажорную версию библиотеки.
* Десятыми НЕОБХОДИМО указывать минорную версию библиотеки.
* Сотыми НЕОБХОДИМО указывать мелкие изменения и фиксы.

Пример:

```
                 ┌───────── мажорная версия
                v1.19.8 
запрещенный ────┘   │ └─── мелкие изменения и фиксы
   символ           └─────── минорная версия
```


### 6. Оформления кода

* Для проверки оформления кода НЕОБХОДИМО использовать [squizlabs/PHP_CodeSniffer](https://github.com/squizlabs/PHP_CodeSniffer)
* Правила для оформления кода НЕОБХОДИМО хранить в файле `phpcs.xml` корневой директории.
* Всем разработчикам библиотеки НЕОБХОДИМО следовать правилам описанным в `phpcs.xml`.


### 7. Config providers

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






