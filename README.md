# Developing

## Resources
[LibHunt](https://www.libhunt.com/) - Big curruated catalog of useful libraries and resources. It has a convenient ability to compare libraries.

## Concepts
[Функциональный интерфейс](https://docs.oracle.com/javase/8/docs/api/java/util/function/package-summary.html) (**Functional Interfaces**, **SAM (Single Abstract Method) Interfaces** - интерфейс который содержит **только один метод**.

**Promise** - Cпособ извещения о завершении обработки (успешной или нет) и получения результата обработки при параллельных вычислениях.
<details>
 
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
</details>  

## Misc

[Naming for Adapter Pattern](https://softwareengineering.stackexchange.com/questions/361777/how-to-name-different-components-in-adapter-pattern) - good name option is **FooFromBar** or **FooFromBarAdapter**.  

**Terms Routine, Subroutine, Function, Procedure, Method, Coroutine**
<details>

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
</details>


# PHP Developing
## Resources
[marcelgsantos/learning-oop-in-php](https://github.com/marcelgsantos/learning-oop-in-php) - A collection of resources to learn object-oriented programming and related concepts for PHP developers.

## Language
**The + operator** - Add items from right-hand array to the left-hand array.
<details>
 
The right-hand array item will be added only if the left-hand array does not contain suitable key, otherwise the item will be ignored. There is no difference between numeric and non-numeric keys.
**Example**: building a config array, where the left-hand array contains only changed parameters, and the right-hand array contains all possible parameters with default values.
</details>

## Performance
[$array[] = $value vs array_push($array, $value)](https://stackoverflow.com/posts/559859/revisions) - *$array[]* is about two times faster, because there is no overhead of calling a function.

## Libraries
[Awesome PHP](https://php.libhunt.com/) A curated list of awesome PHP libraries and resources

[Pre](https://preprocess.io/) - Pre is a PHP preprocessor, designed to make adding new syntax effortless. Flexible integration via Composer

[Stringy](https://github.com/danielstjules/Stringy) A PHP string manipulation library with multibyte support

# Web Developing
**Chrome DevTools**
<details>
 
 ## Useful settings
**Auxiliary Lines** (**Measure**, **Ruler**) - *Settings -> Elements -> Show Rulers*
 </details>

## JS Libraries
[Clams.js](https://github.com/josephschmitt/Clamp.js) - Clamps an HTML element by adding ellipsis to it if the content inside is too long.

# User experience
## System Utilites

[htop](https://www.systutorials.com/docs/linux/man/1-htop/) is intuitive and powerful interactive process viewer.

[strace](https://strace.io/) is Linux utility to monitor and tamper with interactions between processes and the Linux kernel (system calls, signal deliveries, and changes of process state).

<details>
 
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
</details>

**Midnight Commader** is a powerfult text user-interface file manager
<details>
 
**Resources**
- [Use Midnight Commander like a pro](http://klimer.eu/2015/05/01/use-midnight-commander-like-a-pro/)
- [Midnight Commander Tips and Tricks](http://www.softpanorama.org/OFM/MC/mc_tips.shtml)

**Settings**
- Settings will be stored in the *~/.config/mc/ini*
- Datetime format option names are *timeformat_old* (datetime < now - 6 months) and *timeformat_recent* (datetime > now - 6 month). Example of format: `%Y-%m-%d %H:%M`
</details>
