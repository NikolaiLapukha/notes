При натяжке верстки на CMS нужно выносить header и footer в отдельные файлы.
**Для этого нужно:**
	1. Создать два файла: `header.php` и `footer.php`.
	2. Скопировать в `header.php` все от начала до конца тега header из файла `index.php`, а в `footer.php` все от начала тега footer до конца фала `index.php`.
	3. Подключить `header.php` и `footer.php` в `index.php`:

```php
<?php get_header(); ?>
<main>
Основное тело страницы
</main>
<?php get_footer(); ?>
```
