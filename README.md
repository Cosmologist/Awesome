- [Development](#development)
  - [Resources](#resources)
  - [Constructs](#constructs)
  - [Environment](#environment)
    - [Database](#database)
    - [Database: MySQL](#database-mysql)
    - [Docker](#docker)
    - [Git](#git)
    - [IDE: IntelliJ Jetbrains](#intellij-jetbrains)
    - [Search: Sphinx](#search-sphinx)
    - [Web Server](#web-server)
      - [Nginx](#nginx)
  - [Misc](#misc)
- [PHP Development](#php-development)
  - [Symfony Framework](#symfony-framework)
- [JavaScript Development](#javascript-development)
- [Web Development](#web-development)
  - [JavaScript Compatibility Assurance](#javascript-compatibility-assurance)
  - [CSS Compatibility Assurance](#css-compatibility-assurance)
  - [Chrome DevTools](#chrome-devtools)
- [Multilingual development: Fast dive](#multilingual-development--fast-dive)
  - [Go (Golang)](#go-golang)
  - [Java](#java)
  - [Python](#python)
- [Data Processing](#data-processing)
  - [Theory](#theory)
  - [Sound](#sound)
- [Data Communication](#data-communication)
  - [Network](#network)
- [Workspace](#workspace)
  - [System](#system)
    - [User Management](#user-management)
  - [System: Terminal](#terminal)
  - [System: Utilities](#utilities)
  - [Software](#software)
  - [Software: Telephony](#telephony)

# Development

## Resources
- [LibHunt](https://www.libhunt.com/) Big curruated catalog of useful libraries and resources. It has a convenient ability to compare libraries.

## Constructs
- [Функциональный интерфейс](https://docs.oracle.com/javase/8/docs/api/java/util/function/package-summary.html) (**Functional Interfaces**, **SAM (Single Abstract Method) Interfaces** - интерфейс который содержит **только один метод**.
- [Promise](dev/promise.md) в параллельных вычислениях это подход для извещения о завершении обработки (успешной или нет) и получения результата. ```computeAsync().then(successComputationCallback, failComputationCallback)```.
 
## Environment
### Database

#### Storing Files in a Database
> [I know of no advantages to storing data I want to keep for a long time outside of a database.](https://asktom.oracle.com/pls/apex/f?p=100:11:0%3A%3A%3A%3AP11_QUESTION_ID:1011065100346196442) If it is in the database. I can be sure it is professionally managed, backed up, recoverable (with the rest of the data), secured, scalable (try putting 100,000 documents in a single directory, now, put them in table - which one 'scales' - it is not the directory). I can undelete (flashback) easily. I have locking. I have read consistency.

### Database: MySQL
- [MySQL Workbench](https://www.mysql.com/products/workbench/) The best UI-solution to MySQL administration! And a good data management solution.
- [How the LOAD_FILE() Function Works in MySQL](https://database.guide/how-the-load_file-function-works-in-mysql/) Полезно если LOAD_FILE не работает (возвращает `NULL` вместо содержимого)

#### Текстовый и бинарный протоколы
Текстовый протокол оперирует текстовыми данными, бинарный текстовыми и числовыми.  
Бинарный протокол более эффективен так как:
- данные, которыми происходит обмен, эффективней упакованы (занимают меньше места)
- уменьшает количество операций по приведению типов на сервере и восстановлению (опционально) типов на клиенте

**Важно:** MySQL позволяет использовать бинарный протокол только для при работе с prepared statements.

- [https://dev.mysql.com/doc/internals/en/binary-protocol-value.html]
- High Performance MySQL, O'Relly, page #225

### Docker

#### Cheetsheet
- Собрать образ из Dockerfile: ```docker build . --tag=cosmologist/my-app```
- Запустить образ ```docker run cosmologist/my-app```
- Запуск приложений внутри контейнера
  - Зайти в unix-shell внутри контейнера ```docker run --interactive --tty cosmologist/my-app /bin/bash```, кратко ```docker run -it cosmologist/my-app /bin/bash```, для `alpine` где вместо *bash*->*ash* ```docker run -it cosmologist/my-app /bin/ash```
  
#### Run on VPS/VDS (OpenVZ)
Docker is only supported with OpenVZ 7 (based on 3.x kernel, [see](https://openvz.org/Docker_inside_CT_vz7)) or with OpenVZ 6 with kernel version 042stab105.4 or newer ([see](https://openvz.org/Docker_inside_CT)). ([From](https://stackoverflow.com/posts/35951482/revisions))

### Git
- [Pretty git log](http://garmoncheg.blogspot.com/2012/06/pretty-git-log.html)
- [Как удалить из репозитория файлы которые больше не надо трекать (к примеру после измений в .gitignore)](http://www.codeblocq.com/2016/01/Untrack-files-already-added-to-git-repository-based-on-gitignore/): `git rm -r --cached . && git add . && git commit -m ".gitignore fix"`


### IDE
#### IntelliJ Jetbrains
- Показывать `.dot`-файлы и директории в навигаторе `Preferences | File Types | Ignore files and folders`
- Показывать директорию `.idea` в навигаторе `Maintenance (Ctrl+Shift+Alt+/) | Registry | projectView.hide.dot.idea` + перезапуск Idea
- [Как хранить настройки IDE в репозитории вместе с проектом](https://intellij-support.jetbrains.com/hc/en-us/articles/206544839)
  - [Jetbrains.gitignore](https://github.com/github/gitignore/blob/master/Global/JetBrains.gitignore)
 - [Script to reset PHPStorm trial (evaluation) on windows machine](https://gist.github.com/midlan/6a08db14569c409c9c2b9ecb548380f6)
 - [Reset Webstorm/Phpstorm trial on Linux (Ubuntu)](https://gist.github.com/bTokman/620c0f6b541b00c2835c18319bc0963d) - [Важный комментарий](https://gist.github.com/bTokman/620c0f6b541b00c2835c18319bc0963d#gistcomment-2892793)
 
### Search: Sphinx
- При обращении к Sphinx через SphinxQl необходимо дополнительно экранировать ряд символов (не входят в стандарт SQL, используются в `Extended Syntax` для Sphinx) в строковых параметрах, иначе может привести к SQL-инъекции, невалидному запросу (ошибка вида `Unexpected character '/'`) и тп. [Обсуждение](http://sphinxsearch.com/forum/view.html?id=13619#57465), [Реализация для PHP](https://github.com/romainneutron/Sphinx-Search-API-PHP-Client/blob/master/sphinxapi.php#L1511)
  
### Web Server
- [Online HTTP/2 test - Verify if your server or CDN supports HTTP/2](https://tools.keycdn.com/http2-test)

## Misc

[Naming for Adapter Pattern](https://softwareengineering.stackexchange.com/questions/361777/how-to-name-different-components-in-adapter-pattern) - good name option is **FooFromBar** or **FooFromBarAdapter**.  

Terms **Routine**, **Subroutine**, **Function**, **Procedure**, **Method**, **Coroutine**
- **Routine** (**программа**) - общее название блока кода. Программа, библиотека, модуль, процедура, функция и тп.
- **Subroutine** (**подпрограмма**) - блок кода находящийся внутри другого блока кода.
- **Function** (**функция**) - блок кода (subroutine) который умеет возвращать данные.
- **Procedure** (**процедура**) - блок кода (subrotine) который не умеет ничего возвращать.
- **Method** (**метод**) - функция или процедура в составе объекта.
- **Coroutine** (**сопрограмма**) - блоки кода (subroutine) которые могут выполняться асинхронно, можно перключаться между ними (сохраняется состояние (контекст) одного блока, вызывается другой, при возврате управления контекст восстанавливается и продолжается выполнение первого). Corutine существуют только внутри одного общего системного потока, другими словами это реализация многозадачности на уровне языка (не операционной системы). Еще хорощий пример - генераторы (yeld).

Links: 
 - [What is meant by routines in C++?](https://www.quora.com/What-is-meant-by-routines-in-C++)
 - [What are “routines” in programming?](https://www.quora.com/What-are-%E2%80%9Croutines%E2%80%9D-in-programming)
 - [What's the technical definition for “routine”?](https://stackoverflow.com/posts/6885971/revisions)
 - [Сопрограммы (корутины, coroutine) - что это?](https://ru.stackoverflow.com/questions/496002/%D0%A1%D0%BE%D0%BF%D1%80%D0%BE%D0%B3%D1%80%D0%B0%D0%BC%D0%BC%D1%8B-%D0%BA%D0%BE%D1%80%D1%83%D1%82%D0%B8%D0%BD%D1%8B-coroutine-%D1%87%D1%82%D0%BE-%D1%8D%D1%82%D0%BE )
 - [Coroutine, для чего они нужны?](https://toster.ru/q/405733)

# PHP Development

## Language
### Extend
- [Pre](https://preprocess.io/) is a PHP preprocessor, designed to make adding new syntax effortless. Flexible integration via Composer
- [PHP Enum](https://github.com/myclabs/php-enum) грамотная реализация для типа *Enum*. Есть сторонние расширения для интеграции типа с *Doctrine* и *ParamConverter*.

### Tips
- **Оператор `+`** adds items from right-hand array to the left-hand array, only the keys of which are missing in the left-hand array (associative or indexed keys).  Use case: building a config array, where the left-hand array contains only changed parameters, and the right-hand array contains all possible parameters with default values.
- **Оператор эффективней функции** (при одинаковом исполняемом коде конечно-же), так как функция более высокоуровневый элемент языка и ее вызов требует дополнительных накладных расходов. К примеру, [`$array[]` быстрее `array_push`](https://stackoverflow.com/posts/559859/revisions) примерно в два раза.

## Resources
- [Awesome PHP](https://php.libhunt.com/) A curated list of awesome PHP libraries and resources
- [marcelgsantos/learning-oop-in-php](https://github.com/marcelgsantos/learning-oop-in-php) A collection of resources to learn object-oriented programming and related concepts for PHP developers.

## Libraries
- [K-Phoen/rulerz](https://github.com/K-Phoen/rulerz) Powerful implementation of the Specification pattern in PHP
- [nette/utils](https://github.com/nette/utils) Lightweight utilities for string & array manipulation, image handling, safe JSON encoding/decoding, validation, slug or strong password generating etc
- [danielstjules/Stringy](https://github.com/danielstjules/Stringy) A PHP string manipulation library with multibyte support
- [wapmorgan/Morphos](https://github.com/wapmorgan/Morphos) Морфологическая библиотека для английского и русского языков. Умеет склонять, делать плюрализацию (склонение множественного), конвертировать значения в текст (валюта, числа, временные интервалы), подбирать предлоги и окончания

## Environment

### Debug
#### Trigger breakpoint for all exceptions [PhpStorm]h
*Run -> View Breakpoints -> Add (PHP Exception Breakpoints) -> Enter Exception FQCN "Exception"*
![Catch the global exception](https://github.com/Cosmologist/Awesome/blob/master/images/phpstorm-global-exception-breakpoint.png?raw=true)

##### Exclude certain exceptions
- Ignored breakpoint should be exist (inline or via *PHP Exception Breakpoints*) and have uncheked *Suspend* flag
- Select *Any* value (or a specific breakpoint/group of breakpoints) for the "Disable breakpoint until is hit" option of global exception breakpoint.

### WebServer
#### CGI, FastCGI, PHP-FPM
- **CGI** устаревший протокол взаимодействия между веб-сервером и приложениями (скриптами), общение ведется только через STDIN/STDOUT, на каждый запрос создается отдельный процесс приложения, который умирает после ответа.  
- **FastCGI** общение ведется через сокеты или TCP (что дает возможность разнести сервер и приложение), предполагается наличие FastCGI-менеджера, который заранее подготоваливает пул процессов приложения, что позволяет значительно быстрее отдать запрос на обработку. Реализация FastCGI-менеджера может быть встроена в сервер (Apache) или нет (Nginx).  
- **PHP-FastCGI** устаревшая реализация FastCGI встроенная в интерпретатор. В отличие от PHP-FPM - и для CLI (CGI) и для FastCGI использовался общий интерпретатор, для запуска PHP в режиме FastCGI сервиса использовался аргумент ```--bindpath``` в который пробрасывался путь к сокету или TCP-адрес на который биндился FastCGI-менеджер.  
- **PHP-FPM** (FastCGI Process Manager) это современная улучшенная реализация *FastCGI* встроенная в интерпретатор PHP с рядом новых возможностей.

Links:
 - [PHP-FPM, application server made by PHP](https://publications.jbfavre.org/web/php-fpm-apps-server-nginx.en)
 
### Database

[Good explanation of PDO_MYSQL](http://blog.ulf-wendel.de/2008/pdo_mysqlnd-the-new-features-of-pdo_mysql/)
 
#### Нативные типы значений, вместо только строковых, в результатах запросах к MySQL через PDO
MySQL должен передавать данные без изменений, по бинарному протоколу, так как PDО не знает их исходный тип.
Бинарный протокол доступен только при работе с подготовленными выражениями, которые PDO по-умолчанию эмулирует.
```php
// Отключаем эмуляцию
$pdo->setAttribute(PDO::ATTR_EMULATE_PREPARES, false);
// Для PDO дополнительно нужно
$pdo->setAttribute(PDO::ATTR_STRINGIFY_FETCHES, false);
```

# Symfony Framework
## Resources
- https://github.com/sitepoint-editors/awesome-symfony

## Recipes
### Как ввести многострочный текст в YAML-файле
```yaml
# app/config/config.yml
appbundle:
  myservice:
    description: > 
                   This is a 
                   multiline text
```

### Как получить definition сервиса из Extension с включенным autowire
До Symfony 3.3 сервисы загружались вручную (```$loader->load('services.yml');``` и попадали сразу в контейнер, с включенным autowire этого не происходит и это логично, при попытке получить definition *$containerBuilder->getDefinition('myservice')* будет возникать ошибка вида *"You have requested a non-existent service"*. 
Если надо обратиться к definition сервиса, к примеру, чтобы вызвать *addMethodCall*, надо у ContainerBuilder вызвать метод *register*.
```php
$mailboxRegistryDef = $container->register(MailboxRegistry::class);
$mailboxRegistryDef->addMethodCall('add', [$name, $options]);
```

### Как добавить свой тег для autoconfigure
```php
# DependencyInjection\AppExtension.php
$container->registerForAutoconfiguration(FooInterface::class)->addTag('foo.bar');
```
или
```yml
# services.yml
services:
  _instanceof:
    App\Foo\FooInterface:
      tags: ['foo.bar']
```

## Libraries
- **Asset**: Автоматическая генерация версии ассетов (*assets_version*) по хэшу от содержимого. По-умолчанию Symfony предлагает только ручное изменение версии. [Incenteev/hashed-asset-bundle](https://github.com/Incenteev/hashed-asset-bundle)
- [VRiaEnhancedFileBundle](https://github.com/vria/enhanced-file) замена стандартного Symfony Form FileType, с поддержкой режима *Update* и автоматической загрузкой. Стандартный FileType этого не умеет, а в документации этот момент не освещен, не смотря на то, что он не прозрачный и требует знаний Symfony Form internals.  Автора бандла написал [отличную статью](https://vria.eu/news/2016/4/10/creating-enhanced-file-type-for-symfony-forms) на эту тему.

# JavaScript Development
## JQuery
- http://youmightnotneedjquery.com/

## Libraries
- https://github.com/josephschmitt/Clamp.js

# Web Development

## Resources
- [Web Fundamentals](https://developers.google.com/web/fundamentals/) Google's opinionated reference for building amazing web experiences.

## Javascript

## Производительность
### Resources
- https://developers.google.com/web/fundamentals/performance/why-performance-matters/
- https://bitsofco.de/understanding-the-critical-rendering-path/
- https://m.habr.com/ru/company/badoo/blog/322988/

### Что такое Critical Rendering Path (CRP)
Это набор действий совершаемых браузером до старта отрисовки страницы на экране
> 1. Constructing the DOM Tree
> 2. Constructing the CSSOM Tree
> 3. Running JavaScript
> 4. Creating the Render Tree
> 5. Generating the Layout
> 5. Painting

### Как проверить производительность
- [Google Lighthouse](https://developers.google.com/web/tools/lighthouse/) для аудита производительности. Доступен как расширение для Chrome, в виде cli-приложения, как модуль для Node и как часть сервиса [Google PageSpeed Insights](https://developers.google.com/speed/pagespeed/insights/).

### Как увеличить производительность
- Загружать внешние скрипты асинхронно с помощью добавления аттрибута *defer*  в тег *script* - не блокируется парсинг *DOM*, быстрее чем синхронный режим.

#### JavaScript Blocking

##### Resources
- https://flaviocopes.com/javascript-async-defer/

##### Как JavaScript блокирует парсинг страницы
> Браузер формирует узлы DOM/ CSSOM до тех пор, пока не встретит внешние или внутренние скрипты JavaScript.
> Cкрипт может захотеть получить доступ к предшествующим элементам DOM и CSSOM, поэтому браузер приостанавливает парсинг узлов (парсинг DOM блокируется), загружает его (если скрипт вншний) и исполняет, а затем возобновляет парсинг.

##### Как избежать блокировки страницы JavaScript'ом
Использовать асинхронную загрузку скриптов через аттрибуты тега *async* и *defer*, что позволяет избежать блокировок.

##### Чем отличаются аттрибуты async и defer
- *async*
  - загружается асинхронно - нет блокировки парсера
  - выполняется сразу после его загрузки - парсер блокируется на время выполнения
  - не соблюдается последовательность выполнения
- *defer*
  - загружается асинхронно - нет блокировки парсера
  - выполняется после завершения загрузки *DOM* (событие *DOMDocumentLoaded*) - нет блокировки парсера
  - соблюдается последовательность выполнения
  - поддерживается в старых браузерах
  
 ##### Разное
 - *async* и *defer* не имеют смысла для inline-скриптов

### Обеспечение совместимости с браузерами
#### Конвертировать код с помощью транспилера. 
**Транспилер** перегенирирует код с использованием только фиксированного набора языковых конструкций, поддержка которых есть в каждом бразуре, в котором приложение должно работать.

##### Babel Transpiler
[Babel](https://babeljs.io/docs/en/usage) is the most famous and popular transpiler.
```
# Install
npm install @babel/core @babel/cli @babel/preset-env

# Run via CLI
./node_modules/.bin/babel web/js/your-file.js --out-file script-compiled.js --presets=@babel/env
```
[@babel/preset-env](https://babeljs.io/docs/en/babel-preset-env) - most popular preset. Processes JS-scripts to achieve compatibility with a specified set of browsers (see the browserlist to specify set of browsers).

#### Providing polyfills for unsupported browser features
##### Polyfill
Polyfill is a workaround for the specific missed feature.
###### [Loading Polyfills Only When Needed](https://philipwalton.com/articles/loading-polyfills-only-when-needed/)
The idea is to manually check and then dynamically load the polyfill.: ```if (!window.fetch) { loadScript('fetchPolyfill.js'); }```

#### Useful
##### Check you website for compatibility issues
- [SortSite](https://www.powermapper.com/products/sortsite/checks/browser-compatibility/).
##### Notify users with non-supported browsers
- [Obsolete Webpack Plugin](https://github.com/ElemeFE/obsolete-webpack-plugin)** generates a browser-side standalone script that detects browser compatibility based on Browserslist and prompts website users to upgrade it.

## CSS Compatibility Assurance

### Add missed CSS vendor prefixes suitable to required browsers set
CSS vendor prefixes (CSS browser prefixes) are a way for browser makers to add support for new CSS features before those features are fully supported in all browsers. Therefore, to support previous versions of browsers, add prefixes to the style sheet that are suitable for the browsers you need.

#### [Autoprefixer](https://github.com/postcss/autoprefixer)
CSS postprocessor, adds the required vendor prefixes to your stylesheets.

## Инструменты

### Показать вспомогательные линии разметки у элементов [Chrome DevTools]
*Settings -> Elements -> Show Rulers*

### Найти оригинальный обработчик событий элемента (установленный через JQuery)
[JQuery Audit](https://chrome.google.com/webstore/detail/jquery-audit/dhhnpbajdcgdmbbcoakfhmfgmemlncjg).

### Анализ производительности страницы сайта
[https://www.webpagetest.org/](https://www.webpagetest.org/)

## Multilingual development: Fast dive

### Go (Golang)
#### Most Simplified Program
```go
package main

import "fmt"

func main() {
    fmt.Println("hello world")
}
```
#### Execution
Run ```go run hello.go``` or compile and run ```go build hello.go && ./hello```

### Java

#### Hello World Program
```java
// HelloWorld.java

class HelloWorld
{
    public static void main(String[] args)
    {
        System.out.println("Hello World!");
    }
}
```
#### Compile and Run
```javac HelloWorld.java && java HelloWorld```

#### IntelliJ Idea

##### Create Project
*Create New Project -> Create Project From Template (Java Hello World) -> Choose project name and location -> Finish -> Run*

##### Git Integration
- Add `out\` to `.gitignore`


### Python
#### Packages
- Documentation [Installing Python Modules](https://docs.python.org/3/installing/index.html#installing-index)
- Install with pip ```python -m pip install SomePackage```
- Manual installation with setup.py ```python setup.py install```

# Data Processing

## Theory
- **Сигнал** это изменение чего-либо, какой-то характеристики (значения, совокупности значений) и факт изменения величины этой характеристики может кем-то отслеживаться, быть важным.  
- **Аналоговый сигнал** это непрерывное изменение непрерывной величины, к примеру изменение температуры, которое соответственно может быть описано в виде непрерывной функции.  
Можно получить значение изменяемой величины на совершенно любой момент времени и оно всегда будет точным. Но это же вызывает проблему с обработкой (к примеру хранением, хранением без потерь) - в зависимости от его характера это может быть сложно или невозможно.  
- **Дискретизация** это получение значений непрерывной функции с заданной частотой (через интервалы фиксированного размера) - прерывание непрерывной функции. Размер промежутка определяется **частотой дискретизации**.  
- **Дискретный сигнал** это дискретизированный аналоговый сигнал по времени и по значению (мерять значение температуры каждый час). Дискретный сигнал будет приближен к аналоговому оригиналу, и чем больше измерений было (выше частота дискретизации), тем точнее. С такими сигналами уже проще работать, так как их количество за определенный интервал фиксировано и заранее известно.  
- **Цифровой сигнал** это дискретный сигнал, где значения выражаются числами или чаще всего цифрами (0 и 1 в двоичном представлении).

## Sound
Звук это физическое явление, представляющее собой распространение в виде волн механических колебаний в воздушной среде среде. Как и любая волна, звук характеризуется **амплитудой** (определяет громкость) и **частотой** (определяет тон, высоту). Изменения амплитуды и частоты на протяжении времени представляют собой аналоговый сигнал.

### [PCM, Pulse Code Modulation, Ипульсно-кодовая модуляция](https://ru.wikipedia.org/wiki/%D0%98%D0%BC%D0%BF%D1%83%D0%BB%D1%8C%D1%81%D0%BD%D0%BE-%D0%BA%D0%BE%D0%B4%D0%BE%D0%B2%D0%B0%D1%8F_%D0%BC%D0%BE%D0%B4%D1%83%D0%BB%D1%8F%D1%86%D0%B8%D1%8F)
Процесс оцифровки аналоговых сигналов в цифровой. Обычно в контексте оцифровки аналогового аудиосигнала.  
Аналоговый аудиосигнал дискретизируется, амплитуда (значение) квантуется и результат кодируется в нужный формат.

### [SoX (Sound Exchange)](http://sox.sourceforge.net/)
CLI utility and library (libsox) with a huge amount of audio processing features.

#### Usage
##### Add MP3 support
```sudo apt-get install libsox-fmt-mp3```
##### Show information about audio-file
```sox audio.wav```
##### Convert from .mp3 to .wav (PCM), change channels count (to mono) and sample rate
```sox input.mp3 --channels 1 --rate 8000 output.wav```

### VAD (Voice Actitivity Detection)
A technique in which the presence or absence of human speech is detected.

#### Implementations

##### WebRTC VAD
The most famous VAD implementation is part of the Google [WebRTC](https://webrtc.org/) project. WebRTC does not expose the functionality of VAD as public, it is intended for internal project tasks. But you can access VAD functions through sources (C language) or use third-party libraries such as [dpirch/libfvad](https://github.com/dpirch/libfvad).
Library expects two arguments:
- 16-bit mono PCM audio, sampled at 8000, 16000, 32000 or 48000 Hz.
- aggressiveness mode, which is an integer between 0 and 3. 0 is the least aggressive about filtering out non-speech, 3 is the most aggressive.

###### [dpirch/libfvad](https://github.com/dpirch/libfvad)
This is a fork of the VAD engine that is part of the WebRTC Native Code package, for use as a standalone library independent from the rest of the WebRTC code. There are currently no changes in functionality.  
**fvadwav** (examples/fvadwav.c) is an excellent utility that calculates the total duration of the voice and non-voice segments contained in the audio recording.

###### [py-webrtcvad](https://github.com/wiseman/py-webrtcvad)
This is a python wrapper around Google's [WebRTC](https://webrtc.org/) VAD code. Wrapper contains the original VAD source codes extracted from the WebRTC project (C language) and compiles them during installation to native binary package. 

# Data Communication

## Network

### How To

#### Какие порты доступны для исходящих соединений
Можно с помощью сервера [portquiz.net](portquiz.net), у которого специально для этого открыты все TCP-порты.
- проверить конкретный порт: `telnet portquiz.net 80`
- проверить все порты: `nmap portquiz.net`
- проверить 100 популярных портов: `nmap --top-ports 100 portquiz.net`

#### Найти процесс который слушает определенный порт [Windows]
##### PowerShell
```powershell
Get-Process -Id (Get-NetTCPConnection -LocalPort portNumber).OwningProcess
```
##### Resource Monitor
`Win+r` and `resmon`

#### Создать точку доступа Wi-Fi [Windows]
```cmd
# Проверяем что установленный WiFi адаптер имееттакую возможность
# Параметр "Поддержка размещенной сети / Hosted Network Supported" должен быть Да/Yes
netsh wlan show drivers

# Определяем сеть
netsh wlan set hostednetwork mode=allow ssid=test key=999999999

# Запускаем сеть
netsh wlan start hostednetwork

# Затем сеть можно отключить
netsh wlan stop hostednetwork
```

# Workspace

## System

### User Management
#### CheatSheet
- Список всех групп `cat /etc/group | sort` в формате `<имя группы>:<пароль>:<ID группы (gid)>:<пользователи состоящие в группе>`
- Добавить пользователя в группу `adduser <user> <group>`
- Удалить пользователя из группы `groupdel <group>`
- Удалить пользователя из группы `deluser <user> <group>`
- Список групп процесса (пользователя под которым работает процесс) `ps -o supgid,supgrp -p <pid>`

### Terminal
#### Управляющие символы ANSI (ANSI escape code)
Определенная последовательность символов для передачи мета-информации терминалу, пользователю она не отображается. Может трактоваться терминалом, как указание по форматированию содержимого, взаимодействию с пользователем или другими процессами

- [Краткая и информативная вводная с примерами](https://stackoverflow.com/questions/4842424/list-of-ansi-color-escape-sequences/33206814#33206814) - начинать лучше с нее
- [Управляющие последовательности ANSI - Wikipedia](https://ru.wikipedia.org/wiki/%D0%A3%D0%BF%D1%80%D0%B0%D0%B2%D0%BB%D1%8F%D1%8E%D1%89%D0%B8%D0%B5_%D0%BF%D0%BE%D1%81%D0%BB%D0%B5%D0%B4%D0%BE%D0%B2%D0%B0%D1%82%D0%B5%D0%BB%D1%8C%D0%BD%D0%BE%D1%81%D1%82%D0%B8_ANSI)
- [Bash/Prompt customization](https://wiki.archlinux.org/index.php/Bash/Prompt_customization)
- [Build your own Command Line with ANSI escape codes](http://www.lihaoyi.com/post/BuildyourownCommandLinewithANSIescapecodes.html)
- [Terminal codes (ANSI/VT100) introduction](https://wiki.bash-hackers.org/scripting/terminalcodes#terminal_codes_ansivt100_introduction)

### Utilities
- [htop](https://www.systutorials.com/docs/linux/man/1-htop/) #tui #linux Приложение для просмотра и управления запущенными процессами, c интуитивным интерфейсом и с большим количеством возможностей.
- [KiTTY](http://www.9bis.net/kitty/?zone=ru) форк PuTTY [с расширенными возможностями](http://www.9bis.net/kitty/?zone=ru)
- PuTTY
- [strace](workspace/strace.md) is Linux utility to monitor and tamper with interactions between processes and the Linux kernel (system calls, signal deliveries, and changes of process state).
- [Midnight Commander](workspace/midnight-commander.md) is a powerfult text user-interface file manager.

#### PuTTY/KiTTY [Windows]
##### Не закрывать соединение/туннелирование
По-умолчанию, если не пользоваться терминалом, соединение закрывается через некоторое время, если вернуться в терминал и нажать любую клавишу, то соединение автоматически восстановится. Это неудобно при долговременных туннелях.  
`Connection -> "Sending of null packets to keep session active" -> "Seconds between keepalives"` укажите значение `240`, например.

#### Misc
- [FPrint](https://fprint.freedesktop.org/) для работы со сканером отпечатков пальцев. Например, по отпечатку можно входить в систему или использовать его вместо пароля для `sudo` (в Linux) (не забудьте подключить PAM-модуль `sudo pam-auth-update`) и тп.

## Software
### Telephony
- [Asterisk](workspace/asterisk.md) - наиболее известное и популярное программное решение для компьютерной телефонии с открытым исходным кодом.
