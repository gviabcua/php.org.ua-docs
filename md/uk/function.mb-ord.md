---
navigation:
  - function.mb-list-encodings.md: « mb\_list\_encodings
  - function.mb-output-handler.md: mb\_output\_handler »
  - index.md: PHP Manual
  - ref.mbstring.md: Функції для роботи з багатобайтовими рядками
title: mb\_ord
origin_hash: ddf652f5224dc9f1fa9671347921941ca401ea50
---
# mb\_ord

(PHP 7 >= 7.2.0, PHP 8)

mb\_ord — Отримує кодову точку символу Unicode

### Опис

```methodsynopsis
mb_ord(string $string, ?string $encoding = null): int|false
```

Повертає значення кодової точки Unicode переданого символу.

Функция дополняет функцию[mb\_chr()](function.mb-chr.md)

### Список параметрів

`string`

Рядок.

`encoding`

Параметр`encoding` - Це кодування символів. Якщо він опущений або дорівнює **`null`**, для нього буде встановлено внутрішнє кодування символів.

### Значення, що повертаються

Повертає кодову точку Unicode першого символу `string`или\*\*`false`\*\*в случае возникновения ошибки.

### список змін

| Версия | Опис |
| --- | --- |
| 8.0.0 | Тепер параметр `encoding` може набувати значення **`null`** |

### Приклади

```php
<?php

var_dump(mb_ord("A", "UTF-8"));
var_dump(mb_ord("🐘", "UTF-8"));
var_dump(mb_ord("\x80", "ISO-8859-1"));
var_dump(mb_ord("\x80", "Windows-1252"));
?>
```

Результат виконання наведеного прикладу:

int(65)  
int(128024)  
int(128)  
int(8364)

### Дивіться також

-   [mb\_internal\_encoding()](function.mb-internal-encoding.md) \- Встановлює/отримує внутрішнє кодування скрипту
-   [mb\_chr()](function.mb-chr.md) \- Повертає символ за значенням кодової точки Unicode
-   [IntlChar::ord()](intlchar.ord.md) \- Отримати код символ Unicode
-   [ord()](function.ord.md) \- Конвертує перший байт рядка до числа від 0 до 255
