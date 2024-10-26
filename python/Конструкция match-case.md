## Основное

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

## Обработка списков и кортежей

```python
cmd = ("Балакирев С.М.", "Python", 2000.78, 2022)

match cmd:
    case author, title, price, *_:
        print(f"Книга: {author}, {title}, {price}")
    case _:  # wildcard
        print("непонятный формат данных")
# Выведет только три первых элемента
```

```python
t = (int, str, str, float, int)
book = [t[i](x) if t[i] != str else x.strip() for i, x in enumerate(input().split(","))]
match book:
    case (_, author, title) if len(author) >= 6 and len(title) >= 10:
        print('Yes')
    case (_, author, title, price) if len(author) >= 6 and price > 0:
        print('Yes')
    case (_, author, title, year) if year >= 2020:
        print('Yes')
    case (_, author, title, price, year) if price > 0 and year >= 2020:
        print('Yes')
    case _:
        print('No'
```

## Обработка словарей и множеств:

```python
request = {'url': 'https://proproprogs.ru/', 'method': 'GET', 'timeout': 1000}
match request:
    case {'url': url, 'method': method}:
        print(f"Запрос: url: {url}, method: {method}")
    case _:  # wildcard
        print("неверный запрос")
```

```python
json_data = {'id': 2, 'access': True, 'info': ['01.01.2023', {'login': '123', 'email': 'email@m.ru'}, True, 1000]}

match json_data:
    case {'access': access, 'info': [_, {'email': email}, _, _]}:
        print(f"JSON: access: {access}, email: {email}")
    case _:  # wildcard
        print("неверный запрос")
        
```

```python
primary_keys = {1, 2, 3}

match primary_keys:
    case set() as keys if len(keys) == 3:
        print(f"Primary Keys: {keys}")
    case _:  # wildcard
        print("неверный запрос")
```


```python
def book_to_tuple(data: dict | tuple | list) -> tuple | None:
    match data:
        case author, title, year:
            price = None
        case author, title, year, price, *_:
            pass
        case {'author': author, 'title': title, 'year': year, 'price': price}:
            pass
        case {'author': author, 'title': title, 'year': year}:
            price = None
        case _:  # wildcard
            return None
 
    return author, title, year, price
```

```python
class Consts:
    CMD_3 = 3
    CMD_5 = 5
 
 
cmd = 3
 
match cmd:
    case Consts.CMD_3:
        print("3")
    case Consts.CMD_5:
        print("5")
```

