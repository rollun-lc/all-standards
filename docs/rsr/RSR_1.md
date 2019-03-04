
RSR-1: Базовые стандарты оформления проектов
=================================================

Данный раздел описывает каким образом должны быть оформлены проекты в rollun-com.
Проекты подразумевают библиотеки (открытые библиотеки, абстракции, интерфейсы),
сервисы (закрытые реализации компонентов и абстракций)
и приложения (готовые к развертыванию приложения с конфигам).
Эти правила и рекомендации должны придерживаться все разработчики rollun-com.
Раздел также полезен новым сотрудникам и пользователям, так как им будет легче ориентироваться в проекте, 
зная структуру и правила оформление.

Ключевыми словами «НЕОБХОДИМО» («MUST»), «НЕДОПУСТИМО» («MUST NOT»), «ТРЕБУЕТСЯ» («REQUIRED»), 
«НУЖНО» («SHALL»), «НЕ ПОЗВОЛЯЕТСЯ» («SHALL NOT»), «СЛЕДУЕТ» («SHOULD»), «НЕ СЛЕДУЕТ» («SHOULD NOT»), 
«РЕКОМЕНДУЕТСЯ» («RECOMMENDED»), «ВОЗМОЖНО» («MAY») и «НЕОБЯЗАТЕЛЬНЫЙ» («OPTIONAL») в этом документе 
для интерпретации, как описано в [RFC 2119](http://www.ietf.org/rfc/rfc2119.txt) 
([перевод на русский](http://rfc.com.ru/rfc2119.htm)).


### 1. Структура директорий и обязательные файли

Учитывая определенные в этом разделе требования к оформлению проекта, можно сформулировать общие правила 
для структурирование директорий, а также указать обязательные файлы.

##### 1.1. Структура файлов/директорий в корневой директории

* Временные файлы НЕОБХОДИМО хранить в `data` директории.
* Исполняемые файлы НЕОБХОДИМО хранить в `bin` директории.
* НЕОБХОДИМЫЕ директории: 
    - `src` - директория для хранения основного исходного кода проекта
    - `public` - директория для доступа извне
    - `config` - директория для хранения конфигурационных файлов проекта

* НЕОБХОДИМЫЕ файлы: 
    - `.gitignore`
    - `composer.json`
    - `README.md`
    - `LICENSE.md`
    - `.env` - для хранения [переменных окружения](#31-переменные-окружения)
    - `mkdocs.yml` - файл конфигурации для [mkdocs](#24-readmemd-и-полная-документация)
    - `phpcs.xml` - файл конфигурации для [code sniffer](#5-Оформления-кода)

##### 1.2. Структура файлов/директорий в `public` директории

* В данной директории НЕОБХОДИМО, чтобы находился файл `index.php`,
который является точкой входа в приложение через http(s).

* Стили, шрифты, изображения и js-скрипты, если таковы имеются, НЕОБХОДИМО размещать в папках
`css`, `fonts`, `img` и `js` соответственно.

Пример:

```
┌── .
├── ..
├── config/
│   ├── config.php
│   └── container.php
├── docs/
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
├── mkdocs.yml
├── phpcs.xml
└── README.md
```


### 2. Документация и лицензия

Правила оформления документации к проекту.

##### 2.1. Язык

* СЛЕДУЕТ использовать русский язык для оформления документации. 
* Собственные слова и слова которые более понятны на английском языке РЕКОМЕНДУЕТСЯ писать на английском.

Пример слов которые стоит писать на английском: `batch`, `ConfigProvider`, `callback` (более понятно чем `колбэк`)

##### 2.2. Лицензия

* Для открытых библиотек/сервисов СЛЕДУЕТ использовать [BSD-3-Clause](https://opensource.org/licenses/BSD-3-Clause) лицензию (известную как "New BSD License" или "Modified BSD License").
* В LICENSE.md НЕОБХОДИМО хранить всю информацию о лицензии.
* В начале каждого файла с кодом НЕОБХОДИМО поместить следующий текст:
```
/**
 * @copyright Copyright © 2014 Rollun LC (http://rollun.com/)
 * @license LICENSE.md New BSD License
 */
```

##### 2.3. Документирование изменений

* РЕКОМЕНДУЕТСЯ документировать ключевые и полезные для пользователей изменения в проекте.
* Все документированные изменения РЕКОМЕНДУЕТСЯ хранить в `CHANGELOG.md`.

##### 2.4. README.md и полная документация

* В `README.md` РЕКОМЕНДУЕТСЯ описывать короткую информацию о проекте, ссылку на полну документацию, ссылку на issues.
* Для создания полной документации к проекту НЕОБХОДИМО использовать [mkdocs](https://www.mkdocs.org/).
* Для хранения полной документации РЕКОМЕНДУЕТСЯ использовать [GitHub Pages](https://pages.github.com/).
* GitHub Pages НЕОБХОДИМО создавать с `gh-pages` ветви репозитория.

Структура mkdocs проекта, из которого делается build для создания документации имеет директорию `docs` и 
конфигурационный файл `mcdocs.yml`. Поэтому НЕОБХОДИМО директорию `docs` и файл `mcdocs.yml` хранить
в корневой директории проекта.

Пример файлов конфигурации mkdocs, которые лежат в корневой директории проекта:

```
┌── .
├── ..
├── docs/
│   └── index.md
└── mkdocs.yml
```

* Исходные mkdocs файлы (готовый build) НЕОБХОДИМО хранить в корне проекта в ветке `gh-pages`.

Пример файлов документации в ветке `gh-pages`:

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
 
* В проектах в качестве `container` РЕКОМЕНДУЕТСЯ использовать.
[ServiceManager](https://github.com/zendframework/zend-servicemanager).

* Все файлы конфигурации для `ServiceManager` НЕОБХОДИМО хранить в `config/autoload` директории 
и подключать их в `config/config.php`.

* Для конфигурации `ServiceManager` РЕКОМЕНДУЕТСЯ использовать
[zendframework/zend-config-aggregator](https://github.com/zendframework/zend-config-aggregator).

* Сам `ServiceManager` НЕОБХОДИМО получать из файла `config/container.php`.

##### 3.1. Переменные окружения

* Рабочеее состояние окружение ТРЕБУЕТСЯ определять переменной `APP_ENV`.
* Для обозначение `development`, `production`, `testing` окружений НЕОБХОДИМО использовать `dev`, `prod`, `test` значения.
* НЕ РЕКОМЕНДУЕТСЯ иметь значения `APP_ENV`, кроме как: `dev`, `prod`, `test`.
* `debug` режим ТРЕБУЕТСЯ определять переменной `APP_DEBUG`.
* НЕДОПУСТИМО иметь значения `APP_DEBUG`, кроме как: `true`, `false`.
* Переменные `APP_ENV` и `APP_DEBUG` ТРЕБУЕТСЯ определять как переменные окружения 
* Переменная `OUTPUT_STREAM` для определения потока вывода 
([environment variable](https://en.wikipedia.org/wiki/Environment_variable)).

* Для подгрузки переменных окружения в проекте СЛЕДУЕТ использовать 
[symfony/dotenv](https://github.com/symfony/dotenv).

* Переменные окружения которые НЕОБХОДИМО использовать для настроек баз данных:
    - DB_NAME - название базы данных
    - DB_PORT - порт сервера
    - DB_HOST - хост сервера
    - DB_USER - юзер 
    - DB_PASS - пароль
    - DB_SETUP - команда, которая должна выполниться при подключении
  
    Если нужно определить несколько подключений к базам данных НЕОБХОДИМО использовать в конце переменной индекс номера
    подключения. При этом переменные для первого подключения задаются без указания индекса,
    а все последующие начиная с 1.
    
* Переменные окружения по-умолчанию НЕОБХОДИМО хранить в файле `.env` в корне проекта.

    
Пример `.env` файла:
    
```
APP_ENV=app
APP_DEBUG=true

DB_NAME=app_db
DB_PORT=3306
DB_HOST=app.com
DB_USER=admin
DB_PASS=p@ssw0rd
DB_SETUP=charset=utf8

DB_NAME[1]=app_duplicate_db
DB_PORT[1]=3306
DB_HOST[1]=app.com
DB_USER[1]=root
DB_PASS[1]=
DB_SETUP[1]=charset=latin
```

##### 3.2. Configs

* Конфигурационный ключ наивысшего уровня для абстрактной 'абстрактной фабрики' (AbstractFactoryAbstract) НЕОБХОДИМО, 
задавать константой `KEY` этого класа.

* Все ключи по которым абстрактная фабрика будет забирать конфиги НЕОБХОДИМО хранить в константах этой
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

### 4. Версионирование
Для указания версий НЕОБХОДИМО использовать [SemVer](https://semver.org/lang/ru/).

##### TL;DR
Номер версии выглядит следующим образом: `МАЖОРНАЯ.МИНОРНАЯ.ПАТЧ`. При внесении изменений следует увеличивать:
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


### 5. Оформления кода

* Для проверки оформления кода НЕОБХОДИМО использовать [squizlabs/PHP_CodeSniffer](https://github.com/squizlabs/PHP_CodeSniffer).
* Правила для оформления кода НЕОБХОДИМО хранить в файле `phpcs.xml` корневой директории.
* Всем разработчикам проекта НЕОБХОДИМО следовать правилам описанным в `phpcs.xml`.


### 6. Тестирование

* НЕОБХОДИМО чтобы все тесты находились в `test` директории корневой директории.
* Для `unit` тестирования РЕКОМЕНДУЕТСЯ использовать [phpunit/phpunit](https://github.com/sebastianbergmann/phpunit).


### 7. Config providers

Правила создание и хранение конфигурационных файлов ([config providers](https://docs.zendframework.com/zend-config-aggregator/config-providers/)).

* РЕКОМЕНДУЕТСЯ добавлять ConfigProvider к каждому созданому модулю.
* НЕОБХОДИМО, чтобы ConfigProvider был invokable объектом и был назван `ConfigProvider.php`.
* НЕОБХОДИМО, чтобы ConfigProvider находился в корне _src_ директории соответствующего модуля.
* НЕОБХОДИМО, чтобы модуль имел только один ConfigProvider.
* НЕОБХОДИМО добавлять информацию о каждом созданом ConfigProvider в `composer.json` в раздел _config-provider_.

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


### 8. PHPDoc

Пока что не существует PSR стандарта, который описывает как правильно документировать PHP код.
Есть только адаптированный стандарт документирования Javadoc.
Пока стандарт комментирования имеет лишь формальный статус, однако,
планируется его закрепление в качестве одного из PSR стандартов. Подготавливаемый стандарт получит номер PSR-5.

* До появления PSR стандарта НЕОБХОДИМО использовать правила описанные на
[phpdoc.org](http://docs.phpdoc.org/references/phpdoc/index.html).
* НЕОБХОДИМО использовать PSR стандарт (предположительно PSR-5) для документирования как только он будет опубликован.
