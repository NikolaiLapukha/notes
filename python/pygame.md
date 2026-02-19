# Основы

**Pygame** - библиотека для рисования и манипуляции графическими объектами.

Функционал библиотеки:
- рисование графических объектов
- отслеживание событий
- отслеживание и изменение состояний объектов
- быстрая отрисовка изменений на экране устройства пользователя
- работа со звуком

# Импорт модуля

```python
import pygame
``` 
# Инициализация pygame

Инициализация — это процесс подготовки библиотеки Pygame к работе.

```python
pygeme.init()
```

 **Пример кода** :

```python
import pygame

# Инициализация Pygame
pygame.init()

# Основная программа
print("Pygame успешно инициализирован!")

# Завершение работы
pygame.quit()
```

## Инициализация конкретных модулей

Если вы планируете использовать только определённые модули Pygame (например, только графику или только звук), можно инициализировать их отдельно. Это может быть полезно для оптимизации программы.

 **Пример кода** :

```python
import pygame

# Инициализация конкретных модулей
pygame.display.init()  # Модуль для работы с окном
pygame.mixer.init()    # Модуль для работы со звуком

# Основная программа
print("Модули display и mixer успешно инициализированы!")

# Завершение работы
pygame.quit()
```

# Создание окна pygame

Для создания окна используется метод `pygame.display.set_mode()`.

 **Пример кода** :

```python
# Инициализация Pygame
import pygame 

# Инициализация Pygame
pygame.init()

# Создание окна
screen = pygame.display.set_mode((800, 600)) # создаёт окно размером 800×600 пикселей

# Основная программа
print("Окно создано!")

# Завершение работы
pygame.quit()
```

## Настройка заголовка окна

Вы можете задать текст заголовка окна с помощью метода `pygame.display.set_caption()`.

 **Пример кода** :

```python
import pygame

# Инициализация Pygame
pygame.init()

# Создание окна
screen = pygame.display.set_mode((800, 600))
pygame.display.set_caption("Моя первая игра")

# Основная программа
print("Окно создано с заголовком 'Моя первая игра'!")

# Завершение работы
pygame.quit()
```

## Установка иконки окна 

Иконка — это маленькая картинка, которая отображается в верхнем левом углу окна или на панели задач. Для установки иконки используется метод `pygame.display.set_icon()`.

 **Пример кода** :

```python
import pygame

# Инициализация Pygame
pygame.init()

# Создание окна
screen = pygame.display.set_mode((800, 600))
pygame.display.set_caption("Моя первая игра")

# Загрузка и установка иконки
icon = pygame.image.load("icon.png")
pygame.display.set_icon(icon)

# Основная программа
print("Окно создано с иконкой!")

# Завершение работы
pygame.quit()
```

## Работа с цветом и фоном

Чтобы залить фон окна определённым цветом, используйте метод `screen.fill()`.

#### **Пример кода** :

```python
import pygame

# Инициализация Pygame
pygame.init()

# Создание окна
screen = pygame.display.set_mode((800, 600))
pygame.display.set_caption("Моя первая игра")

# Цвета
WHITE = (255, 255, 255)
RED = (255, 0, 0)

# Заливка фона
screen.fill(WHITE)

# Обновление экрана
pygame.display.flip()

# Основная программа
print("Окно создано с белым фоном!")

# Завершение работы
pygame.quit()
```

# Игровой цикл

Игровой цикл — это сердце любой игры. Он работает бесконечно, пока игра активна, и выполняет следующие задачи:

1. Обрабатывает события (например, нажатия клавиш или движение мыши).
2. Обновляет состояние игры.
3. Отрисовывает изменения на экране.

 **Пример игрового цикла** :

```python
running = True # флаг
while running: # вечный цикл
    for event in pygame.event.get(): # список игровых событий
        if event.type == pygame.QUIT: # сравнение типа события
            running = False # смена значения флага
    pygame.display.flip() # обновление экрана
pygame.quit() # завершение работы 
```

# Работа с фигурами в pygame

Фигуры — это основные элементы графики в играх:

- Квадраты могут использоваться для создания персонажей, блоков или препятствий.
- Круги подходят для объектов, таких как мячи или пули.
- Линии используются для границ, траекторий или эффектов.

 **Основные принципы работы с фигурами**

Все фигуры рисуются на поверхности (`screen`), которая создаётся при инициализации окна. Для отрисовки используется модуль `pygame.draw`.

##  Рисование квадрата

Квадрат — это частный случай прямоугольника, где ширина и высота равны.

 **Метод** :

```python
pygame.draw.rect(surface, color, (x, y, width, height))
```

**Пример кода:**

```python
import pygame

# Инициализация Pygame
pygame.init()

# Создание окна
screen = pygame.display.set_mode((640, 480))
pygame.display.set_caption("Рисование квадрата")

# Цвета
WHITE = (255, 255, 255)
RED = (255, 0, 0)

# Основной цикл
running = True
while running:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

    # Заливка фона
    screen.fill(WHITE)

    # Рисование квадрата
    pygame.draw.rect(screen, RED, (100, 100, 100, 100))

    # Обновление экрана
    pygame.display.flip()

# Завершение работы
pygame.quit()
```

## Рисование круга

Круг рисуется с помощью метода `pygame.draw.circle`.

#### **Метод** :

```python
pygame.draw.circle(surface, color, (center_x, center_y), radius)
```

#### **Параметры** :

- `surface`: поверхность, на которой рисуется фигура.
- `color`: цвет фигуры в формате RGB.
- `(center_x, center_y)`: координаты центра круга.
- `radius`: радиус круга.

**Пример кода:**

```python
# Рисование круга
pygame.draw.circle(screen, BLUE, (320, 240), 50)
```

## **Рисование линии**

Линия рисуется с помощью метода `pygame.draw.line`.

**Метод** :

```python
pygame.draw.line(surface, color, (start_x, start_y), (end_x, end_y), thickness)
```

**Пример кода:**

```python

# Рисование линии
pygame.draw.line(screen, GREEN, (50, 50), (590, 430), 5)

```

# Обработка событий

## Обработка нажатий клавиш

Pygame предоставляет два типа событий для клавиш:

- `KEYDOWN`: возникает при нажатии клавиши.
- `KEYUP`: возникает при отпускании клавиши.

#### **Пример кода** :

```python
import pygame

# Инициализация Pygame
pygame.init()

# Создание окна
screen = pygame.display.set_mode((640, 480))
pygame.display.set_caption("Обработка клавиш")

# Цвета
WHITE = (255, 255, 255)

# Основной цикл
running = True
while running:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False
        elif event.type == pygame.KEYDOWN:
            if event.key == pygame.K_LEFT:
                print("Нажата стрелка влево")
            elif event.key == pygame.K_RIGHT:
                print("Нажата стрелка вправо")
        elif event.type == pygame.KEYUP:
            if event.key == pygame.K_LEFT:
                print("Отпущена стрелка влево")
            elif event.key == pygame.K_RIGHT:
                print("Отпущена стрелка вправо")

    # Заливка фона
    screen.fill(WHITE)

    # Обновление экрана
    pygame.display.flip()

# Завершение работы
pygame.quit()
```

#### **Объяснение кода** :

1. `pygame.KEYDOWN`: проверяет нажатие клавиш.
2. `pygame.KEYUP`: проверяет отпускание клавиш.
3. `event.key`: содержит код нажатой клавиши (например, `pygame.K_LEFT` для стрелки влево).

## Обработка зажатых клавиш

Для обработки зажатых клавиш используется метод `pygame.key.get_pressed()`. 

Этот метод возвращает словарь, где каждая клавиша представлена как булева переменная (`True` — клавиша зажата, `False` — отпущена).

 **Пример кода** :

```python
import pygame

# Инициализация Pygame
pygame.init()

# Создание окна
screen = pygame.display.set_mode((640, 480))
pygame.display.set_caption("Зажатые клавиши")

# Цвета
WHITE = (255, 255, 255)
RED = (255, 0, 0)

# Координаты прямоугольника
x, y = 320, 240

# Основной цикл
running = True
while running:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

    # Получение состояния клавиш
    keys = pygame.key.get_pressed()
    if keys[pygame.K_LEFT]:
        x -= 5
    if keys[pygame.K_RIGHT]:
        x += 5
    if keys[pygame.K_UP]:
        y -= 5
    if keys[pygame.K_DOWN]:
        y += 5

    # Заливка фона
    screen.fill(WHITE)

    # Рисование прямоугольника
    pygame.draw.rect(screen, RED, (x, y, 50, 50))

    # Обновление экрана
    pygame.display.flip()

# Завершение работы
pygame.quit()
```

## Обработка событий мыши

Pygame поддерживает три основных типа событий мыши:

- `MOUSEBUTTONDOWN`: возникает при нажатии кнопки мыши.
- `MOUSEBUTTONUP`: возникает при отпускании кнопки мыши.
- `MOUSEMOTION`: возникает при движении мыши.

```python
import pygame

# Инициализация Pygame
pygame.init()

# Создание окна
screen = pygame.display.set_mode((640, 480))
pygame.display.set_caption("Обработка событий мыши")

# Цвета
WHITE = (255, 255, 255)
BLUE = (0, 0, 255)

# Основной цикл
running = True
while running:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False
        elif event.type == pygame.MOUSEBUTTONDOWN:
            print(f"Клик мыши в позиции {event.pos}")
        elif event.type == pygame.MOUSEMOTION:
            print(f"Движение мыши в позицию {event.pos}")

    # Заливка фона
    screen.fill(WHITE)

    # Обновление экрана
    pygame.display.flip()

# Завершение работы
pygame.quit()
```

# Анимация в Pygame

## Простая анимация: движение объекта

Давайте начнём с простой анимации — движения прямоугольника по экрану.

 **Метод** :

Используйте переменные для хранения координат объекта и изменяйте их в игровом цикле.

**Пример кода** :

```python
import pygame

# Инициализация Pygame
pygame.init()

# Создание окна
screen = pygame.display.set_mode((640, 480))
pygame.display.set_caption("Анимация: движение")

# Цвета
WHITE = (255, 255, 255)
RED = (255, 0, 0)

# Начальные координаты прямоугольника
x, y = 50, 50
speed_x, speed_y = 3, 2  # Скорость движения

# Основной цикл
running = True
while running:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

    # Обновление координат
    x += speed_x
    y += speed_y

    # Отскок от границ экрана
    if x <= 0 or x >= 640 - 50:  # Проверка горизонтальных границ
        speed_x = -speed_x
    if y <= 0 or y >= 480 - 50:  # Проверка вертикальных границ
        speed_y = -speed_y

    # Заливка фона
    screen.fill(WHITE)

    # Рисование прямоугольника
    pygame.draw.rect(screen, RED, (x, y, 50, 50))

    # Обновление экрана
    pygame.display.flip()

    # Контроль частоты кадров
    pygame.time.delay(10)

# Завершение работы
pygame.quit()
```

#### **Объяснение кода** :

1. `x, y`: координаты прямоугольника.
2. `speed_x, speed_y`: скорость движения по осям X и Y.
3. `pygame.time.delay(10)`: задержка между кадрами (в миллисекундах).
