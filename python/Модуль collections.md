Python содержит встроенный модуль collections, который содержит специализированные типы коллекций, альтернативных традиционным list, tuple, dict:

- namedtuple
- defaultdict
- OrderedDict
- Counter
- ChainMap
- deque

#  Именованные кортежи

Именованные кортежи (тип namedtuple) — это подтип обычных кортежей в Python. У них те же функции, что и у обычных, но их значения можно получать как с помощью индекса (например, [0]), так и с помощью имени через точку (например, .name).

Приведенный ниже код:

```python
from collections import namedtuple

Point = namedtuple('Point', ['x', 'y'])     # объявляем тип Point именованного кортежа

point = Point(3, 7)                         # создаем именованный кортеж Point

print(point)
print(point.x, point.y)
print(point[0], point[1])
print(type(point))
```

выводит:

```no-highlight
Point(x=3, y=7)
3 7
3 7
<class '__main__.Point'>
```


## Функция namedtuple()

Функция namedtuple() выступает в роли фабричной функции, порождающей новые типы данных.

Сигнатура данной функции имеет вид: 

namedtuple(typename, field_names, *, rename=False, defaults=None, module=None)
То есть функция принимает два обязательных параметра typename и field_names и три необязательных rename, defaults, module, имеющих значения по умолчанию False, None, None соответственно.

Параметры typename и field_names
Параметр typename отвечает за имя создаваемого типа, параметр field_names за названия полей. Имя типа — это строка с типом, который нужно сделать именованным кортежем. В качестве параметра field_names можно использовать:

- список
- словарь
- кортеж
- строка
- множество
Параметр field_names является списком:

```python
from collections import namedtuple Point = namedtuple('Point', ['x', 'y']) # в качестве второго параметра передаем список point = Point(2, 4) print(point)
```

### Параметр rename

Допустим, мы импортируем данные из CSV-файла и превращаем каждую строку в именованный кортеж. Структура файла имеет вид:

```no-highlight
name,surname,age,class
Timur,Guev,28,11
Ruslan,Chaniev,22,9
...
```

Названия полей мы берем из заголовка CSV-файла:

```python
from collections import namedtuple

headers = ('name', 'surname', 'age', 'class')

Student = namedtuple('Student', headers)
```

Поскольку одно поле имеет название `class` (ключевое слово языка Python) мы получаем ошибку: `ValueError: Type names and field names cannot be a keyword: 'class'`.

Проблема заключается в том, что мы не знаем, будут ли в качестве названий полей у нас ключевые слова языка Python или нет. Для решения данной проблемы можно использовать параметр `rename` со значением `True`.

### Параметр defaults

Параметр `defaults` используется для того, чтобы установить значения по умолчанию для полей именованного кортежа.

Приведенный ниже код:

```python
from collections import namedtuple

Point = namedtuple('Point', ['x', 'y'], defaults=(0, 0))
point1 = Point()      # используем значения по умолчанию
point2 = Point(1, 9)

print(point1)
print(point2)
```

выводит:

```no-highlight
Point(x=0, y=0)
Point(x=1, y=9)
```

Можно указать значение по умолчанию только для некоторых полей, при этом `defaults` присваивает значения по умолчанию с конца.

Приведенный ниже код:

```python
from collections import namedtuple

Point = namedtuple('Point', ['x', 'y'], defaults=(0,))
point =  Point(7)      # используем значения по умолчанию для y
print(point)
```

выводит:

```no-highlight
Point(x=7, y=0)
```

### Параметр module

Приведенный ниже код:

```python
from collections import namedtuple

Point = namedtuple('Point', ['x', 'y'])
point = Point(1, 2)
print(type(point))
```

выводит:

```no-highlight
<class '__main__.Point'>
```

Если мы укажем допустимое имя модуля для этого аргумента, тогда атрибуту `.__ module__` результирующего именованного кортежа будет присвоено это значение.

Приведенный ниже код:

```python
from collections import namedtuple

Point = namedtuple('Point', ['x', 'y'], module='customtypes')
point = Point(1, 2)
print(type(point))
```

выводит:

```no-highlight
<class 'customtypes.Point'>
```

## Распаковка именованного кортежа

Мы можем распаковывать именованный кортеж, также как и обычный.

Приведенный ниже код:

```python
from collections import namedtuple

Person = namedtuple('Person', ['name', 'age', 'height'])

timur = Person('Тимур', 29, 170)

name, age, height = timur

print(name)
print(age)
print(height)
```

выводит:

```no-highlight
Тимур
29
170
```

