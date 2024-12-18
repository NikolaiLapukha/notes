Встроенный модуль `string` раньше использовался для расширения стандартных возможностей (функционала) строкового типа данных `str`. На текущий момент все функции из модуля `string` переехали в методы строкового типа данных `str`, однако в модуле `string` остались удобные константные строки, которые можно использовать при решении задач.

## Методы модуля string

### `string.ascii_letters` - Возвращает все буквы англ. алфавита в обоих регистрах

```python
import string

print(string.ascii_letters)#abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ
```

### `string.ascii_uppercase` - Возвращает все буквы англ. алфавита в верхнем регистре

```python
import string
print(string.ascii_uppercase)#ABCDEFGHIJKLMNOPQRSTUVWXYZ
```

### `string.ascii_lowercase` - Возвращает все буквы англ. алфавита в нижнем регистре

```python
import string
print(string.ascii_lowercase)#abcdefghijklmnopqrstuvwxyz
```

### `string.digits` - Возвращает числа от 0 до 9

```python
import string
print(string.digits)#0123456789
```

### `string.hexdigits` - Возвращает все шестнадцатиричные числа

```python
import string
print(string.hexdigits)#0123456789abcdefABCDEF
```
### `string.octdigits` - Возвращает все восьмеричные цифры

```python
import string
print(string.octdigits)#01234567
```

### `string.punctuation` - Возвращает все спецсимволы 

```python
import string
print(string.punctuation)#!"#$%&'()*+,-./:;<=>?@[\]^_`{|}~
```

### `string.printable` - Возвращает все буквы, числа и символы

```python
import string
print(string.printable)#0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ!"#$%&'()*+,-./:;<=>?@[\]^_`{|}~ \t\n\r\x0b\x0c
```


`