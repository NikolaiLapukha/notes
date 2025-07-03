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

## Атрибуты _fields, _field_defaults

Именованные кортежи имеют два дополнительных атрибута: `_fields` и `_field_defaults`. Первый атрибут содержит кортеж строк, в котором перечислены имена полей. Второй атрибут содержит словарь, который сопоставляет имена полей с соответствующими значениями по умолчанию, если таковые имеются.

Приведенный ниже код:

```python
from collections import namedtuple

Person = namedtuple('Person', ['name', 'age', 'height'])

tim = Person('Тимур', 29, 170)

print(tim)
print(tim._fields)
print(Person._fields)
```

выводит:

```no-highlight
Person(name='Тимур', age=29, height=170)
('name', 'age', 'height')
('name', 'age', 'height')
```

## Методы _make(), _replace(), _asdict()

Именованные кортежи (тип `namedtuple`) являются производными от обычных кортежей (тип `tuple`), поэтому наследуют их методы, а также добавляют три новых: `_make(), _replace(), _asdict()`.

### Метод _make()

Метод `_make()` используется для создания именованных кортежей из итерируемых объектов (список, кортеж, строка, словарь и т.д.).

Приведенный ниже код:

```python
from collections import namedtuple

Person = namedtuple('Person', ['name', 'age', 'height'])

timur = Person._make(['Timur', 29, 170])

print(timur)
```

выводит:

```no-highlight
Person(name='Timur', age=29, height=170)
```

### Метод _asdict()

Мы можем преобразовывать именованные кортежи в словари с помощью метода `_asdict()`. Этот метод возвращает словарь, в котором имена полей используются в качестве ключей. Ключи результирующего словаря находятся в том же порядке, что и поля в исходном именованном кортеже.

Приведенный ниже код:

```python
from collections import namedtuple

Person = namedtuple('Person', ['name', 'age', 'height'])

timur = Person._make(['Timur', 29, 170])

print(timur._asdict())
```

выводит:

```no-highlight
{'name': 'Timur', 'age': 29, 'height': 170}
```

### Метод _replace()

Метод `_replace()` позволяет создавать новые именованные кортежи на основании уже существующих с заменой некоторых значений. Потребность в данном методе вызвана тем, что именованные кортежи являются неизменяемыми.

Приведенный ниже код:

```python
from collections import namedtuple

Person = namedtuple('Person', ['name', 'age', 'height', 'country'])

timur1 = Person('Тимур', 29, 170, 'Russia')
timur2 = timur1._replace(age=30, country='Germany')

print(timur1)
print(timur2)
```

выводит:

```no-highlight
Person(name='Тимур', age=29, height=170, country='Russia')
Person(name='Тимур', age=30, height=170, country='Germany')
```


# defaultdict
Основная проблема при работе с обычными словарями (тип `dict`) – это попытка получить доступ (или изменить значение) по несуществующему ключу. Это приводит к возникновению ошибки `KeyError`. Несмотря на то что мы научились решать данную проблему штатными способами, стандартная библиотека предоставляет тип данных `defaultdict`.

Тип `defaultdict` ведет себя почти так же, как обычный словарь `dict`, но если мы попытаемся получить доступ (или изменить значение) по несуществующему ключу, то `defaultdict` автоматически создаст ключ и сгенерирует для него значение по умолчанию. Такое поведение делает `defaultdict` удобным вариантом обработки недостающих ключей в словарях.

Для того чтобы не возникало ошибки при обращении по несуществующему ключу с помощью квадратных скобок, достаточно использовать альтернативный вариант словаря – `defaultdict`.

Приведенный ниже код:

```python
from collections import defaultdict

info = defaultdict(int)       # создаем словарь со значением по умолчанию 0

info['name'] = 'Timur'
info['age'] = 29
info['job'] = 'Teacher'

print(info['salary'])
print(info)
```

выводит:

```no-highlight
0
defaultdict(<class 'int'>, {'name': 'Timur', 'age': 29, 'job': 'Teacher', 'salary': 0})
```

Функция `defaultdict()` принимает в качестве аргумента тип элемента по умолчанию. Таким образом, для ключей, к которым происходит обращение, словарь `defaultdict` поставит в соответствие дефолтный элемент данного типа:

- для `int` – число `0`
- для `float` – число `0.0`
- для `bool` – значение `False`
- для `str` – пустая строка `''`
- для `list` – пустой список `[]`
- для `tuple` – пустой кортеж `()`
- для `set` – пустое множество `set()`
- для `dict` – пустой словарь `{}`

Помимо первого аргумента – типа элемента по умолчанию – мы можем передать второй аргумент: словарь, на основании которого будет создан `defaultdict`.

Приведенный ниже код:

```python
from collections import defaultdict

info = defaultdict(int, {'name': 'Timur', 'age': 29, 'job': 'Teacher'})

print(info['name'])
print(info['salary'])
print(info)
```

# тип данных OrderedDict

Тип `OrderedDict` является подтипом типа `dict`, сохраняющий порядок, в котором пары "ключ-значение" вставляются в словарь. Когда мы перебираем объект типа `OrderedDict`, его элементы перебираются в исходном порядке.

## Изменение OrderedDict словаря

Тип `OrderedDict` является изменяемым. Мы можем вставлять новые элементы, обновлять и удалять существующие элементы. Если мы вставим новый элемент в существующий `OrderedDict` словарь, то этот элемент добавится в конец словаря.

Приведенный ниже код:

```python
from collections import OrderedDict

numbers = OrderedDict(one=1, two=2, three=3)

print(numbers)

numbers['four'] = 4

print(numbers)
```

выводит:

```no-highlight
OrderedDict([('one', 1), ('two', 2), ('three', 3)])
OrderedDict([('one', 1), ('two', 2), ('three', 3), ('four', 4)])
```


## Итерирование по OrderedDict словарю

Доступ к элементам и итерирование по `OrderedDict` словарям работает так же, как и у обычных словарей. Мы можем перебирать ключи напрямую или можем использовать словарные методы `items()`, `keys()` и `values()`.

Приведенный ниже код:

```python
from collections import OrderedDict

numbers = OrderedDict(one=1, two=2, three=3)

# обращение по ключу
print(numbers['one'])
print(numbers['three'])

print()

# перебор ключей напрямую
for key in numbers:
    print(key, '->', numbers[key])

print()

# перебор пар (ключ, значение) через метод
for key, value in numbers.items():
    print(key, '->', value)

print()

# перебор ключей через метод
for key in numbers.keys():
    print(key, '->', numbers[key])

print()

# перебор значений через метод
for value in numbers.values():
    print(value)
```


Обычные словари (тип `dict`) начиная с Python 3.8 также поддерживают использование встроенной функции `reversed()`.

## Методы popitem() и move_to_end()

`OrderedDict` словари имеют два полезных метода:

- метод `move_to_end()` позволяет переместить существующий элемент либо в конец, либо в начало словаря
- метод `popitem()` позволяет удалить и вернуть элемент либо из конца, либо из начала словаря

### Метод move_to_end()

Методу `move_to_end()` можно передать два аргумента:

- `key` (обязательный аргумент) – ключ, который идентифицирует перемещаемый элемент
    
- `last` (необязательный аргумент) – логическое значение (тип `bool`), которое определяет, в какой конец словаря мы перемещаем элемент, значение `True` (по умолчанию) перемещает элемент в конец, значение `False` – в начало

Приведенный ниже код:

```python
from collections import OrderedDict

numbers = OrderedDict(one=1, two=2, three=3)
print(numbers)

numbers.move_to_end('one')       # last=True
print(numbers)

numbers.move_to_end('three', last=False)       # last=False
print(numbers)
```

выводит:

```no-highlight
OrderedDict([('one', 1), ('two', 2), ('three', 3)])
OrderedDict([('two', 2), ('three', 3), ('one', 1)])
OrderedDict([('three', 3), ('two', 2), ('one', 1)])
```
### Метод popitem()

Метод `popitem()` по умолчанию удаляет и возвращает элемент в порядке [LIFO](https://ru.wikipedia.org/wiki/LIFO) (Last-In/First-Out, последний пришел/первый ушел). Другими словами, метод `popitem()` удаляет элементы с конца словаря.

Приведенный ниже код:

```python
from collections import OrderedDict

numbers = OrderedDict(one=1, two=2, three=3)

print(numbers.popitem())
print(numbers)

print(numbers.popitem())
print(numbers)
```

выводит:

```no-highlight
('three', 3)
OrderedDict([('one', 1), ('two', 2)])
('two', 2)
OrderedDict([('one', 1)])
```
## Сравнение словарей

При сравнении на равенство обычных словарей (тип `dict`) порядок расположения их элементов **неважен**.

Приведенный ниже код:

```python
letters1 = dict(a=1, b=2, c=3, d=4)
letters2 = {'b': 2, 'a': 1, 'c': 3, 'd': 4}
letters3 = dict([('a', 1), ('b', 2), ('c', 3), ('d', 4)])

print(letters1 == letters2)
print(letters1 == letters3)
```

выводит:

```no-highlight
True
True
```

При сравнение на равенство `OrderedDict` словарей порядок расположения их элементов **важен**.

Приведенный ниже код:

```python
from collections import OrderedDict

letters1 = OrderedDict(a=1, b=2, c=3, d=4)
letters2 = OrderedDict({'b': 2, 'a': 1, 'c': 3, 'd': 4})
letters3 = OrderedDict([('a', 1), ('b', 2), ('c', 3), ('d', 4)])

print(letters1 == letters2)
print(letters1 == letters3)
```

выводит:

```no-highlight
False
True
```

При сравнении на равенство обычного словаря (тип `dict`) и `OrderedDict` словаря порядок расположения их элементов **неважен**.

# тип данных Counter

Тип `Counter` является подтипом типа `dict`, специально разработанный для подсчета хешируемых объектов в Python. `Counter` хранит объекты в качестве ключей, а их количество — в качестве значений.

## Создание Counter

Существует несколько способов создания объектов типа `Counter`. Самый простой и распространенный способ основан на передаче коллекции с данными (список, строка, кортеж и т.д.) в конструктор типа.

Приведенный ниже код:

```python
from collections import Counter

counter = Counter('mississippi')     # создаем счетчик на основе строки
print(counter)
```

выводит:

```no-highlight
Counter({'i': 4, 's': 4, 'p': 2, 'm': 1})
```

Мы можем создавать объекты типа `Counter`, явно указывая начальные значения количества объектов.

Приведенный ниже код:

```python
from collections import Counter

counter1 = Counter({'i': 4, 's': 4, 'p': 2, 'm': 1})
counter2 = Counter(i=4, s=4, p=2, m=1)

print(counter1)
print(counter2)
```

выводит:

```no-highlight
Counter({'i': 4, 's': 4, 'p': 2, 'm': 1})
Counter({'i': 4, 's': 4, 'p': 2, 'm': 1})
```

## Обновление данных

Для изменения объектов типа `Counter` мы можем использовать метод `update()`. Реализация данного метода не заменяет значения как у обычных словарей (тип `dict`), а суммирует существующие значения. При этом для новых объектов метод `update()` создает новые пары `ключ: количество`.

Приведенный ниже код:

```python
from collections import Counter

letters = Counter({'i': 4, 's': 4, 'p': 2, 'm': 1})
print(letters)

letters.update('missouri')
print(letters)
```

выводит:

```no-highlight
Counter({'i': 4, 's': 4, 'p': 2, 'm': 1})
Counter({'i': 6, 's': 6, 'p': 2, 'm': 2, 'o': 1, 'u': 1, 'r': 1})
```

Мы также можем передавать методу `update()` другой объект типа `Counter`, либо обычный словарь (тип `dict`).

## Доступ к элементам и итерирование

Доступ к элементам и итерирование по `Counter` словарям работает так же, как и у обычных словарей. Мы можем перебирать ключи напрямую или можем использовать словарные методы `items()`, `keys()` и `values()`.

