**Чтобы на CMS создавать любое число однотипных элементов прямо из админки нужно использовать цикл для группы полей, например цикл на CFS, для этого нужно:**

1. Создать группу полей для нужной страницы и задать ему тип поля цикл:
![[Цикл.png]]

2. Создать поля для элемента цикла:
![[wordpress/Элементы цикла.png]]
![[Элементы цикла 2.png]]
3. Добавить код цикла в верстку:

```php
<?php 
	$items = CFS()->get('header_loop');
		foreach($items as $item){
			?>
			// здесь должно быть тело элемента цикла
			<?php
		}
?>
```

**Пример:**
```php
<?php 
		$items = CFS()->get('header_loop');
			foreach ($items as $item) {
				?>
					<div class="header_item">
							<?= $item['loop_img']; ?>
								<h2 class="header_item-title">
									<?= $item['loop_title']; ?>
									</h2>
								<p class="header_item-text">
									<?= $item['loop_text']; ?>
								</p>
					</div>
				<?php
		}
?>
```
