## Функция partial()

Частичное применение функций — это техника, основанная на возможности возвращать функции из других функций.

 Функция `partial()` возвращает `partial` объект, который при вызове ведет себя как функция.

Приведенный выше код можно переписать с использованием функции `partial()` в виде:

```python
from functools import partial

def multiply(a, b):
    return a * b

double = partial(multiply, 2)
triple = partial(multiply, 3)
```

В нашем случае `partial` объекты `double` и `triple` ведут себя как функция `multiply()`, которой в качестве первого аргумента передали число 22 в первом случае и 33 во втором.  

Приведенный ниже код:

```python
print(double(5))        # 2 * 5
print(triple(10))       # 3 * 10
```

выводит:

```undefined
10
30
```


Обратите внимание на то, что мы зафиксировали только один аргумент, поэтому новые `partial` объекты теперь ожидают только один аргумент. Если мы попытаемся передать более одного аргумента, то получим ошибку.

Приведенный ниже код:

```python
print(double(5, 6))
```

приводит к возникновению ошибки:

```no-highlight
TypeError: multiply() takes 2 positional arguments but 3 were given
```


### Объекты, возвращаемые функцией partial()

Как уже было сказано выше, функция `partial()` возвращает специальные `partial` объекты, которые при вызове ведут себя как функции. Такие объекты содержат три полезных атрибута:

- `func` — исходная функция
- `args` — зафиксированные позиционные аргументы (тип `tuple`)
- `keywords` — зафиксированные именованные аргументы (тип `dict`)

При необходимости к ним можно получить доступ с помощью стандартной точечной нотации.

Приведенный ниже код:

```python
from functools import partial

def pretty_print(text, symbol, count):
    print(symbol * count)
    print(text)
    print(symbol * count)

star_pretty_print = partial(pretty_print, 'Hi!!!', symbol='*')

star_pretty_print(count=7)

print(star_pretty_print.args)
print(star_pretty_print.keywords)

star_pretty_print.func('Исходная функция', symbol='~', count=20)
```

выводит:

```no-highlight
*******
Hi!!!
*******
('Hi!!!',)
{'symbol': '*'}
~~~~~~~~~~~~~~~~~~~~
Исходная функция
~~~~~~~~~~~~~~~~~~~~
```

### Функция update_wrapper()

Как несложно заметить, частичное применение с помощью функции `partial()` работает подобно декоратору. При этом у `partial` объекта нет явных атрибутов `__name__` и `__doc__` от начальной функции. Доступ к этим атрибутам возможен только через исходную функцию с помощью атрибута `func`.

С помощью функции `update_wrapper()` из модуля `functools` можно скопировать и добавить атрибуты `__name__` и `__doc__` из исходной функции в `partial` объект.

Приведенный ниже код:

```python
from functools import partial, update_wrapper

def multiply(a, b):
    '''Функция перемножает два числа и возвращает вычисленное значение.'''
    return a * b

double = partial(multiply, 2)

update_wrapper(double, multiply)   # копируем информацию из функции multiply в partial объект double

print(double.__name__)
print(double.__doc__)
```

выводит:

```no-highlight
multiply
Функция перемножает два числа и возвращает вычисленное значение.
```

## Декоратор lru_cache

В модуле `functools` уже реализован декоратор `lru_cache`, дающий возможность кэшировать результат вычисления функции, используя стратегию Least Recently Used. Это простой, но мощный метод, который позволяет использовать в коде возможности кэширования.

Приведенный ниже код:

```kotlin
from functools import lru_cache​

@lru_cache()
def fibonacci(n):
    if n <= 2:
        return 1
    else:
        return fibonacci(n - 1) + fibonacci(n - 2)
```

добавляет кэширование к функции `fibonacci()`. Декоратор `lru_cache` сохраняет результаты вызова `fibonacci()` для каждого уникального значения аргумента.

### Аргументы декоратора lru_cache

При декорировании функций с помощью декоратора `lru_cache` мы можем использовать следующие аргументы:

- `maxsize=128` — максимальный размер кэша (тип `int`)
- `typed=False` — как кэшировать при разных типах аргументов (тип `bool`)

Если для параметра `maxsize` установлено значение `None`, то кэш может расти без ограничений.

Если для `typed` задано значение `True`, то результаты вызовов функции для аргументов разных типов будут кэшироваться отдельно. Например, `f(3)` и `f(3.0)` будут рассматриваться как отдельные вызовы с разными результатами. Если для `typed` задано значение `False`, то вызовы будут рассматриваться как одинаковые.

Приведенный ниже код:

```python
from functools import lru_cache

@lru_cache(typed=False)
def concat(text, num):
    return text + ' ' + str(num)

print(concat('beegeek', 4))
print(concat('beegeek', 5.0))
print(concat('beegeek', 4.0))
```

выводит:

```no-highlight
beegeek 4
beegeek 5.0
beegeek 4
```

Как мы видим, третий вызов функции с аргументами `('beegeek', 4.0)` использует закэшированный результат первого вызова с аргументами `('beegeek', 4)`.

Приведенный ниже код:

```python
from functools import lru_cache

@lru_cache(typed=True)
def concat(text, num):
    return text + ' ' + str(num)

print(concat('beegeek', 4))
print(concat('beegeek', 5.0))
print(concat('beegeek', 4.0))
```

выводит:

```no-highlight
beegeek 4
beegeek 5.0
beegeek 4.0
```

### Дополнительные методы декоратора lru_cache

Чтобы помочь измерить эффективность кэша и настроить параметр `maxsize`, декорированная функция имеет метод `cache_info()`, который возвращает именованный кортеж, показывающий `hits`, `misses`, `maxsize` и `currsize`.

Мы можем использовать информацию, возвращаемую `cache_info()`, чтобы понять, как работает кэш, и настроить его, чтобы найти подходящий баланс между скоростью работы и объемом памяти:

- `hits` – количество значений, которые `lru_cache` вернул непосредственно из памяти, поскольку они присутствовали в кэше
- `misses` – количество значений, которые были вычислены, а не взяты из памяти
- `maxsize` – это размер кэша, который мы определили, передав его декоратору
- `currsize` – текущий размер кэша

Приведенный ниже код:

```python
from functools import lru_cache

@lru_cache(typed=False)
def concat(text, num):
    return text + ' ' + str(num)

print(concat('beegeek', 1))
print(concat('beegeek', 1.0))
print(concat('beegeek', True))
print(concat('beegeek', 4.0))
print(concat('beegeek', 5))

print(concat.cache_info())
```

выводит:

```no-highlight
beegeek 1
beegeek 1
beegeek 1
beegeek 4.0
beegeek 5
CacheInfo(hits=2, misses=3, maxsize=128, currsize=3)
```

Декоратор `lru_cache` также предоставляет метод `cache_clear()` для очистки кэша.