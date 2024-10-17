Il est possible d'insérer du code php dans du code HTML. Il existe deux manière de faire

# Les variables
Pour afficher du PHP dans du HTML, il est possible d'utiliser la synthaxe `<?= ... ?>`. Elle est en fait équivalente à la synthaxe `<?php echo ...?>`
```php
<?php $int = 10; ?>

...
<p>Ma variable est <?= $int ?></p>
...
```

# Afficher du code plus complexe
Si l'on souhaite vraiment implémenter du code PHP dans le HTML, il faut utiliser la synthaxe `<?php ... ?>` :

```php
<select id="source" name="source">
	<?php foreach($liste as element): ?>
		<option value = "<?php echo $element;>"><?php echo $element; ?></option>
	<?php endforeach; ?>
</select>
	
```