В работе с командной строкой мы часто сталкиваемся с ситуациями, в которых необходимо повышать привилегии и выполнять команды от имени суперпользователя `root`.

В этом уроке обсудим, как стать другим пользователем. Для этого зайдите в систему и воспользуйтесь утилитой `su` (сокращение от _substitute user_ или _switch user_). Когда-то такой способ был основным, но сейчас он устарел и не рекомендуется к использованию.

Основной способ повышать привилегии в современных системах — утилита `sudo` (_substitute user and do_ — дословно «подменить пользователя и выполнить»).

Использовать `sudo` очень просто, достаточно написать эту команду слева от любой другой и выполнить. По умолчанию она пытается повысить привилегии до суперпользователя:

```bash
# Нет прав на выполнение
touch /etc/myfile

touch: cannot touch '/etc/myfile': Permission denied

# С `sudo` все работает
sudo touch /etc/myfile

# Видно, что владелец файла — это суперпользователь `root`
stat /etc/myfile

  File: '/etc/myfile'
  Size: 0           Blocks: 0          IO Block: 4096   regular empty file
Device: ca01h/51713d    Inode: 2761        Links: 1
Access: (0644/-rw-r--r--)  Uid: (    0/    root)   Gid: (    0/    root)

# Нет прав на удаление
rm /etc/myfile

rm: remove write-protected regular empty file '/etc/myfile'? y
rm: cannot remove '/etc/myfile': Permission denied

# Опять помогла утилита `sudo`
sudo rm /etc/myfile
```

Иногда нужно выполнить команду из-под пользователя, отличного от `root`. Тогда придется добавить флаг `-u`:

```bash
sudo -u nobody mkdir /tmp/test
# Директория создана от имени пользователя nobody
stat /tmp/test

  File: '/tmp/test'
  Size: 4096        Blocks: 8          IO Block: 4096   directory
Device: ca01h/51713d    Inode: 4577        Links: 2
Access: (0755/drwxr-xr-x)  Uid: (65534/  nobody)   Gid: (65534/ nogroup)
```

