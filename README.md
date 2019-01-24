- [Development](#development)
  - [Resources](#resources)
  - [Constructs](#constructs)
  - [Misc](#misc)
- [PHP Development](#php-development)
  - [Resources](#resources-1)
  - [Language](#language)
  - [Environment](#environment)
  - [Libraries](#libraries)
  - [Performance](#performance)
- [Symfony Development](#symfony-development)
  - [Libraries](#libraries-1)
- [Web Development](#web-development)
  - [Chrome DevTools](#chrome-devtools)
  - [JS Libraries](#js-libraries)
- [Development Environment](#development-environment)
  - [Database](#database)
  - [MySQL Database](#mysql-database)
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

## Language
**The + operator** - Add items from right-hand array to the left-hand array.
 
The right-hand array item will be added only if the left-hand array does not contain suitable key, otherwise the item will be ignored. There is no difference between numeric and non-numeric keys.
**Example**: building a config array, where the left-hand array contains only changed parameters, and the right-hand array contains all possible parameters with default values.

## Environment
### CGI, FastCGI, PHP-FPM
**CGI** - устаревший протокол взаимодействия между веб-сервером и приложениями (скриптами), общение ведется только через STDIN/STDOUT, на каждый запрос создается отдельный процесс приложения, который умирает после ответа.  
**FastCGI** - общение ведется через сокеты или TCP (что дает возможность разнести сервер и приложение), предполагается наличие FastCGI-менеджера, который заранее подготоваливает пул процессов приложения, что позволяет значительно быстрее отдать запрос на обработку. Реализация FastCGI-менеджера может быть встроена в сервер (Apache) или нет (Nginx).  
**PHP-FastCGI** - устаревшая реализация FastCGI встроенная в интерпретатор. В отличие от PHP-FPM - и для CLI (CGI) и для FastCGI использовался общий интерпретатор, для запуска PHP в режиме FastCGI сервиса использовался аргумент ```--bindpath``` в который пробрасывался путь к сокету или TCP-адрес на который биндился FastCGI-менеджер.  
**PHP-FPM** (FastCGI Process Manager) - это современная улучшенная реализация *FastCGI* встроенная в интерпретатор PHP с рядом новых возможностей.

Links:
 - [PHP-FPM, application server made by PHP](https://publications.jbfavre.org/web/php-fpm-apps-server-nginx.en)

## Libraries
- [Awesome PHP](https://php.libhunt.com/) A curated list of awesome PHP libraries and resources
- [nette/utils](https://github.com/nette/utils) Lightweight utilities for string & array manipulation, image handling, safe JSON encoding/decoding, validation, slug or strong password generating etc
- [danielstjules/Stringy](https://github.com/danielstjules/Stringy) A PHP string manipulation library with multibyte support
- [Pre](https://preprocess.io/) - Pre is a PHP preprocessor, designed to make adding new syntax effortless. Flexible integration via Composer

## Performance
[$array[] = $value vs array_push($array, $value)](https://stackoverflow.com/posts/559859/revisions) - *$array[]* is about two times faster, because there is no overhead of calling a function.

# Symfony Development
## Libraries
- [Incenteev/hashed-asset-bundle](https://github.com/Incenteev/hashed-asset-bundle) Apply an asset version based on a hash of the asset for symfony/asset

# Web Development
## Chrome DevTools
 
### Useful settings
**Auxiliary Lines** (**Measure**, **Ruler**) - *Settings -> Elements -> Show Rulers*

## JS Libraries
[Clams.js](https://github.com/josephschmitt/Clamp.js) - Clamps an HTML element by adding ellipsis to it if the content inside is too long.

# Development Environment
## Database

### Storing Files in a Database
> [I know of no advantages to storing data I want to keep for a long time outside of a database.](https://asktom.oracle.com/pls/apex/f?p=100:11:0%3A%3A%3A%3AP11_QUESTION_ID:1011065100346196442) If it is in the database. I can be sure it is professionally managed, backed up, recoverable (with the rest of the data), secured, scalable (try putting 100,000 documents in a single directory, now, put them in table - which one 'scales' - it is not the directory). I can undelete (flashback) easily. I have locking. I have read consistency.

## MySQL Database
The best UI-solution to MySQL administration! And a good data management solution.

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

