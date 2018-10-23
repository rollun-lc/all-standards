
RSR-2: Базовые стандарты оформления библиотек
=================================================

**Этот стандарт является расширением RSR-1 стандарта**.

Данный раздел описывает каким образом должны быть оформлены библиотеки в rollun-com рассширяя RSR-1 стандарт.
Эти правила и рекомендации должны придерживаться все разработчики библиотек для rollun-com.

Ключевыми словами «НЕОБХОДИМО» («MUST»), «НЕДОПУСТИМО» («MUST NOT»), «ТРЕБУЕТСЯ» («REQUIRED»), 
«НУЖНО» («SHALL»), «НЕ ПОЗВОЛЯЕТСЯ» («SHALL NOT»), «СЛЕДУЕТ» («SHOULD»), «НЕ СЛЕДУЕТ» («SHOULD NOT»), 
«РЕКОМЕНДУЕТСЯ» («RECOMMENDED»), «ВОЗМОЖНО» («MAY») и «НЕОБЯЗАТЕЛЬНЫЙ» («OPTIONAL») в этом документе 
для интерпретации, как описано в [RFC 2119](http://www.ietf.org/rfc/rfc2119.txt) 
([перевод на русский](http://rfc.com.ru/rfc2119.htm)).


### 1 Структура директорий и обязательные файли

Учитывая, определены в этом разделе, требования к оформлению библиотеки можно сформулировать общие правила 
для структурирование директорий, а также указать обязательные файлы.

##### 1.1. Структура файлов/директорий в корневой директории

* НЕОБХОДИМЫЕ директории: `example`
* `index.php` файл НЕДОПУСТИМО использовать кроме как для запуска [примеров](#2-examples).


### 2. Examples

* В библиотеки РЕКОМЕНДУЕТСЯ иметь файлы примеров работы основного функционала.
* Все файлы примеров НЕОБХОДИМО хранить а `example` директории.
* НЕОБХОДИМО иметь возможность запустить каждый файл с примером.
* Доступ ко все файлам примеров НЕОБХОДИМО предоставить только через `public/index.php`.
* Логику подключения файла с примером РЕКОМЕНДУЕТЬСЯ размещать в `public/index.php`.
* Рассширение файлов примеров ТРЕБУЕТЬСЯ только `.php`.