Модуль `os` обеспечивает портативный способ использования функциональных возможностей, зависящих от операционной системы.

Импорт модуля:

```python
import os
```

## Управление файлами

### Функция `os.system(command: str)`

Функция выполняет консольную команду 

```python
import os

os.system('ping 8.8.8.8')
```

### Функция  `os.mkdir(command: str)`

Создает директорию

```python
import os

os.mkdir('test')
```

### Функция   `os.makedirs(command: str)`

Создает вложенную структуру каталогов

```python
import os

os.makedirs('ont/two/three')
```

### Функция `os.replace()`

 Перемещает файл с сохранение старого имени или с изменённым именем

```python
import os
os.replace('/home/nikolay/python/data.pkl', '/home/nikolay/data.pkl')
```

### Функция    `os.getcwd()`

Возвращает путь текущей дериктории

### Функция `os.listdir()`

Возвращает список файлов и директорий по пути

```python
import os
path = os.getcwd()
print(os.listdir(path))
```

### Функция `os.walk(path)`

Возвращает итерируемуй объект путей и файлов

```python
import os
path = os.getcwd()
for i in os.walk(path):
    print(i)
```

### Функция `os.remove(path)`

Удаляет файл по пути

