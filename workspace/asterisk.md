# Asterisk
Наиболее распространенное программное решение для компьютерной телефонии с открытым исходным кодом.

## Basics
*Звонок* поступает по одному из **каналов** и передается в **контекст**, который описывает последовательной действий (**extension**) по его обработке. 

1. **Каналами** (**Channels**) называются источники поступающих звонков/соединений (телефоны, шлюзы и тп) на сервер
2. **Extension** это описание действия (**application**) которое надо выполнить и условие (опционально) для выполнения. Абстрактно *extension* можно представить в виде фрагмента псевдокода: ```if (condition === true) { executeAction }```
3. **Контекст** это именованная группа *extension*ов.
4. **Dialplan**ом называется набор всех *контекстов*, прописанных в конфигурации.

### Extension
#### Формат 
```exten => name,priority,action()```

#### Имя/условие/шаблон
- обычная метка для *extension* в формате `([0-9]|[ABCD]|[a-z])+`
- условие выполнения действия
  a. по *state* соединения `i|s|h|t|T|o` (Invalid, Start, Hangup, Timeout, AbsoluteTimeout, Operator)
  b. по идентификатору соединения (номер телефона) или по шаблону для идентификатора (начинается с *_*)

**Формат шаблона**
- X - any digit from 0-9
- Z - any digit from 1-9
- N - any digit from 2-9
- [12679] - any digit in the brakets (in the example: 1,2,6,7,9)
- . - (dot) wildcard, matches everything remaining 

**Пример шаблона**
( _1234. - matches anything strating with 1234 excluding 1234 itself).

#### Пример контекста
```
[incoming]
exten => s,1,Answer()
exten => s,n,Playback(hello-world)
exten => s,n,Hangup() 
```
- **s** (Start) зарезервированное имя и соответствуют состоянию входящего соединения в самом начале.
- **priority** число определяет последовательность выполнения в рамках экстеншенов с одним именем (условием). *n* значит следующее число, чтобы не писать 1,2,3

#### Пример контекста с несколькими группами по имени/шаблону
```
[incoming]
exten => +74951234567,1,Answer()
exten => +74951234567,n,Playback(hello-moscow)
exten => +74951234567,n,Hangup() 
exten => +78121234567,1,Answer()
exten => +78121234567,n,Playback(hello-piter)

exten => +78121234567,n,Hangup() 
```

### Useful
- [Chapter 5. Dialplan Basics, Asterisk: The Future of Telephony, 2nd Edition](https://www.oreilly.com/library/view/asterisk-the-future/9780596510480/ch05.html) Отличная вводная
- [Asterisk Book 3rd Edition [HTML][Eng]](http://www.asteriskdocs.org/en/3rd_Edition/asterisk-book-html-chunk/index.html)
- [FreePBX](https://www.freepbx.org/) web-интерфейс для управления сервером. Наиболее известное и распространенное решение по сравнению с другими.
