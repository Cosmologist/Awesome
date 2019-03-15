- [Development](#development)
  - [Resources](#resources)
  - [Constructs](#constructs)
  - [Environment](#environment)
    - [Database](#database)
    - [Database: MySQL](#database-mysql)
    - [Docker](#docker)
    - [Git](#git)
    - [IDE: IntelliJ Jetbrains](#intellij-jetbrains)
  - [Misc](#misc)
- [PHP Development](#php-development)
  - [Language](#language)
  - [Resources](#resources-1)
  - [Libraries](#libraries)
  - [Environment](#environment)
- [Symfony Development](#symfony-development)
  - [Libraries](#libraries-1)
- [JavaScript Development](#javascript-development)
  - [Language](#language-1)
  - [Libraries](#libraries-2)
- [Web Development](#web-development)
  - [JavaScript Compatibility Assurance](#javascript-compatibility-assurance)
  - [CSS Compatibility Assurance](#css-compatibility-assurance)
  - [Chrome DevTools](#chrome-devtools)
- [Various Languages - Fast Start](#various-languages---fast-start)
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
[MySQL Workbench](https://www.mysql.com/products/workbench/) The best UI-solution to MySQL administration! And a good data management solution.

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
#### Pretty `git log` output [[Source](http://garmoncheg.blogspot.com/2012/06/pretty-git-log.html)]
```sh
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit --"
```

### IDE
#### IntelliJ Jetbrains

##### Показывать `.dot`-файлы и директории в навигаторе 
Настройка `Preferences | File Types | Ignore files and folders`

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
- [nette/utils](https://github.com/nette/utils) Lightweight utilities for string & array manipulation, image handling, safe JSON encoding/decoding, validation, slug or strong password generating etc
- [danielstjules/Stringy](https://github.com/danielstjules/Stringy) A PHP string manipulation library with multibyte support

## Environment

### Debug
#### Trigger breakpoint for all exceptions [PhpStorm]
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

# Symfony Development
## Framework
### Multiline text in the .yml
```yaml
# app/config/config.yml
appbundle:
  myservice:
    description: > 
                   This is a 
                   multiline text
# will parsed as "This is a multiline text"
```
## Libraries
- [Incenteev/hashed-asset-bundle](https://github.com/Incenteev/hashed-asset-bundle) Apply an asset version based on a hash of the asset for symfony/asset

# JavaScript Development
## Language

## Libraries
[Clams.js](https://github.com/josephschmitt/Clamp.js) - Clamps an HTML element by adding ellipsis to it if the content inside is too long.

# Web Development
## JavaScript Compatibility Assurance
Each browser version implements a specific set of ECMAScript language features. Then you should provide compatible scripts to specific browsers set.

### Convert your scripts to older standards

#### Transpiler
Takes the syntax that older browsers won’t understand (e.g. classes, ‘const’, arrow functions), and turns them into syntax they will understand (functions, ‘var’, functions).

#### Babel Transpiler
[Babel](https://babeljs.io/docs/en/usage) is the most famous and popular transpiler.
```
# Install
npm install @babel/core @babel/cli @babel/preset-env

# Run via CLI
./node_modules/.bin/babel web/js/your-file.js --out-file script-compiled.js --presets=@babel/env
```
[@babel/preset-env](https://babeljs.io/docs/en/babel-preset-env) - most popular preset. Processes JS-scripts to achieve compatibility with a specified set of browsers (see the browserlist to specify set of browsers).

### Providing polyfills for unsupported browser features
#### Polyfill
Polyfill is a workaround for the specific missed feature.
##### [Loading Polyfills Only When Needed](https://philipwalton.com/articles/loading-polyfills-only-when-needed/)
The idea is to manually check and then dynamically load the polyfill.: ```if (!window.fetch) { loadScript('fetchPolyfill.js'); }```

### Useful
#### Check you website for compatibility issues
- [SortSite](https://www.powermapper.com/products/sortsite/checks/browser-compatibility/).
#### Notify users with non-supported browsers
- [Obsolete Webpack Plugin](https://github.com/ElemeFE/obsolete-webpack-plugin)** generates a browser-side standalone script that detects browser compatibility based on Browserslist and prompts website users to upgrade it.

## CSS Compatibility Assurance

### Add missed CSS vendor prefixes suitable to required browsers set
CSS vendor prefixes (CSS browser prefixes) are a way for browser makers to add support for new CSS features before those features are fully supported in all browsers. Therefore, to support previous versions of browsers, add prefixes to the style sheet that are suitable for the browsers you need.

#### [Autoprefixer](https://github.com/postcss/autoprefixer)
CSS postprocessor, adds the required vendor prefixes to your stylesheets.

## Chrome DevTools

### Отображение вспомогательных линий разметки у элементов
*Settings -> Elements -> Show Rulers*

### Найти оригинальный обработчик событий элемента (установленного через JQuery)
К примеру, c помощью расширения [JQuery Audit](https://chrome.google.com/webstore/detail/jquery-audit/dhhnpbajdcgdmbbcoakfhmfgmemlncjg). *(Так как подписан на событие именно JQuery)*. 

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
Проверить доступ к порту можно следующим образом: `telnet portquiz.net 80` ([portquiz.net](portquiz.net) - публичный сервер на котором открыты все TCP-порты).  
Получить список всех портов можно с помощью nmap: `nmap IP` или только по первым 100 списка популярных портов `nmap --top-ports 100 portquiz.net`

# Workspace

## System

### Terminal
#### Управляющие символы ANSI (ANSI escape code)
Cпециальные символы, встраиваемые в текстовый вывод (stdout) приложения, для форматирования содержимого (цвет, форматирование) или для взаимодействия с пользователем или другими процессами

- [Краткая и информативная вводная с примерами](https://stackoverflow.com/questions/4842424/list-of-ansi-color-escape-sequences/33206814#33206814) - начинать лучше с нее
- [Управляющие последовательности ANSI - Wikipedia](https://ru.wikipedia.org/wiki/%D0%A3%D0%BF%D1%80%D0%B0%D0%B2%D0%BB%D1%8F%D1%8E%D1%89%D0%B8%D0%B5_%D0%BF%D0%BE%D1%81%D0%BB%D0%B5%D0%B4%D0%BE%D0%B2%D0%B0%D1%82%D0%B5%D0%BB%D1%8C%D0%BD%D0%BE%D1%81%D1%82%D0%B8_ANSI)
- [Bash/Prompt customization](https://wiki.archlinux.org/index.php/Bash/Prompt_customization)
- [Build your own Command Line with ANSI escape codes](http://www.lihaoyi.com/post/BuildyourownCommandLinewithANSIescapecodes.html)
- [Terminal codes (ANSI/VT100) introduction](https://wiki.bash-hackers.org/scripting/terminalcodes#terminal_codes_ansivt100_introduction)

### Utilities
- [htop](https://www.systutorials.com/docs/linux/man/1-htop/) #tui #linux Приложение для просмотра и управления запущенными процессами, c интуитивным интерфейсом и с большим количеством возможностей.
- [strace](workspace/strace.md) is Linux utility to monitor and tamper with interactions between processes and the Linux kernel (system calls, signal deliveries, and changes of process state).
- [Midnight Commander](workspace/midnight-commander.md) is a powerfult text user-interface file manager.
- [FPrint](https://fprint.freedesktop.org/) - интеграция сканеров отпечатков пальцев. Например, по отпечатку можно входить в систему или использовать его вместо пароля для `sudo` (в Linux) (не забудьте подключить PAM-модуль `sudo pam-auth-update`) и тп.

## Software
### Telephony
- [Asterisk](workspace/asterisk.md) - наиболее известное и популярное программное решение для компьютерной телефонии с открытым исходным кодом.
