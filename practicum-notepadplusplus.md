# Работа с текстом в продвинутом текстовом редакторе  

В этом практикуме мы будем работать со сменой [кодировок файла](https://support.microsoft.com/ru-ru/office/%D0%B2%D1%8B%D0%B1%D0%BE%D1%80-%D0%BA%D0%BE%D0%B4%D0%B8%D1%80%D0%BE%D0%B2%D0%BA%D0%B8-%D1%82%D0%B5%D0%BA%D1%81%D1%82%D0%B0-%D0%BF%D1%80%D0%B8-%D0%BE%D1%82%D0%BA%D1%80%D1%8B%D1%82%D0%B8%D0%B8-%D0%B8-%D1%81%D0%BE%D1%85%D1%80%D0%B0%D0%BD%D0%B5%D0%BD%D0%B8%D0%B8-%D1%84%D0%B0%D0%B9%D0%BB%D0%BE%D0%B2-60d59c21-88b5-4006-831c-d536d42fd861) и форматов конца строки, со скрытыми символами и режимом переноса строк. 
Профессиональные текстовые редакторы Поиск и замена. Регулярные выражения.


Что понадобится: **NotePad++.**  
Владельцы Mac-ов используют аналоги: редакторы **Sublime**, **Atom**, **BBEdit**, **Fraise** и т.д.  
(_Обратите внимание: Обычный Блокнот (NotePad), Word и прочие офисные редакторы для этого практикума не годятся_).  

Файлы для работы:
1. [dovlatov3.utf8.txt](https://disk.yandex.ru/d/ln9iiduNMDRWVQ) и [dovlatov3.txt](https://disk.yandex.ru/d/7S5ji7WmHsQoIQ)  
2. [простая html-страничка](https://disk.yandex.ru/d/nJI_mHX6r4ECPw) и [html-страничка c бутстрапом](https://disk.yandex.ru/d/hcnAlxniLNU5fw)  
3. [tsv-файл из ELAN](https://disk.yandex.ru/d/02JsinlNdLyQSQ)  

## 1. Кодировки

Типы кодировок текста для русского языка:

* [Unicode](https://ru.wikipedia.org/wiki/%D0%AE%D0%BD%D0%B8%D0%BA%D0%BE%D0%B4) (UTF-8 без цифровой подписи BOM и с нею) - основная кодировка для автоматической обработки текстовых файлов  
* [Cyrillic Windows (cp1251)](https://ru.wikipedia.org/wiki/Windows-1251) - кодировка компании Microsoft для Windows  
* KOI8-R, DOS, ... - более старые форматы  
* ASCII (American Standard Code for Information Interchange) - предок всех вышеупомянутых  

**Упражнение**
1) Откройте файл [dovlatov3.utf8.txt](https://disk.yandex.ru/d/ln9iiduNMDRWVQ).  
В меню "Кодировки" замените текущую на Windows-1251, затем обратно на UTF-8 без BOM.

Если вы открываете файл и видите "кракозябры", то с помощью меню "Кодировки" можно подобрать правильную.

"Преобразовать в...": переводит файл в другую кодировку (затем файл нужно сохранить). Windows-1251 называется ANSI.


## 2. Вид → Отображение символов и Перенос строк  

В меню Отображение символов отметьте чекбоксы: (а) отображать пробелы и табуляции, (b) отображать символы конца строки ((c) отображать все символы).
Перенос строк (text wrap) автоматически переносит текст на новую строку, как в Word. Видимые концы строк при этом не сохраняются (являются "мягкими", то есть вычисляются редактором по специальному алгоритму).


## 3. Формат конца строки

Непечатаемые символы, обозначающие конец строки:

Win-формат: CR+LF `\r\n`

old-Mac-формат: CR `\r`

UNIX-формат: LF `\n`

В режиме отображения символов конца строки вы увидите "СR", "LF", которые при поиске и замене в расширенном режиме и в режиме регулярных выражений задаются как эскейп-символы `\r`, `\n`, соответственно.  


## 4. Поиск и замена  
Меню для поиска и замены доступно по горячей клавише Ctrl+F (см. также меню Поиск и замена или Правка, в зависимости от редактора)  
Отмена операции: Ctrl+Z  
По умолчанию, в NotePad++ поиск происводится начиная с текущей позиции курсора до конца файла, включите чекбокс "Зациклить поиск", чтобы замена проводилась по всему файлу.  

**Упражнение**  
1) Найдите все вхождения отрицания _не_.  
2) Замените их на _НЕ_.  
3) Отмените последнюю операцию.


## 5. Режим поиска "Регулярные выражения"

* Табуляция: экскейп-символ `\t`

Замените все пробелы на табуляцию и затем наоборот. 

* Концы строк: `\r\n` или `\n`, в зависимости от формата конца строк, см. выше.  

Замените концы строк на пробел.

* `^` - начало строки, `$` - конец строки  

* `к[аоиу]т` - найдет _кат_, _кот_, _кит_, _кут_

* `[а-яё]` - найдет все буквы русского алфавита

* `[0-9a-z@_.]` - все знаки, допустимые в адресе электронной почты

Узнайте, есть ли в тексте латинские буквы?

* `[^а-я]` - "крышка" обозначает НЕ, т. е. все символы, кроме указанного диапазона а-я.

* `[^!]$`- найдет концы абзацев, не заканчивающиеся на восклицательный знак

* `.` - любой символ

* `.+` - повтор (любого символа) 1 или более раз

* `.*` - повтор (любого символа) 0 или более раз

* `е+` - найдет _е_, _ее_, _еее_...

* `[нм]+` - найдет сочетания _нн_, _мм_, _нм_, _мн_, _ммм_, _нннн_, _мнннннм_...

* `л.+` - найдет букву _л_ и далее все символы до конца строки

* `л[а-яё]+` - что найдется здесь?

* `˽я[а-яё]*` - (в начале пробел) найдет слова, начинающиеся с _я_, в том числе слово _я_

Этот поиск "__жадный__" - он будет искать строку максимальной длины, соответствующую условию в "Искать".

Запрос `<.*>` в строке `<p>что-то здесь</p>` найдет всю строку целиком: `<p>что-то здесь</p>`

Нежадный ("__ленивый__") поиск:

* `.+?`

* `.*?`

-- ищет до первого вхождения символа, указанного после ?

* `<.*?>` - найдет тег `<p>`, затем тег `<p>`: `<p>что-то здесь</p>`

* `ч.+о` - найдет `"что-то"`

* `ч.+?о` - найдет `"что"`

Найдите с помощью "ленивого поиска" последовательность букв от пробела до пробела (слово).


## 7. Регулярные выражения: эскейп-символы

* `\.` - ищет точку

* `\\` - ищет обратный слэш

* `\+`, `\*`, `\[`, `\]`, `\(` - ищет плюс, звездочку, знаки скобок и т.п.

Найдите все концы абзацев, заканчивающиеся на точку.


## 8. Использование условий поиска (backreference)  

Заключите все условие или его части в скобки. 

В поле "Заменить"

* `\1`, `\2`, `\3` - обозначает части поиска, которые в строке поиска заключены в первую, вторую и третью пару скобок, соответственно

* `([^ -])- ([^ -])` → `\1\2` - уберет дефисы, оставшиеся после удаления жестких концов строк.

Задание: Задайте маску поиска конца прямой речи.  

Подсказка: используйте `[ ]` со списком знаков препинания  

**__Предупреждение: язык регулярных выражений может немного различаться в разных редакторах и в разных языках программирования (нотацией), но в целом набор приемов и принципы поиска одинаковы.__**



## Практикум  

##### А. Файл для работы - [dovlatov3.txt](https://disk.yandex.ru/d/7S5ji7WmHsQoIQ)  

1)    убрать ударения
2)    заменить прописные буквы строчными в заголовке
3)    заменить пробелы в начале абзацев на табуляцию
4)    убрать "жесткие" концы строк, оставив деление на абзацы и мини-рассказы  
5)    при этом аккуратно обработать слова с переносами
6)    убрать "лишние" пробелы (два и больше)

**Полезные приемы** 
##### Уберите все знаки ударения

Выделите символ ударения, меню Поиск → Замена,
поле Заменить оставьте пустым. (Режим поиска: обычный, Заменить всё)

Правка → Преобразовать выделение → строчные

Замена пробелов в начале строки на табуляцию:  
* Найти: `^˽˽˽˽˽` (5 пробелов) или `^˽+` (любое количество пробелов в начале строки)
* Заменить: `\t` (Режим поиска: расширенный)

Замена границ мини-рассказов в тексте:  
* Найти: `\r\n\r\n`, 
* Заменить на псевдослово (например, #newdoc#). (Режим поиска: расширенный)

Замена концов строк на пробел:  
* Найти: `\r\n` 
* Заменить на 1 пробел. (Режим поиска: расширенный)

Верните границы абзацев и мини-рассказов. (Догадайтесь, как! Подсказка: абзацы начинаются с табуляции).


##### Дополнительное задание 1:
Cоздайте список уникальных слов по вашему файлу.  

0) сохраните содержимое файла в новый файл dovlatov_wordlist.txt  
1) переведите все слова в нижний регистр (Правка -> Конвертировать Регистр / Edit -> Convert case to...)   
2) сделайте так, чтобы каждое слово шло с новой строки, вставив концы строк  
3) сделайте так, чтобы каждый знак препинания также шел с новой строки  
4) отсортируйте строки по алфавиту (Правка -> Операции со строками -> Сортировать по возрастанию / Edit -> Line operations -> Sort lines lexicographically ascending).  
5) удалите повторяющиеся строки с помощью регулярных выражений  
    `^(.*\r\n)\1+` -> `\1`    


##### Дополнительное задание 2: 
В файле с текстом разметьте начало и конец прямой речи с помощью тега <speech>, например, вот так:
```    
   -- <speech>Не думаю</speech>, -- сказал редактор, потом вдруг
рассердился, -- <speech>хватит!  Вечные отговорки!  Всё не как
у людей!  Извольте одеваться так, как подобает
работнику солидной газеты!</speech>
```
Все ли реплики прямой речи вам удастся так разметить?


  
  
  
### Дополнительные материалы

* Краткий курс по регулярным выражениям в NotePad++](http://markantoniou.blogspot.ru/2008/06/notepad-how-to-use-regular-expressions.html)  
  

Для знатоков: 
* `\d+{3,5}` - арабские цифры повторяются от 3 до 5 раз (в NotePad++ нет)
* `\0` обозначает все условие поиска (не во всех редакторах доступно)  
* `$1` вместо `\1` и т.д. -- в редакторе Atom (подъязык регулярных выражений для Perl)  

[Еще один 


  
  