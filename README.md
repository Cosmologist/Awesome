- [Development](#development)
  - [Resources](#resources)
  - [Constructs](#constructs)
  - [Misc](#misc)
- [PHP Development](#php-development)
  - [Resources](#resources-1)
  - [Libraries](#libraries)
  - [Environment](#environment)
  - [Nuances](#nuances)
- [Symfony Development](#symfony-development)
  - [Libraries](#libraries-1)
- [Web Development](#web-development)
  - [Chrome DevTools](#chrome-devtools)
  - [JS Libraries](#js-libraries)
- [Various Languages - Fast Start](#various-languages---fast-start)
  - [Go (Golang)](#go-golang)
  - [Java](#java)
- [Development Environment](#development-environment)
  - [Database](#database)
  - [MySQL Database](#mysql-database)
- [Data Processing](#data-processing)
  - [Sound](#sound)
    - [Concepts](#concepts)
- [Workspace](#workspace)
  - [Utilities](#utilites)
  - [Receipts](#receipts)

# Development

## Resources
[LibHunt](https://www.libhunt.com/) - Big curruated catalog of useful libraries and resources. It has a convenient ability to compare libraries.

## Constructs
[Функциональный интерфейс](https://docs.oracle.com/javase/8/docs/api/java/util/function/package-summary.html) (**Functional Interfaces**, **SAM (Single Abstract Method) Interfaces** - интерфейс который содержит **только один метод**.

**Promise** - Cпособ извещения о завершении обработки (успешной или нет) и получения результата обработки при параллельных вычислениях.
 
```js
function computeAsync(inputData) {
  return new Promise(function (resolve, reject) {
    ... // долгие вычисления
    
    if (error) {
      // уведомляем что вычисления завершены с ошибкой
      // можем передать любые данные, которые будут переданы в failComputationCallback (смотри ниже)
      reject(errorData)
    } else {
      // уведомляем что вычисления завершены с ошибкой
      // можем передать любые данные, которые будут переданы в successComputationCallback (смотри ниже)
      resolve(data) // уведомляем что вычисления завершены успешно, можем вернуть дополнительную информацию
    }
  }
)
...
computeAsync().then(successComputationCallback, failComputationCallback)
```
- [Using_promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises)

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

## Resources
[marcelgsantos/learning-oop-in-php](https://github.com/marcelgsantos/learning-oop-in-php) - A collection of resources to learn object-oriented programming and related concepts for PHP developers.

## Libraries
- [Awesome PHP](https://php.libhunt.com/) A curated list of awesome PHP libraries and resources
- [nette/utils](https://github.com/nette/utils) Lightweight utilities for string & array manipulation, image handling, safe JSON encoding/decoding, validation, slug or strong password generating etc
- [danielstjules/Stringy](https://github.com/danielstjules/Stringy) A PHP string manipulation library with multibyte support
- [Pre](https://preprocess.io/) - Pre is a PHP preprocessor, designed to make adding new syntax effortless. Flexible integration via Composer

## Environment
### WebServer
#### CGI, FastCGI, PHP-FPM
**CGI** - устаревший протокол взаимодействия между веб-сервером и приложениями (скриптами), общение ведется только через STDIN/STDOUT, на каждый запрос создается отдельный процесс приложения, который умирает после ответа.  
**FastCGI** - общение ведется через сокеты или TCP (что дает возможность разнести сервер и приложение), предполагается наличие FastCGI-менеджера, который заранее подготоваливает пул процессов приложения, что позволяет значительно быстрее отдать запрос на обработку. Реализация FastCGI-менеджера может быть встроена в сервер (Apache) или нет (Nginx).  
**PHP-FastCGI** - устаревшая реализация FastCGI встроенная в интерпретатор. В отличие от PHP-FPM - и для CLI (CGI) и для FastCGI использовался общий интерпретатор, для запуска PHP в режиме FastCGI сервиса использовался аргумент ```--bindpath``` в который пробрасывался путь к сокету или TCP-адрес на который биндился FastCGI-менеджер.  
**PHP-FPM** (FastCGI Process Manager) - это современная улучшенная реализация *FastCGI* встроенная в интерпретатор PHP с рядом новых возможностей.

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

## Nuances

### The + operator
Adds items from right-hand array to the left-hand array, only the keys of which are missing in the left-hand array (associative or indexed keys).  
**Example**: building a config array, where the left-hand array contains only changed parameters, and the right-hand array contains all possible parameters with default values.

### `$array[]` vs `array_push`
`$array[]` is about [two times faster](https://stackoverflow.com/posts/559859/revisions), because there is no overhead of calling a function.

# Symfony Development
## Libraries
- [Incenteev/hashed-asset-bundle](https://github.com/Incenteev/hashed-asset-bundle) Apply an asset version based on a hash of the asset for symfony/asset

# Web Development

## JS Libraries
[Clams.js](https://github.com/josephschmitt/Clamp.js) - Clamps an HTML element by adding ellipsis to it if the content inside is too long.

### Compatibility Assurance
- **[Loading Polyfills Only When Needed](https://philipwalton.com/articles/loading-polyfills-only-when-needed/)** The idea is to manually check and then dynamically load the polyfill.: ```if (!window.fetch) { loadScript('fetchPolyfill.js'); }```
- **[Browserlist](https://github.com/browserslist/browserslist)** is the standard format of config file to share your target browsers between different front-end tools.
- **[Obsolete Webpack Plugin](https://github.com/ElemeFE/obsolete-webpack-plugin)** generates a browser-side standalone script that detects browser compatibility based on Browserslist and prompts website users to upgrade it.
- **[SortSite](https://www.powermapper.com/products/sortsite/checks/browser-compatibility/)** (web version) is an application for testing your website for browser compatibility.

#### Babel
[Babel](https://babeljs.io/docs/en/usage) is a tool (transpiler) whose the main goal is to achieve compatability with specified targets (like browsers, node) by processing your code.
```
# Install
npm install --save-dev @babel/core @babel/cli @babel/preset-env
# Run via CLI
./node_modules/.bin/babel web/js/your-file.js --out-file script-compiled.js --presets=@babel/env
```
[@babel/preset-env preset](https://babeljs.io/docs/en/babel-preset-env) - most popular preset. Processes JS-scripts to achieve compatibility with a specified set of browsers (see the browserlist to specify set of browsers).

## Chrome DevTools
### Useful settings
**Auxiliary Lines** (**Measure**, **Ruler**) - *Settings -> Elements -> Show Rulers*

## Various Languages - Fast Start

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
#### Most Simplified Program
```java
class HelloWorld
{
    public static void main(String[] args)
    {
        System.out.println("Hello World!");
    }
}
```
#### Execution
```javac HelloWorld.java && java HelloWorld```

#### Project Structure (Archetype)
**Archetype** is a project stucture convention.  
You can use one of the [common archetypes](http://maven.apache.org/archetypes/index.html) or create your own.

#### Packages

##### Types
- **.jar**-файл (Java ARchive) (ZIP-archive with compiled classes + metadata)
- Sources

##### Name convention
org.springframework.spring:2.5.5
- **Package name**: org.springframework.spring
- **Group name**: org.springframework
- **Artifact name**: spring
- **Version**: 2.5.5


# Development Environment
## Database

### Storing Files in a Database
> [I know of no advantages to storing data I want to keep for a long time outside of a database.](https://asktom.oracle.com/pls/apex/f?p=100:11:0%3A%3A%3A%3AP11_QUESTION_ID:1011065100346196442) If it is in the database. I can be sure it is professionally managed, backed up, recoverable (with the rest of the data), secured, scalable (try putting 100,000 documents in a single directory, now, put them in table - which one 'scales' - it is not the directory). I can undelete (flashback) easily. I have locking. I have read consistency.

## MySQL Database
[MySQL Workbench](https://www.mysql.com/products/workbench/) The best UI-solution to MySQL administration! And a good data management solution.

### Текстовый и бинарный протоколы
Текстовый протокол оперирует текстовыми данными, бинарный текстовыми и числовыми.  
Бинарный протокол более эффективен так как:
- данные, которыми происходит обмен, эффективней упакованы (занимают меньше места)
- уменьшает количество операций по приведению типов на сервере и восстановлению (опционально) типов на клиенте
**Важно:** MySQL позволяет использовать бинарный протокол только для при работе с prepared statements.

- [https://dev.mysql.com/doc/internals/en/binary-protocol-value.html]
- High Performance MySQL, O'Relly, page #225

# Data Processing
## Concepts

### Сигналы

**Сигнал** — это изменение чего-либо, какой-то характеристики (значения, совокупности значений) и факт изменения величины этой характеристики может кем-то отслеживаться, быть важным.  
**Аналоговый сигнал** - непрерывное изменение непрерывной величины, к примеру изменение температуры, которое соответственно может быть описано в виде непрерывной функции.  
Можно получить значение изменяемой величины на совершенно любой момент времени и оно всегда будет точным. Но это же вызывает проблему с обработкой (к примеру хранением, хранением без потерь) - в зависимости от его характера это может быть сложно или невозможно.  
**Дискретизация** - получение значений непрерывной функции с заданной частотой (через интервалы фиксированного размера) - прерывание непрерывной функции. Размер промежутка определяет **частоту дискретизации**.  
**Дискретный сигнал** - дискретизированный аналоговый сигнал по времени и по значению (мерять значение температуры каждый час). Дискретный сигнал будет приближен к аналоговому оригиналу, и чем больше измерений было (выше частота дискретизации), тем точнее. С такими сигналами уже проще работать, так как их количество за определенный интервал фиксировано и заранее известно.  
**Цифровой сигнал** - дискретный сигнал, где значения выражаются числами или чаще всего цифрами (0 и 1 в двоичном представлении).

## Sound
### Concepts

#### Звук
Физическое явление, представляющее собой распространение в виде волн механических колебаний в воздушной среде среде. Как и любая волна, звук характеризуется **амплитудой** (определяет громкость) и **частотой** (определяет тон, высоту). Изменения амплитуды и частоты на протяжении времени представляют собой аналоговый сигнал.

#### [PCM, Pulse Code Modulation, Ипульсно-кодовая модуляция](https://ru.wikipedia.org/wiki/%D0%98%D0%BC%D0%BF%D1%83%D0%BB%D1%8C%D1%81%D0%BD%D0%BE-%D0%BA%D0%BE%D0%B4%D0%BE%D0%B2%D0%B0%D1%8F_%D0%BC%D0%BE%D0%B4%D1%83%D0%BB%D1%8F%D1%86%D0%B8%D1%8F)
Процесс оцифровки аналоговых сигналов в цифровой. Обычно в контексте оцифровки аналогового аудиосигнала.  
Аналоговый аудиосигнал дискретизируется, амплитуда (значение) квантуется и результат кодируется в нужный формат.

# Workspace
## Utilites

[htop](https://www.systutorials.com/docs/linux/man/1-htop/) is intuitive and powerful interactive process viewer
  
[Midnight Commader](http://midnight-commander.org) is a powerfult text user-interface file manager

**Resources**
- [Use Midnight Commander like a pro](http://klimer.eu/2015/05/01/use-midnight-commander-like-a-pro/)
- [Midnight Commander Tips and Tricks](http://www.softpanorama.org/OFM/MC/mc_tips.shtml)

**Settings**
- Settings will be stored in the *~/.config/mc/ini*
- Datetime format option names are *timeformat_old* (datetime < now - 6 months) and *timeformat_recent* (datetime > now - 6 month). Example of format: `%Y-%m-%d %H:%M`

[strace](https://strace.io/) is Linux utility to monitor and tamper with interactions between processes and the Linux kernel (system calls, signal deliveries, and changes of process state).

**Examples**
```
# Monitoring file activity
strace -p process-pid

# Monitoring the network
strace -e trace=network

# Monitoring memory calls
strace -e trace=memory
```
**Resources**
- [The ultimate strace cheat sheet](https://linux-audit.com/the-ultimate-strace-cheat-sheet/)

### Receipts

**Какие порты доступны для исходящих соединений**
 
Проверить доступ к порту можно следующим образом: `telnet portquiz.net 80` ([portquiz.net](portquiz.net) - публичный сервер на котором открыты все TCP-порты).  
Получить список всех портов можно с помощью nmap: `nmap IP` или только по первым 100 списка популярных портов `nmap --top-ports 100 portquiz.net`

