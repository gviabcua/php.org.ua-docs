---
navigation:
  - function.mb-split.md: « mb\_split
  - function.mb-str-split.md: mb\_str\_split »
  - index.md: PHP Manual
  - ref.mbstring.md: Функції для роботи з багатобайтовими рядками
title: mb\_str\_pad
origin_hash: ddf652f5224dc9f1fa9671347921941ca401ea50
---
# mb\_str\_pad

(PHP 8 >= PHP 8.3.0)

mb\_str\_pad — Доповнює мультибайтовий рядок іншим мультибайтовим рядком до заданої довжини

### Опис

```methodsynopsis
mb_str_pad(    string $string,    int $length,    string $pad_string = " ",    int $pad_type = STR_PAD_RIGHT,    ?string $encoding = null): string
```

Ця функція повертає рядок `string`, доповнену зліва, праворуч або з обох сторін до заданої довжини, де довжина вимірюється в кодових точках Юнікод. Якщо необов'язковий аргумент `pad_string` не передано, то рядок `string`будет дополнена пробелами, иначе она будет дополнена символами параметра`pad_string` до потрібної довжини.

### Список параметрів

`string`

Вхідний рядок.

`length`

Если значение параметра`length` негативно, менше або дорівнює довжині вхідного рядка, то доповнення не відбувається і повертається вихідний рядок `string`

`pad_string`

> **Зауваження** :
> 
> Рядок `pad_string` може бути урізана, якщо необхідна кількість символів, що доповнюються, не ділиться націло на довжину рядка `pad_string`

`pad_type`

Необов'язковий аргумент `pad_type`, можливі значення: **`STR_PAD_RIGHT`** **`STR_PAD_LEFT`**, или\*\*`STR_PAD_BOTH`**По умолчанию будет использована константа**`STR_PAD_RIGHT`\*\*

`encoding`

Параметр`encoding` - Це кодування символів. Якщо він опущений або дорівнює **`null`**, для нього буде встановлено внутрішнє кодування символів.

### Значення, що повертаються

Повертає доповнений рядок.

### Приклади

**Приклад #1 Приклад використання функції** mb\_str\_pad()\*\*\*\*

```php
<?php
var_dump(mb_str_pad('▶▶', 6, '❤❓❇', STR_PAD_RIGHT)); // string(18) "▶▶❤❓❇❤"
var_dump(mb_str_pad('▶▶', 6, '❤❓❇', STR_PAD_LEFT));  // string(18) "❤❓❇❤▶▶"
var_dump(mb_str_pad('▶▶', 6, '❤❓❇', STR_PAD_BOTH));  // string(18) "❤❓▶▶❤❓"

var_dump(mb_str_pad("🎉", 3, "祝", STR_PAD_LEFT));   // string(10) "祝祝🎉"
?>
```
