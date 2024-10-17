В Python версии 3.10 появилась новая конструкция под названием match/case, которая позволяет достаточно гибко анализировать переменные на соответствие шаблонов и для найденного совпадения выполнять некоторые заданные операции. Данный оператор имеет следующий синтаксис:

```python
match <переменная>:
    case <шаблон_1>:
        операторы
    ...
    case < шаблон_n>:
        операторы
    case _:
        иначе (default) 
```

Пример:

```python
cmd = 'top'

match cmd:
    case 'top':
        print('Вверх')
    case 'left':
        print('Влево')

```

Пример:

```python
cmd = 'top'
match cmd:
    case "top" | "left" | "right":
        print("вверх, влево или вправо") # 
    case _:  # wildcard
        print("другое")
```


## Проверка типа данных


```python
num = 5

match num:
    case str():
        print(f'{num} is string')
    case int():
        print(f'{num} is number')

# 5 is number
```


```python
cmd = 2.5
 
match cmd:
    case str() as command if len(command) < 10 and command[0] == 'c':
        print(f"строковая команда: {command}")
    case bool() as command:
        print(f"булева команда: {command}")
    case int() | float() as command if 0 <= command <= 9:
        print(f"команда: {command}")
    case _:  # wildcard
        print(f"другая команда")
# Вывод
# команда 2.5
```

