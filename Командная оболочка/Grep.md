`grep` (сокращение от global regular expression print). 
Эта утилита выполняет поиск определенного текста по файлу или файлам.

```bash
man grep

SYNOPSIS
       grep [OPTIONS] PATTERN [FILE...]
       grep [OPTIONS] [-e PATTERN]...  [-f FILE]...  [FILE...]
```

Рассмотрим этот пример подробнее:

`PATTERN` — это то, что мы хотим найти. Это может быть конкретная строчка или определенный шаблон с регулярными выражениями
`FILE` — путь до файла, в котором нужно искать.

Иногда мы не знаем, в каком файле находится то, что мы ищем. При этом мы можем знать директорию, в которой лежит этот файл.

В такой ситуации нужно сделать два изменения:

Добавить опцию -r — она указывает, что надо искать внутри директории. Обратите внимание, что поиск идет рекурсивно, то есть с включением всех поддиректорий
Указать путь до директории, а не файла
Попробуем применить утилиту grep с опцией -r:

```bash
grep -r bashrc .

./.profile:    # include .bashrc if it exists
./.profile:    if [ -f "$HOME/.bashrc" ]; then
./.profile: . "$HOME/.bashrc"
./.bash_history:du -sh .bashrc
./.bash_history:stat .bashrc
./.bash_history:stat -h .bashrc
./.bash_history:file .bashrc
./.bash_history:stat .bashrc
./.bash_history:cat .bashrc
./.bashrc:# ~/.bashrc: executed by bash(1) for non-login shells.
./.bashrc:# this, if it's already enabled in /etc/bash.bashrc and /etc/profile
./.bashrc:# sources /etc/bash.bashrc).
```

