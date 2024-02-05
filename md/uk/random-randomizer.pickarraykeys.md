---
navigation:
  - random-randomizer.nextint.md: '« Random\\Randomizer::nextInt'
  - random-randomizer.serialize.md: 'Random\\Randomizer::\_\_serialize »'
  - index.md: PHP Manual
  - class.random-randomizer.md: Random\\Randomizer
title: 'Random\\Randomizer::pickArrayKeys'
origin_hash: ddf652f5224dc9f1fa9671347921941ca401ea50
---
# Random\\Randomizer::pickArrayKeys

(PHP 8 >= 8.2.0)

Random\\Randomizer::pickArrayKeys — Вибирає випадкові ключі масиву

### Опис

```methodsynopsis
public Random\Randomizer::pickArrayKeys(array $array, int $num): array
```

Поступово вибирає `num` окремих ключів масиву вхідного масиву `array`

Кожен ключ вхідного масиву `array` з рівною ймовірністю буде повернено.

**Застереження**

Вибір ключів масиву залежить від внутрішньої структури вхідного масиву `array`. Ключі масиву, що повертається, можуть бути різними для двох однакових вхідних масивів і двох об'єктів [Random\\Engine](class.random-engine.md) з однаковим станом, залежно від того, як було створено вхідні масиви.

### Список параметрів

`array`

Масив, ключі масиву якого вибираються.

`num`

Кількість ключів масиву, що повертаються; має бути між і кількістю елементів у параметрі `array`

### Значення, що повертаються

Массив (array), содержащий`num` окремих ключів масиву `array`

Повертається масив (array) буде списком ([array\_is\_list()](function.array-is-list.md)). Це буде підмножина масивів (array), що повертаються функцією [array\_keys()](function.array-keys.md)

### Помилки

-   Якщо параметр `num`меньше або більше кількості елементів у параметрі`array`, буде викинуто виняток [ValueError](class.valueerror.md)
-   Будь-які [Throwable](class.throwable.md), що викидаються методом[Random\\Engine::generate()](random-engine.generate.md)базового[`Random\Randomizer::$engine`](class.random-randomizer.md#random-randomizer.props.engine)

### Приклади

**Приклад #1 Приклад використання** Random\\Randomizer::pickArrayKeys()\*\*\*\*

```php
<?php
$r = new \Random\Randomizer();

$fruits = [ 'red' => '🍎', 'green' => '🥝', 'yellow' => '🍌', 'pink' => '🍑', 'purple' => '🍇' ];

// Выборка 2 случайных ключей массива:
echo "Ключи: ", implode(', ', $r->pickArrayKeys($fruits, 2)), "\n";

// Выборка ещё 3:
echo "Ключи: ", implode(', ', $r->pickArrayKeys($fruits, 3)), "\n";
?>
```

Висновок наведеного прикладу буде схожим на:

```
Ключи: yellow, purple
Ключи: red, green, yellow
```

**Приклад #2 Вибір випадкових значень**

```php
<?php
$r = new \Random\Randomizer();

$fruits = [ 'red' => '🍎', 'green' => '🥝', 'yellow' => '🍌', 'pink' => '🍑', 'purple' => '🍇' ];

$keys = $r->pickArrayKeys($fruits, 2);
// Поиск значения для выбранных ключей.
$selection = array_map(
    static fn ($key) => $fruits[$key],
    $keys
);

echo "Значения: ", implode(', ', $selection), "\n";
?>
```

Висновок наведеного прикладу буде схожим на:

```
Значения: 🍎, 🍇
```

### Дивіться також

-   [array\_keys()](function.array-keys.md) \- Повертає все або деяке підмножина ключів масиву
