---
navigation:
  - function.mb-list-encodings.md: « mblistencodings
  - function.mb-output-handler.md: мбoutputhandler »
  - index.md: PHP Manual
  - ref.mbstring.md: Функції для роботи з багатобайтовими рядками
title: мбord
---
# мбord

(PHP 7> = 7.2.0, PHP 8)

мбord — Отримує кодову точку символу Unicode

### Опис

```methodsynopsis
mb_ord(string $string, ?string $encoding = null): int|false
```

Повертає значення кодової точки Unicode для цього символу.

Функція доповнює [мбchr()](function.mb-chr.md)

### Список параметрів

`string`

Рядок

`encoding`

Параметр `encoding` є символьним кодуванням. Якщо він опущений або дорівнює **`null`**, замість нього буде використано значення внутрішнього кодування.

### Значення, що повертаються

Кодова точка Unicode для першого символу `string` або **`false`** у разі виникнення помилки.

### список змін

| Версия | Описание |
| --- | --- |
|  | Тепер параметр `encoding` може набувати значення **`null`** |

### Приклади

```php
<?php
var_dump(mb_ord("A", "UTF-8"));
var_dump(mb_ord("🐘", "UTF-8"));
var_dump(mb_ord("\x80", "ISO-8859-1"));
var_dump(mb_ord("\x80", "Windows-1252"));
?>
```

Результат виконання цього прикладу:

int(65)  
int(128024)  
int(128)  
int(8364)

### Дивіться також

-   [мбinternalencoding()](function.mb-internal-encoding.md) - Встановлення/отримання внутрішнього кодування скрипту
-   [мбchr()](function.mb-chr.md) - Повертає символ за значенням кодової точки Unicode
-   [IntlChar::ord()](intlchar.ord.md) - Отримати код символ Unicode
-   [ord()](function.ord.md) - Конвертує перший байт рядка до числа від 0 до 255
