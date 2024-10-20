## `random.random()` - Возвращает случайное вещественное число в диапазоне от 0 до 1

```python
import random
print(random.random()) # 0.6815...
```

## `random.uniform()` - Возвращает случайное вещественное число в заданном диапазоне 

```python
import random
print(random.uniform(1, 5)) # 2.4635...
```

## `random.randint()` - Возвращает случайное целое число в заданном диапазоне

```python
import random
print(random.randint(1, 5)) # 5
```

## `random.randrange(от, до, шаг)` - Возвращает случайное целое число в заданном диапазоне также позволяет задать шаг

```python
import random
print(random.randrange(2, 10, 2)) # 6
print(random.randrange(10)) # от 0 до 10
```

## `random.gauss(mu, sigma)` - Возвращает Гауссовскую случайную величину

```python
import random
print(random.gauss(0, 3.5)) # -4.1089...
```

## `random.choice` - Возвращает случайно выбранный элемент из последовательности

```python
import random
lst = [4, 5, 6, 1, 2, 8]
print(random.choice(lst)) # 6
```

## `random.shuffle` - Случайным образом перемешивает элементы изменяемой коллекции

```python
import random
lst = [4, 5, 6, 1, 2, 8]
random.shuffle(lst)
print(lst) # 
```

## `random.sample(lst, 3)` - Возвращает случайные элементы в заданном количестве в заданной коллекции

```python
import random
lst = [4, 5, 6, 1, 2, 8]
res = random.sample(lst, 3)
print(res) # [6, 8, 1]
```

## `random.seed(3)` - Зерно случайно последовательности, дает возможность генерировать одну и ту же последовательность 

```python
import random
random.seed(3)
lst = [random.randint(1, 10) for i in range(11)]
print(lst) 
```

## Примеры программ

**Программа которая случайно перемешивает столбцы матрицы**

```python
import sys
import random
# установка "зерна" датчика случайных чисел, чтобы получались одни и те же случайные величины
random.seed(1)

# считывание списка из входного потока
lst_in = list(map(str.strip, sys.stdin.readlines()))

def shuffle_columns(lst):
    shuffled_columns = list(zip(*lst))
    random.shuffle(shuffled_columns)
    return [list(column) for column in shuffled_columns]

# Преобразование строки в двумерный список
lst = [[int(x) for x in row.split()] for row in lst_in]

# Перемешивание столбцов
shuffled = shuffle_columns(lst)
# обратная трансформация матрицы
res = list(zip(*shuffled))
# Вывод результата
for row in res:
    print(*row)
```