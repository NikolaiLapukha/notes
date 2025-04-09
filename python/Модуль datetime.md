Для удобной работы с датой и временем в Python есть модуль `datetime`. Данный модуль используется для работы со временем и датами, позволяя представлять данную информацию в наиболее удобной форме.
Типы данных модуля `datetime`:
- `date` - представляет собой информацию о дате, исключая данные о времени, на основе Григорианского календаря.
- `time` - представляет собой информацию о времени, полностью исключая сведения о дате.
- `datime` - содержит информацию о времени и дате, основываясь на данных из Григорианского календаря.
- `timedelta` - описывает определенный период во времени, который находится между двумя различными моментами.
- `tzinfo` - представляет различные сведения о часовом поясе.
- `timezone` - описывает время, руководствуясь стандартом UTC.

# Тип данных `date`

При создании новой даты (тип данных `date`) нужно указать год, месяц и день.

```python
from datetime import date

my_date = date(1992, 10, 6)    # тип date: год + месяц + день

print(my_date)
print(type(my_date))
```


выводит:

```python
1992-10-06
<class 'datetime.date'>
```

Если необходимо получить информацию о текущей дате на компьютере, на котором выполняется программа, то используется встроенный метод `today()`.

```python
from datetime import date

creation_date = date.today()
print(creation_date)
```


Методы `fromordinal()` и `toordinal()` позволяют создать дату из номера дня, начиная с `0001-01-01`, и наоборот, преобразовать дату в номер дня.

```python
from datetime import date

date1 = date.fromordinal(365)     # дата, соответствуюшая номеру дня 365
date2 = date(1999, 12, 26)

print(date1)
print(date2.toordinal())     
```

выводит:

```no-highlight
0001-12-31
730114
```
# Тип данных time

Тип данных (класс) `time` используется для представления данных о времени и включает информацию о часах, минутах, секундах и микросекундах. Данный тип данных полностью игнорирует информацию о дате.

При создании времени (тип данных `time`) нужно указать часы, минуты, секунды и микросекунды.

```python
from datetime import time

my_time = time(11, 20, 54, 1234)    # тип time: часы + минуты + секунды + микросекунды

print(my_time)
print(type(my_time))
```

В отличие от дат (тип данных `date`), чтобы создать объект типа `time`, необязательно указывать все его атрибуты в конструкторе. Недостающие данные о времени автоматически заполняются нулями.


# Сравнение дат и времени

Дату (тип `date`) и время (тип `time`) можно сравнивать с помощью операторов `==, !=, <, >, <=` и  `>=`.

```python
from datetime import date, time

date1 = date(2022, 10, 15)
date2 = date(1999, 12, 26)

time1 = time(13, 10, 5)
time2 = time(21, 32, 59)

print(date1 < date2)
print(time1 < time2)
```

выводит

```python
False
True
```

## **`timedelta`** 

`timedelta` — это класс из модуля `datetime` в Python, который представляет **разницу между двумя датами или временем**. Он используется для выполнения арифметических операций с датами.

```python
from datetime import datetime, timedelta

start_date = datetime.strptime("05.11.2021", "%d.%m.%Y").date()
end_date = datetime.strptime("09.11.2021", "%d.%m.%Y").date()

current_date = start_date
while current_date <= end_date:
    print(current_date)  # Выводим каждую дату в диапазоне
    current_date += timedelta(days=1)  # Увеличиваем дату на 1 день
```
# Встроенные функции str() и repr()

На практике часто используются две встроенные функции `str()` и `repr()`. С их помощью можно получить строковое представление объекта.

Встроенная функция `str()` возвращает объект **в неформальном (понятном человеку)** строковом представлении.

Приведенный ниже код:

```python
from datetime import date, time

my_date = date(2021, 12, 31)
my_time = time(11, 20, 54)

print(my_date)
print(my_time)
```


выводит:

```no-highlight
2021-12-31
11:20:54
```

По сути мы наблюдаем результат работы функции `str()`, которая вызывается за кулисами и преобразует указанные объекты в читаемый для человека вид.

Приведенный ниже код использует явный вызов функции `str()` и идентичен коду выше.

```python
from datetime import date, time

my_date = date(2021, 12, 31)
my_time = time(11, 20, 54)

print(str(my_date))
print(str(my_time))
```

Встроенная функция `repr()` возвращает объект **в формальном (понятном интерпретатору)** строковом представлении.

Приведенный ниже код:

```python
from datetime import date, time

my_date = date(2021, 12, 31)
my_time = time(11, 20, 54)

print(repr(my_date))
print(repr(my_time))
```

выводит:

```no-highlight
datetime.date(2021, 12, 31)
datetime.time(11, 20, 54)
```

# Форматирование даты и времени

По умолчанию вывод даты и времени осуществляется в ISO формате:

- дата имеет вид: `YYYY-MM-DD`
- время имеет вид: `HH:MM:SS` или `HH:MM:SS.ffffff`

Для форматированного вывода даты и времени используется метод `strftime()` (для обоих типов `date` и `time`).

Приведенный ниже код:

```python
from datetime import date, time

my_date = date(2021, 8, 10)
my_time = time(7, 18, 34)

print(my_date)                             # вывод в ISO формате
print(my_time)                             # вывод в ISO формате

print(my_date.strftime('%d/%m/%y'))        # форматированный вывод даты
print(my_date.strftime('%A %d, %B %Y'))    # форматированный вывод даты
print(my_time.strftime('%H.%M.%S'))        # форматированный вывод времени
```

выводит:

```python
2021-08-10
07:18:34
10/08/21
Tuesday 10, August 2021
07.18.34
```


| Формат | Значение                                                                                                                   | Пример                                                                                                             |
| ------ | -------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| `%a`   | Сокращенное название дня недели                                                                                            | Sun, Mon, …, Sat (en_US)  <br>Пн, Вт, ..., Вс (ru_RU)                                                              |
| `%A`   | Полное название дня недели                                                                                                 | Sunday, Monday, …, Saturday (en_US)  <br>понедельник, ..., воскресенье (ru_RU)                                     |
| `%w`   | Номер дня недели [0, …, 6]                                                                                                 | 0, 1, …, 6 (0=воскресенье, 6=суббота)                                                                              |
| `%d`   | День месяца [01, …, 31]                                                                                                    | 01, 02, …, 31                                                                                                      |
| `%b`   | Сокращенное название месяца                                                                                                | Jan, Feb, …, Dec (en_US);  <br>янв, ..., дек (ru_RU)                                                               |
| `%B`   | Полное название месяца                                                                                                     | January, February, …, December (en_US);  <br>Январь, ..., Декабрь (ru_RU)                                          |
| `%m`   | Номер месяца [01, …,12]                                                                                                    | 01, 02, …, 12                                                                                                      |
| `%y`   | Год без века [00, …, 99]                                                                                                   | 00, 01, …, 99                                                                                                      |
| `%Y`   | Год с веком                                                                                                                | 0001, 0002, …, 2013, 2014, …, 9999  <br>В Linux год выводится без ведущих нулей:  <br>1, 2, …, 2013, 2014, …, 9999 |
| `%H`   | Час (24-часовой формат) [00, …, 23]                                                                                        | 00, 01, …, 23                                                                                                      |
| `%I`   | Час (12-часовой формат) [01, …, 12]                                                                                        | 01, 02, …, 12                                                                                                      |
| `%p`   | До полудня или после (при 12-часовом формате)                                                                              | AM, PM (en_US)                                                                                                     |
| `%M`   | Число минут [00, …, 59]                                                                                                    | 00, 01, …, 59                                                                                                      |
| `%S`   | Число секунд [00, …, 59]                                                                                                   | 00, 01, …, 59                                                                                                      |
| `%f`   | Число микросекунд                                                                                                          | 000000, 000001, …, 999999                                                                                          |
| `%z`   | Разница с UTC в формате ±HHMM[SS[.ffffff]]                                                                                 | +0000, -0400, +1030, +063415, ...                                                                                  |
| `%Z`   | Временная зона                                                                                                             | UTC, EST, CST                                                                                                      |
| `%j`   | День года [001,366]                                                                                                        | 001, 002, …, 366                                                                                                   |
| `%U`   | Номер недели в году (неделя начинается с воскр.).Неделя, предшествующая первому воскресенью, является нулевой. [00, …, 53] | 00, 01, …, 53                                                                                                      |
| `%W`   | Номер недели в году (неделя начинается с пон.) Неделя, предшествующая первому понедельнику, является нулевой. [00, …, 53]  | 00, 01, …, 53                                                                                                      |
| `%c`   | Дата и время                                                                                                               | Tue Aug 16 21:30:00 1988 (en_US);  <br>03.01.2019 23:18:32 (ru_RU)                                                 |
| `%x`   | Дата                                                                                                                       | 08/16/88 (None); 08/16/1988 (en_US);  <br>03.01.2019 (ru_RU)                                                       |
| `%X`   | Время                                                                                                                      |                                                                                                                    |

Приведенный ниже код:

```python
from datetime import date, time

my_date = date(2021, 8, 10)
my_time = time(7, 18, 34)

print(my_date.gg('%a %A %w %d %b %B %m %y %Y %H %I %p %M %S %f %z %Z %j %U %W %c %x %X'))
print(my_time.strftime('%a %A %w %d %b %B %m %y %Y %H %I %p %M %S %f %z %Z %j %U %W %c %x %X'))
```

выводит:

```no-highlight
Tue Tuesday 2 10 Aug August 08 21 2021 00 12 AM 00 00 000000   222 32 32 Tue Aug 10 00:00:00 2021 08/10/21 00:00:00
Mon Monday 1 01 Jan January 01 00 1900 07 07 AM 18 34 000000   001 00 01 Mon Jan  1 07:18:34 1900 01/01/00 07:18:34
```

## Использование локализации

Для того чтобы использовать конкретную локализацию (перевод на язык), нужно использовать модуль `locale`.

Приведенный ниже код устанавливает русскую локализацию:

```python
from datetime import date
import locale

locale.setlocale(locale.LC_ALL, 'ru_RU.UTF-8')

my_date = date(2021, 8, 10)
print(my_date.strftime("%A %d, %B %Y"))    # форматированный вывод даты в русской локализации
```

и выводит:

```no-highlight
вторник 10, Август 2021
```

Для того чтобы получить строковое представление объектов типа `date` и `time` в ISO формате, можно воспользоваться методом `isoformat()`.

Приведенный ниже код:

```python
from datetime import date, time

my_date = date(2021, 12, 31)
my_time = time(21, 15, 17)

print('Дата: ' + my_date.isoformat())
print('Время: ' + my_time.isoformat())
```

выводит:

```no-highlight
Дата: 2021-12-31
Время: 21:15:17
```

# Преобразование строки в дату и время

## Самостоятельное преобразование данных

```python
from datetime import date, time

day, month, year = input('Введите дату в формате ДД.ММ.ГГГГ').split('.')
hour, minute, second = input('Введите время в формате ЧЧ:ММ:СС').split(':')

my_date = date(int(year), int(month), int(day))        # создаем объект типа date
my_time = time(int(hour), int(minute), int(second))    # создаем объект типа time

print(my_date)
print(my_time)
```

преобразует данные из строки в дату и время и выводит:

```no-highlight
2021-11-13
21:34:59
```

Так же можно сделать с обработкой исключений и вводом в цикле до тех пор пока не будут введены верные данные.

```python
from datetime import date, time

while True:
    try:
        day, month, year = input('Введите дату в формате ДД.ММ.ГГГГ').split('.')

        my_date = date(int(year), int(month), int(day))

        print('Введена корректная дата:', my_date)
        break
    except ValueError:    # перехватываем ошибку типа ValueError
        print('Введенная дата не является корректной, попробуйте еще раз')
```
## Преобразование строки в дату с помощью метода fromisoformat()

Для того чтобы преобразовать строку из ISO формата в объект даты (`date`) или в объект времени (`time`), можно использовать метод `fromisoformat()`.

Приведенный ниже код:

```python
from datetime import date, time

my_date = date.fromisoformat('2020-01-31')
my_time = time.fromisoformat('10:20:30')

print(my_date)
print(my_time)
print(type(my_date))
print(type(my_time))
```

выводит:

```no-highlight
2020-01-31
10:20:30
<class 'datetime.date'>
<class 'datetime.time'>
```

# Тип данных datetime

Типы данных `date` и `time` позволяют работать по отдельности с датами и временами. Однако на практике чаще требуется работать одновременно и с датой, и со временем. Для таких целей используется тип данных `datetime` из одноименного модуля `datetime`.

Чтобы иметь возможность использовать этот тип данных, необходимо предварительно его импортировать из модуля `datetime`:

```python
from datetime import datetime
```

Приведенный ниже код:

```python
from datetime import datetime

my_datetime = datetime(1992, 10, 6, 9, 40, 23, 51204)    # создаем полную дату-время
only_date = datetime(2021, 12, 31)                       # создаем дату-время с нулевой временной информацией

print(my_datetime)
print(only_date)
print(type(my_datetime))
```

выводит:

```python
1992-10-06 09:40:23.051204
2021-12-31 00:00:00
<class 'datetime.datetime'>
```

## Методы combine(), date(), time()

Сформировать новый объект типа `datetime` можно с помощью двух разных объектов, представляющих дату и время (`date` и `time`). Для этого используется метод `combine()`.

Приведенный ниже код:

```python
from datetime import date, time, datetime

my_date = date(1992, 10, 6)
my_time = time(10, 45, 17)
my_datetime = datetime.combine(my_date, my_time)

print(my_datetime)
```

выводит:

```no-highlight
1992-10-06 10:45:17
```

Если, наоборот, нужно получить из даты-времени (тип `datetime`) по отдельности дату (тип `date`) и время (тип `time`), то используются методы `date()` и `time()` соответственно.

```python
from datetime import datetime

my_datetime = datetime(2022, 10, 7, 14, 15, 45)
my_date = my_datetime.date()                     # получаем только дату (тип date)
my_time = my_datetime.time()                     # получаем только время (тип time)
```

## Методы now(), utcnow(), today()

Для того, чтобы получить текущее время на момент исполнения программы, используются методы `now()` и `utcnow()` для локального и UTC времени соответственно.

Приведенный ниже код:

```python
from datetime import datetime

datetime_now = datetime.now()
datetime_utcnow = datetime.utcnow()

print(datetime_now)           # текущее локальное время (московское) на момент запуска программы
print(datetime_utcnow)        # текущее UTC время на момент запуска программы
```

выводит:

```no-highlight
2021-08-13 08:03:43.224568
2021-08-13 05:03:43.224568
```

С выходом Python 3.12 метод `utcnow()` устарел и подготовлен к удалению в будущих версиях языка, поэтому вместо него рекомендуется использовать метод `now()`, указав в качестве аргумента константу `UTC` модуля `datetime`.

Приведенный ниже код:

```python
from datetime import datetime, UTC

print(datetime.now(UTC))
```


## Метод timestamp()

Метод `timestamp()` позволяет преобразовать объект типа `datetime` в количество секунд, прошедших с момента начала эпохи. Данный метод возвращает значение типа `float`.

Приведенный ниже код:

```python
from datetime import datetime

my_datetime = datetime(2021, 10, 13, 8, 10, 23)

print(my_datetime.timestamp())
```

выводит:

```no-highlight
1634101823.0
```

## Метод fromtimestamp()

Метод `fromtimestamp()` позволяет преобразовать количество секунд, прошедших с момента начала эпохи, в объект типа `datetime`. Данный метод является обратным по отношению к методу `timestamp()`.

Приведенный ниже код:

```python
from datetime import datetime

my_datetime = datetime.fromtimestamp(1634101823.0)

print(my_datetime)
```

выводит:

```no-highlight
2021-10-13 08:10:23
```

## Метод strptime

Метод преобразует строку (первый аргумент) в объект `datetime` согласно переданному формату (второй аргумент).

Приведенный ниже код работает аналогично коду выше:

```python
from datetime import datetime

datetime_str = input('Введите дату/время в формате ДД.ММ.ГГГГ ЧЧ:ММ:СС')

my_datetime = datetime.strptime(datetime_str, '%d.%m.%Y %H:%M:%S')

print(my_datetime)
```

Рассмотрим примеры работы данного метода.

Приведенный ниже код:

```python
from datetime import datetime

datetime0 = datetime.strptime('10.08.2034 13:55:59', '%d.%m.%Y %H:%M:%S')
datetime1 = datetime.strptime('10/08/21', '%d/%m/%y')
datetime2 = datetime.strptime('Tuesday 10, August 2021', '%A %d, %B %Y')
datetime3 = datetime.strptime('18.20.34', '%H.%M.%S')
datetime4 = datetime.strptime('2021/08/10', '%Y/%m/%d')
datetime5 = datetime.strptime('10.08.2021 (Tuesday, August)', '%d.%m.%Y (%A, %B)')
datetime6 = datetime.strptime('Year: 2021, Month: 08, Day: 10, Hour: 18.', 'Year: %Y, Month: %m, Day: %d, Hour: %H.')

print(datetime0, datetime1, datetime2, datetime3, datetime4, datetime5, datetime6, sep='\n')
```

выводит:

```no-highlight
2034-08-10 13:55:59
2021-08-10 00:00:00
2021-08-10 00:00:00
1900-01-01 18:20:34
2021-08-10 00:00:00
2021-08-10 00:00:00
2021-08-10 18:00:00
```

