## Битовая операция Не `~`

```python
a = 10
bin(a)
print(~a) # -11
```

## Битовая операция И `&`

```python
flag = 5
mask = 4
print(flag & mask) # 4
```

## Битовая операция Или `|`

```python
flag = 8
mask = 5
print(flag | mask) # 13
```

## Битовая операция Исключающее Или (XOR) `^`

```python
flag = 4
mask = 5
print(flag ^ mask) # 1
```

## Смещение бита вправо `>>`

```python
x = 160
print(bin(x)) # 0b10100000
x = x >> 1
print(bin(x)) # 0b1010000
print(x) # 80
```

## Смещение бита влево `<<`

```python
x = 200
print(bin(x)) # 0b11001000
x = x << 1
print(bin(x)) # 0b110010000
print(x) 400
```

