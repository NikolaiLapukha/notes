## Основы
**Pygame** - библиотека для рисования и манипуляции графическими объектами.

Функционал библиотеки:
- рисование графических объектов
- отслеживание событий
- отслеживание и изменение состояний объектов
- быстрая отрисовка изменений на экране устройства пользователя
- работа со звуком

## Импорт модуля

```python
import pygame
``` 
## Основной каркас приложения

После импорта модуля нужно добавить функцию `init()` для импорта основного функционала

```python
import pygame
pygame.init()
```

Далее нужно сформировать окно:

```python
pygame.display.set_mode((600, 400))
```

Также можно задать заголовок окна:

```python
pg.display.set_caption('Pravachki (beta version)')
```

Затем нужно добавить главный цикл обработки событий:

```python
FPS = 60 # количество кадров в секунду
clock = pg.time.Clock() # объект класса счетчика для обработка кадров
while True: # вечный цикл
    for event in pg.event.get(): # цикл по очереди событий
        if event.type == pg.QUIT: # если текущий объект события равен quit
            exit() # выйти из  приложений
    clock.tick(FPS) # Обработка кадров
```

## Рисование графических примитивов

Метод для рисования графических примитивов ` pygame.draw` 

```python
pg.draw.rect(screen, (255, 255, 255), (10, 10, 50, 100)) # рисование прямоугольника
```

![[Pasted image 20241008154512.png]]

поверхность:

```python
screen = pg.display.set_mode((600, 400), pg.RESIZABLE)
# pg.display.flip() # сделать слой рисования видимым
pg.display.update() # то же самое что и flip только более гибкий, может отображать отдельные объекты, а не весь слой
```

**Рисование линии**:

```python
pg.draw.line(screen, (255, 255, 255), (200, 40), (350, 70))
```

Рисование полигона:

```python
pg.draw.polygon(screen, WHITE, [[150, 210], [180, 250], [90, 290], [30, 230]])
```

Рисование круга:

```python
pg.draw.circle(screen, BLUE, (300, 250), 40)
```

Рисование эллипса:

```python
pg.draw.ellipse(screen, BLUE, (300, 300, 100, 50), 1)
```


## Обработка событий от клавиатуры

За обработку событий отвечает метод `pygame.event`

`pygame.KEYDOWN` - метод обработки нажатия клавиш

`K_LEFT` - метод нажатия стрелки влево

`K_RIGHT` - метод нажатия стрелки вправо

`K_UP` - метод нажатия стрелки вверх

`K_DOWN` - метод нажатия стрелки вверх

`K_a, K_d, K_w, K_s` - методы обработки нажатий на клавиши a, d, w, s.

Пример обработки нажатий стрелок и клавиш a,w,s,d:

```python
while True:
    for event in pg.event.get():
        if event.type == pg.QUIT:
            exit()

    keys = pg.key.get_pressed()

    if keys[pg.K_RIGHT] or keys[pg.K_d]:
        x += speed
    elif keys[pg.K_LEFT] or keys[pg.K_a]:
        x -= speed
    elif keys[pg.K_UP] or keys[pg.K_w]:
        y -= speed
    elif keys[pg.K_DOWN] or keys[pg.K_s]:
        y += speed
```

## Обработка событий от мыши

`pygame.MOUSEBUTTONDOWN` - метод обработки нажатия кнопок мыши

`pygame.MOUSEMOTION` - метод обработки позиций мыши

`pygame.MOUSEBUTTONUP` - метод обработки отпускания кнопки мыши

Пример программы рисования квадрата:

```python
    pressed = pg.mouse.get_pressed()
    if pressed[0]:
        pos = pg.mouse.get_pos()

        if sp is None:
            sp = pos

        width = pos[0] - sp[0]
        height = pos[1] - sp[1]
        
        screen.fill(WHITE)
        pg.draw.rect(screen, BLUE, pg.Rect(sp[0], sp[1], width, height))
        pg.display.update()
```

## Создание поверхностей и их 

Создание поверхности:

```python
surf = pygame.Surface((200, 200))
```
## Рисование текста

Метод чтобы получить текст из локальной файловой системы:

```python
 pygame.font.Font
```

Пример отрисовки текста:

```python
ft = pg.font.Font('YandexSDLight.ttf', 24)
sc_text = ft.render('Hello world', 1, RED)
pos = sc_text.get_rect(center = (WIDTH / 2, HEIGHT / 2))
screen.fill(WHITE)
screen.blit(sc_text, pos)
pg.display.update()
```

## Работа с изображениями
### Создание с отрисовка

Проверка поддерживает ли устройство другие форматы, кроме встроенного:

```python
pygame.image.get_extended()
```

Создание объекта изображения:

```python
car = pg.image.load('images/car.bmp')
```

Определение место положения и отрисовка на экране:

```python
car_rect = car.get_rect(center = (WIDHT / 2, HEIGHT / 2))
screen.blit(car, car_rect)
pg.display.update()
```

Сделать лишний цвет прозрачным:

```python
car.set_colorkey((255, 255, 255))
```

Преобразование картинки в нужный формат пикселей:

```python
car = pg.image.load('images/car.bmp').convert()
bg = pg.image.load('images/sand.jpg').convert()
finish = pg.image.load('images/finish.png').convert_alpha()
```

### Трансформация 

Пример уменьшения масштаба изображения:

```python
bg = pg.transform.scale(bg, (bg.get_width() / 2, bg.get_height() / 2))
```

```python
car_down = pg.transform.flip(car, 0, 1) # переворачивает изображение по оси у
car_left = pg.transform.rotate(car, 90) # поворачивает изображение на 90 градусов влево
car_right = pg.transform.rotate(car, -90) # поворачивает изображение на 90 градусов вправо
```
## Спрайты

Создание спрайта:

```python
class MySprite(pygame.sprite.Sprite):
    def __init__(self, image):
    super().__init__()
    self.image = image
    self.rect = self.image.get_rect()
```
## Контроль столкновений

Методы класса `pygame.Rect` отвечают за контроль столкновений:
- `pygame.Rect.collidepoint(x, y)` - проверка попадания точки в прямоугольник
- `pygame.Rect.colliderect(Rect)` - проверка пересечения двух прямоугольник
- `pygame.Rect.colliderect(Rect)` - проверка пересечения хотя бы одного прямоугольника из списка list
- `pygame.Rect.collidelistall(list)` - проверка пересечения всех прямоугольников из списка list 

