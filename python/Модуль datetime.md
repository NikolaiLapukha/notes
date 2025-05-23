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

# Тип данных timedelta

Тип данных `timedelta` представляет собой временной интервал (разница между двумя объектами `datetime` или `date`) и используется для удобного выполнения различных манипуляций над типами `datetime` или `date`.

Мы можем выбрать любые их сочетания для задания временного интервала, при этом все аргументы являются необязательными и по умолчанию равны `0`.

Приведенный ниже код:

```python
from datetime import timedelta

delta = timedelta(days=7, hours=20, minutes=7, seconds=17)

print(delta)
print(type(delta))
```

выводит:

```no-highlight
7 days, 20:07:17
<class 'datetime.timedelta'>
```

## Метод `total_seconds()`

Метод `total_seconds()` возвращает общее количество секунд, содержащееся во временном интервале`timedelta`.


Приведенный ниже код:

```python
from datetime import timedelta

delta = timedelta(days=50, seconds=27, microseconds=10, milliseconds=29000, minutes=5, hours=8, weeks=2)

print('Количество дней =', delta.days)
print('Количество секунд =', delta.seconds)
print('Количество микросекунд =', delta.microseconds)

print('Общее количество секунд =', delta.total_seconds())
```

выводит:

```no-highlight
Количество дней = 64
Количество секунд = 29156
Количество микросекунд = 10
Общее количество секунд = 5558756.00001
```

# Модуль time

В Python помимо встроенного модуля `datetime` есть еще модуль `time`, который обычно используется при работе с текущим временем.

Модуль `time` предоставляет только функции, позволяющие работать со временем.

Использование модуля `time` дает возможность:

- отображать информацию о времени, прошедшем с начала эпохи
- преобразовывать значение системного времени к удобному виду
- прерывать выполнение программы (установка паузы) на заданное количество секунд
- измерять время выполнения программы целиком или ее отдельных модулей

## Функция time()

Для того чтобы получить количество секунд, прошедших с момента начала эпохи, необходимо использовать одноименную функцию `time()` из модуля `time`.

Приведенный ниже код:

```python
import time

seconds = time.time()    # получаем количество прошедших секунд в виде float числа
print('Количество секунд с начала эпохи =', seconds)
```

выводит (на момент запуска 3131 августа 20212021 года):

```no-highlight
Количество секунд с начала эпохи = 1630387918.35439
```

В Python 3.7 добавили функцию `time_ns()`, которая возвращает целочисленное значение, представляющее то же время, прошедшее с эпохи, но в наносекундах, а не в секундах.
## Функция ctime()

Для того чтобы получить текущую дату в более удобном для человека виде, нужно использовать функцию `ctime()`. Функция `ctime()` принимает в качестве аргумента количество секунд, прошедших с начала эпохи, и возвращает строку, представляющую собой **местное (локальное) время**.

Приведенный ниже код:

```python
import time

seconds = 1630387918.354396
local_time = time.ctime(seconds)

print('Местное время:', local_time)
```

выводит:

```no-highlight
Местное время: Tue Aug 31 08:31:58 2021
```

## Функция sleep()

Функция `sleep()` используется для добавления задержки в выполнении программы. Эта функция принимает в качестве аргумента количество секунд (`secs`) и добавляет задержку в выполнении программы на указанное количество секунд.

Рассмотрим программный код:

```python
import time 

print('Before the sleep statement')
time.sleep(3)
print('After the sleep statement')
```

## Измерение времени выполнения программы

Очень часто нам бывает необходимо измерить время выполнения всей программы, либо отдельных ее частей. Чтобы найти данную величину, достаточно посчитать разницу в секундах между точкой старта и местом, где она завершает свою работу.

```python
import time

start_time = time.time()

for i in range(5): 
    print(i)
    time.sleep(1)

end_time = time.time()

elapsed_time = end_time - start_time
print(f'Время работы программы = {elapsed_time}')
```

Несмотря на простоту вышеописанного подхода, использовать его в серьезных целях, где требуется точный и независимый от операционной системы (ОС) результат, не рекомендуется. Все дело в том, что числовое значение времени, получаемое таким образом, может иметь погрешности за счет внутренних особенностей работы компьютера, в среде которого выполняется программа. Более того, системные часы могут быть подкорректированы вручную пользователем во время выполнения программы.

### Функция monotonic()

Для измерения времени выполнения программы идеально подходит функция `monotonic()`, доступная на всех ОС, так как ее результат не зависит от корректировки системных часов.

Функция `monotonic_ns()` похожа на `monotonic()`, но возвращает время в наносекундах. Работает не на всех операционных системах.

```python
import time

start_time = time.monotonic()

for i in range(5): 
    print(i)
    time.sleep(0.5)

end_time = time.monotonic()

elapsed_time = end_time - start_time
print(f'Время работы программы = {elapsed_time}')
```

### Функция perf_counter()

Для самого точного измерения времени выполнения программы следует использовать функцию `perf_counter()`. Данная функция использует таймер с наибольшим доступным разрешением, что делает эту функцию отличным инструментом для измерения времени выполнения кода на коротких интервалах.

```python
import time

start_time = time.perf_counter()

for i in range(5): 
    print(i)
    time.sleep(1)

end_time = time.perf_counter()

elapsed_time = end_time - start_time
print(f'Время работы программы = {elapsed_time}')
```


# Тип данных struct_time

В модуле `time` имеется единственный тип данных, который называется `struct_time`. Данный тип является именованным кортежем, представляющий информацию о времени. Структура представления времени `struct_time` чем-то похожа на тип `datetime`, который изучался ранее.

Именованный кортеж `struct_time` состоит из следующих атрибутов:

|Номер индекса|Атрибут|Значение|
|---|---|---|
|0|`tm_year`|диапазон от 0000 до 9999|
|1|`tm_mon`|диапазон от 1 до 12|
|2|`tm_mday`|диапазон от 1 до 31|
|3|`tm_hour`|диапазон от 0 до 23|
|4|`tm_min`|диапазон от 0 до 59|
|5|`tm_sec`|диапазон от 0 до 61|
|6|`tm_wday`|диапазон от 0 до 6, понедельник = 0|
|7|`tm_yday`|диапазон от 1 до 366|
|8|`tm_isdst`|значения -1, 0, 1|
|N/A|`tm_zone`|сокращение названия часового пояса|
|N/A|`tm_gmtoff`|смещение к востоку от UTC в секундах|

# Модуль calendar

модулю `calendar`, который содержит полезные типы данных и функции для работы с календарем.

## Модуль calendar

По умолчанию модуль `calendar` следует григорианскому календарю, где понедельник является первым днем недели (имеет номер 00), а воскресенье — последним днем недели (имеет номер 66).

## Атрибуты модуля calendar
### Атрибут day_name

Атрибут `calendar.day_name` возвращает итерируемый объект, содержащий названия дней недели на английском языке.

Приведенный ниже код:

```python
import calendar

for name in calendar.day_name:
    print(name)
```

выводит:

```no-highlight
Monday
Tuesday
Wednesday
Thursday
Friday
Saturday
Sunday
```

### Атрибут month_name

Атрибут `calendar.month_name` возвращает итерируемый объект, содержащий названия месяцев года.

Приведенный ниже код:

```python
import calendar, locale

english_names = list(calendar.month_name)
print(english_names)

locale.setlocale(locale.LC_ALL, 'ru_RU.UTF-8')

russian_names = list(calendar.month_name)
print(russian_names)
```

выводит:

```no-highlight
['', 'January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December']
['', 'Январь', 'Февраль', 'Март', 'Апрель', 'Май', 'Июнь', 'Июль', 'Август', 'Сентябрь', 'Октябрь', 'Ноябрь', 'Декабрь']
```

### Атрибут month_abbr

Атрибут `calendar.month_abbr` возвращает итерируемый объект, содержащий сокращенные названия месяцев года.

Приведенный ниже код:

```python
import calendar, locale

english_names = list(calendar.month_abbr)
print(english_names)

locale.setlocale(locale.LC_ALL, 'ru_RU.UTF-8')

russian_names = list(calendar.month_abbr)
print(russian_names)
```

выводит:

```no-highlight
['', 'Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec']
['', 'янв', 'фев', 'мар', 'апр', 'май', 'июн', 'июл', 'авг', 'сен', 'окт', 'ноя', 'дек']
```

### Атрибуты номеров дней недели

Для получения номеров дней недели можно использовать атрибуты: `MONDAY, TUESDAY, ..., SUNDAY`.

Приведенный ниже код:

```python
import calendar

print(calendar.MONDAY)
print(calendar.TUESDAY)
print(calendar.WEDNESDAY)
print(calendar.THURSDAY)
print(calendar.FRIDAY)
print(calendar.SATURDAY)
print(calendar.SUNDAY)
```

## Функции модуля calendar

По умолчанию в модуле `calendar` понедельник является первым днем недели (имеет номер 0), а воскресенье – последним днем недели (имеет номер 6).

Функция `setfirstweekday()` позволяет изменить поведение по умолчанию и устанавливает заданный день недели в качестве начала недели.

Например, чтобы установить первый будний день воскресенье, мы используем код:

```python
import calendar

calendar.setfirstweekday(calendar.SUNDAY)     # эквивалентно calendar.setfirstweekday(6)
```

### Функция setfirstweekday()

По умолчанию в модуле `calendar` понедельник является первым днем недели (имеет номер 0), а воскресенье – последним днем недели (имеет номер 6).

Функция `setfirstweekday()` позволяет изменить поведение по умолчанию и устанавливает заданный день недели в качестве начала недели.

Например, чтобы установить первый будний день воскресенье, мы используем код:

```python
import calendar

calendar.setfirstweekday(calendar.SUNDAY)     # эквивалентно calendar.setfirstweekday(6)
```


### Функция firstweekday()

Функция `firstweekday()` возвращает целое число, означающее день недели, установленное в качестве начала недели.

Приведенный ниже код:

```python
import calendar

print(calendar.firstweekday())
calendar.setfirstweekday(calendar.SUNDAY)
print(calendar.firstweekday())
```

### Функция isleap()

Проверяет является ли год высокосным, если да - возвращает `true`

Приведенный ниже код:

```python
import calendar

print(calendar.isleap(2020))
print(calendar.isleap(2021))
```

выводит:

```no-highlight
True
False
```


### Функция leapdays()

Функция `leapdays(y1, y2)` возвращает количество високосных лет в диапазоне от `y1` до `y2` (исключая), где `y1` и `y2` – годы.

Приведенный ниже код:

```python
import calendar

print(calendar.leapdays(2020, 2025))
```

выводит:

```no-highlight
2
```

### Функция weekday()

Функция `weekday(year, month, day)` возвращает день недели в виде целого числа (где 0 – понедельник, 6 – воскресенье) для заданной даты. Аргументы функции `year` – год начиная с 1970, `month` – месяц в диапазоне 1−12, `day` – число в диапазоне 1−31.

Приведенный ниже код:

```python
import calendar

print(calendar.weekday(2021, 9, 1))     # среда
print(calendar.weekday(2021, 9, 2))     # четверг
```

выводит:

```no-highlight
2
3
```

### Функция monthcalendar()

Функция `monthcalendar(year, month)` возвращает матрицу, представляющую календарь на месяц. Каждая строка матрицы представляет неделю.

Приведенный ниже код:

```python
import calendar

print(*calendar.monthcalendar(2021, 9), sep='\n')
```

выводит:

```no-highlight
[0, 0, 1, 2, 3, 4, 5]
[6, 7, 8, 9, 10, 11, 12]
[13, 14, 15, 16, 17, 18, 19]
[20, 21, 22, 23, 24, 25, 26]
[27, 28, 29, 30, 0, 0, 0]
```

### Функция monthrange()

Функция `monthrange(year, month)` возвращает день недели первого дня месяца и количество дней в месяце в виде кортежа для указанного года `year` и месяца `month`.
ava
Приведенный ниже код:

```python
import calendar

print(calendar.monthrange(2022, 1))     # январь 2022 года
print(calendar.monthrange(2021, 9))     # сентябрь 2021 года
```

выводит:

```no-highlight
(5, 31)
(2, 30)
```
### Функция month()

Функция `month(year, month, w=0, l=0)` возвращает календарь на месяц в многострочной строке. Аргументами функции являются: `year` (год), `month` (месяц), `w` (ширина столбца даты) и `l` (количество строк, отводимые на неделю).

Приведенный ниже код:

```python
import calendar

print(calendar.month(2021, 9))
print(calendar.month(2021, 10))
print(calendar.month(2021, 9, w=3))
print(calendar.month(2021, 9, l=2))
print(calendar.month(2021, 9, w=5, l=2))
```

выводит:

```no-highlight
   September 2021
Mo Tu We Th Fr Sa Su
       1  2  3  4  5
 6  7  8  9 10 11 12
13 14 15 16 17 18 19
20 21 22 23 24 25 26
27 28 29 30

    October 2021
Mo Tu We Th Fr Sa Su
             1  2  3
 4  5  6  7  8  9 10
11 12 13 14 15 16 17
18 19 20 21 22 23 24
25 26 27 28 29 30 31
```


### Функция calendar()

Функция `calendar(year, w=2, l=1, c=6, m=3)` возвращает календарь на весь год в виде многострочной строки. Аргументами функции являются: `year` (год),  `w` (ширина столбца даты), `l` (количество строк, отводимые на неделю), `c` (количество пробелов между столбцом месяца) и  `m` (количество столбцов).

Приведенный ниже код:

```python
import calendar

print(calendar.calendar(2021))
```

выводит:

```no-highlight
                                  2021

      January                   February                   March
Mo Tu We Th Fr Sa Su      Mo Tu We Th Fr Sa Su      Mo Tu We Th Fr Sa Su
             1  2  3       1  2  3  4  5  6  7       1  2  3  4  5  6  7
 4  5  6  7  8  9 10       8  9 10 11 12 13 14       8  9 10 11 12 13 14
11 12 13 14 15 16 17      15 16 17 18 19 20 21      15 16 17 18 19 20 21
18 19 20 21 22 23 24      22 23 24 25 26 27 28      22 23 24 25 26 27 28
25 26 27 28 29 30 31                                29 30 31
```

# Модуль dateutil

Установка модуля:

```python
pip install python-dateutil
```

## Работа с модулем

После установки можно начинать работать с самим модулем.

Dateutil разбит на несколько подклассов:

- easter,
- parser,
- relativedelta,
- rrule,
- tz
- и некоторые другие.

## Импорт нужных методов

```python
# нужно импортировать модуль datetime
from datetime import datetime, date

from dateutil.relativedelta import relativedelta, FR, TU
from dateutil.easter import easter
from dateutil.parser import parse
from dateutil import rrule
```

## Datetime и relativedata

Итак, dateutil зависит от модуля datetime. Он использует его объекты.

Подкласс `relativedelta` расширяет возможности модуля datetime, предоставляя функции для работы с датами и временем относительно полученных данных.

```python
# Создание нескольких объектов datetime для работы
dt_now = datetime.now()
print("Дата и время прямо сейчас:", dt_now)
dt_today = date.today()
print("Дата сегодня:", dt_today)
# Следующий месяц
print(dt_now + relativedelta(months=+1))
 
# Следующий месяц, плюс одна неделя
print(dt_now + relativedelta(months=+1, weeks=+1))
 
# Следующий месяц, плюс одна неделя, в 17:00.
print(dt_now + relativedelta(months=+1, weeks=+1, hour=17))
 
# Следующая пятница
print(dt_today + relativedelta(weekday=4))
```

## Datetime и easter

Подкласс `easter` используется для вычисления даты и времени с учетом разных календарей.

Этот подкласс довольно компактный и включает всего один аргумент с тремя вариантами:

- Юлианский календарь `EASTER_JULIAN=1`.
- Григорианский календарь `EASTER_ORTHODOX=2`.
- Западный календарь `EASTER_WESTERN=3`.

```python
print("Юлианский календарь:", easter(2021, 1))
print("Григорианский календарь:", easter(2021, 2))
print("Западный календарь:", easter(2021, 3))
```

Вывод:

```python
Юлианский календарь: 2021-04-19
Григорианский календарь: 2021-05-02
Западный календарь: 2021-04-04
```

## Datetime и parser

Подкласс `parser` добавляет продвинутый парсер даты и времени, с помощью которого можно парсить разные форматы даты и времени.

```python
print(parse("Thu Sep 25 10:36:28 BRST 2003"))
 
# Мы также можем игнорировать часовой пояс
print(parse("Thu Sep 25 10:36:28 BRST 2003", ignoretz=True))
 
# Мы можем не указывать часовой пояс или год.
print(parse("Thu Sep 25 10:36:28"))
 
# Мы можем подставить переменные
default = datetime(2020, 12, 25)
print(parse("10:36", default=default))
```

## Datetime и rrule

Подкласс `rrule` использует пользовательский ввод для предоставлении информации о повторяемости объекта `datetime`.

```python
# Вывод 5 дней от даты старта
print(list(rrule.rrule(rrule.DAILY, count=5, dtstart=parse("20201202T090000"))))
 
# Вывод 3 дней от даты старта с интервалом 10
print(list(rrule.rrule(rrule.DAILY, interval=10, count=3, dtstart=parse("20201202T090000"))))
 
# Вывод 3 дней с интервалом неделя
print(list(rrule.rrule(rrule.WEEKLY, count=3, dtstart=parse("20201202T090000"))))
 
# Вывод 3 дней с интервалом месяц
print(list(rrule.rrule(rrule.MONTHLY, count=3, dtstart=parse("20201202T090000"))))
 
# Вывод 3 дней с интервалом год
print(list(rrule.rrule(rrule.YEARLY, count=3, dtstart=parse("20201202T090000"))))
```

# Модуль Arrow  

Модуль Arrow в Python – это библиотека, заменяющая datetime. Это позволяет легко создавать экземпляры даты и времени с учетом часового пояса. Это простой модуль с удобным для человека подходом к созданию, обработке, форматированию и преобразованию дат, времени и временных меток.  

Установка:

```python
pip install arrow  
```

## Пример использования 

Код:

```python
import arrow
utc_now = arrow.utcnow()
now = arrow.now('Europe/London')
local_now = arrow.now()
print(utc_now)
print(now)
print(local_now)
```

Вывод:

```python
2025-05-18T17:01:40.964745+00:00                                                                   
2025-05-18T18:01:40.965014+01:00                                                                    
2025-05-18T20:01:40.965047+03:00 
```

## Преобразование часового пояса  

```python
pst_time = ist_time.to('US/Pacific') 
print('Current PST Time =', pst_time)  
```

## Дата в форматированную строку  

```python
print('Formatted Date =', local_time.format()) 
print('Specific Formatted Date =', local_time.format('YYYY-MM-DD HH:mm:ss ZZ'))  
```

## Создание экземпляра даты из аргументов  

```python
dt = arrow.get(2018, 9, 26) 
print(dt)  
```

## Манипуляции с датой и временем  

Мы можем использовать функции replace() и shift() для получения будущих и прошлых дат.  

```python
utc_time = arrow.utcnow() 
print('Current UTC Time =', utc_time) 
utc_time_updated = utc_time.replace(year=2019, month=6) 
print('Updated UTC Time =', utc_time_updated) 
utc_time_updated = utc_time.shift(years=-2, weeks=4) 
print('Updated UTC Time =', utc_time_updated)  
```

Вывод:

```python
Current UTC Time = 2018-09-26T06:16:54.727167+00:00 
Updated UTC Time = 2019-06-26T06:16:54.727167+00:00 
Updated UTC Time = 2016-10-24T06:16:54.727167+00:00  
```

