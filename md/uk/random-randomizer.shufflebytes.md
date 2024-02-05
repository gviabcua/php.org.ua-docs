---
navigation:
  - random-randomizer.shufflearray.md: '« Random\\Randomizer::shuffleArray'
  - random-randomizer.unserialize.md: 'Random\\Randomizer::\_\_unserialize »'
  - index.md: PHP Manual
  - class.random-randomizer.md: Random\\Randomizer
title: 'Random\\Randomizer::shuffleBytes'
origin_hash: ddf652f5224dc9f1fa9671347921941ca401ea50
---
# Random\\Randomizer::shuffleBytes

(PHP 8 >= 8.2.0)

Random\\Randomizer::shuffleBytes — Отримує байтову перестановку рядка

### Опис

```methodsynopsis
public Random\Randomizer::shuffleBytes(string $bytes): string
```

Повертає рівномірно обрану перестановку вхідних байтів `bytes`

Кожна можлива перестановка вхідного значення `bytes` з рівною ймовірністю буде повернуто.

### Список параметрів

`bytes`

Рядок (string), байти якої перемішуються.

Вхідний рядок (string) не буде змінено.

### Значення, що повертаються

Перестановка байтов параметра`bytes`

### Помилки

-   Будь-які [Throwable](class.throwable.md), що викидаються методом[Random\\Engine::generate()](random-engine.generate.md)базового[`Random\Randomizer::$engine`](class.random-randomizer.md#random-randomizer.props.engine)

### Приклади

**Приклад #1 Приклад використання** Random\\Randomizer::shuffleBytes()\*\*\*\*

```php
<?php
$r = new \Random\Randomizer();

// Перемешивание байтов в строке:
echo "«", $r->shuffleBytes("PHP is great!"), "»\n";

?>
```

Висновок наведеного прикладу буде схожим на:

```
« ga rHs!PPiet»
```

**Приклад #2 Byte-wise shuffling breaks Unicode characters**

```php
<?php
$r = new \Random\Randomizer();

$unicode = "🍎, 🥝, 🍌, 🍑, 🍇";
$shuffled = $r->shuffleBytes( $unicode );

// Побайтовое перемешивание символов, отличных от ASCII, разрушает их,
// в результате чего на выходе появляются недопустимые последовательности
// (обозначаемые символом замены Unicode) или даже совершенно другие символы.
echo "Исходные данные: ", $unicode, "\n";
echo "Перемешанные: «", $shuffled, "»\n";
echo "Перемешанные байты: ", bin2hex($shuffled), "\n";
?>
```

Висновок наведеного прикладу буде схожим на:

```
Исходные данные: 🍎, 🥝, 🍌, 🍑, 🍇
Перемешанные: «� ��,�����🍟,� �� �, �,��»
Перемешанные байты: 87208e912c8d9fa5f0f0f09f8d9f2cf09f208c9d20f02c209f2c8d8d
```
