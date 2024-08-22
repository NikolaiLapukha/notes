**Для того чтобы установить свой сайт на Wordpress на сервер Ubuntu нужно**:
1. Установить `apache2 mariadb-server mariadb-client php phpmyadmin`:
```bash
sudo apt install apache2 mariadb-server mariadb-client php phpmyadmin php-mbstring php-gettext-languages
```

2. Создать директорию сайта по пути: `/var/www/название сайта`
```bash
sudo mkdir назвние_сайта
```

3. Задать права всем файлам сайта: `sudo chmod -R 755 директория_сайта`

4. Возможно нужно создать пользователя для базы данных, под которым потом нужно будет заходить в `phpmyadmin`:
```sql
GRANT ALL ON *.* TO 'admin'@'localhost' IDENTIFIED BY 'password' WITH GRANT OPTION;
```

5. Зайти в `phpmyadmin` и создать базу данных для сайта.

6. Скачать Wordpress с официального сайта:
```bash
wget https://ru.wordpress.org/latest-ru_RU.tar.gz
```

7. Извлечь файлы из архива:
```bash
tar -xvf latest-ru_RU.tar.gz
```

8. Скопировать файлы Wordpress в директорию сайта:
```bash
➜  ~ cd wordpress 
➜  wordpress cp -r * /var/www/site
```

9. Зайти в админку Wordpress и провести установку и настройку.