## Пустое значение

Во многих языках программирования (Java, C++, C#, JavaScript и т.д.) существует ключевое слово `null`, которое можно присвоить переменным. Концепция ключевого слова `null` заключается в том, что оно дает переменной нейтральное или "нулевое" поведение.

В языке Python, слово `null` заменено на `None`, поскольку слово `null` звучит не очень дружелюбно, а `None` относится именно к требуемой функциональности – это ничего и не имеет поведения.

## Литерал ==None==

Литерал `None` в Python позволяет представить `null` переменную, то есть переменную, которая не содержит какого-либо значения. Другими словами, `None` – это специальная константа, означающая пустоту. Если более точно, то `None` – это объект специального типа данных `NoneType`.

Следующий программный код:

```python
var = None
print(type(var))
```

выведет:

```python
<class 'NoneType'>
```

Мы можем присвоить значение `None` любой переменной, однако мы не можем самостоятельно создать другой `NoneType` объект.


## Проверка на None
Для того чтобы проверить значение переменной на None, мы используем либо оператор is, либо оператор проверки на равенство == .

Следующий программный код:

```python
var = None
if var is None:  # используем оператор is
  print('None')
else:
  print('Not None')
```

выведет:

```python
None
```

Следующий программный код:

```python
var = None
if var == None:  # используем оператор ==
  print('None')
else:
  print('Not None')
```

выведет:

```python
None
```


## Сравнение None с другими типами данных

Сравнение `None` с *любым объектом, отличным от None*, дает значение ==False==.
Сравнивать `None` с *другими типами данных* можно только на ==равенство==.

Следующий программный код:

```python
print(None == None)
```

выведет:

```python
True
```

Следующий программный код:
```python
print(None == 17)
print(None == 3.14)
print(None == True)
print(None == [1, 2, 3])
print(None == 'Beegeek')
```

выведет:

```python
False
False
False
False
False
```