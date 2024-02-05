---
navigation:
  - function.mb-check-encoding.md: « mb\_check\_encoding
  - function.mb-convert-case.md: mb\_convert\_case »
  - index.md: PHP Manual
  - ref.mbstring.md: Функції для роботи з багатобайтовими рядками
title: mb\_chr
origin_hash: ddf652f5224dc9f1fa9671347921941ca401ea50
---
# mb\_chr

(PHP 7 >= 7.2.0, PHP 8)

mb\_chr — Повертає символ за значенням кодової точки Unicode

### Опис

```methodsynopsis
mb_chr(int $codepoint, ?string $encoding = null): string|false
```

Повертає рядок, що містить символ, вказаний значенням кодової точки Unicode, закодований у вказаному кодуванні.

Функция дополняет[mb\_ord()](function.mb-ord.md)

### Список параметрів

`codepoint`

Значение кодовой точки Unicode, например`128024`для*U+1F418 ELEPHANT*

`encoding`

Параметр`encoding` - Це кодування символів. Якщо він опущений або дорівнює **`null`**, для нього буде встановлено внутрішнє кодування символів.

### Значення, що повертаються

Повертає рядок, що містить запитаний символ, якщо його можна представити в заданому кодуванні, або \*\*`false`\*\*в случае возникновения ошибки.

### список змін

| Версия | Опис |
| --- | --- |
| 8.0.0 | Тепер параметр `encoding` може набувати значення **`null`** |

### Приклади

**Приклад #1 Тестування різних способів завдання**

```php
<?php

$values = [65, 63, 0x20AC, 128024];
foreach ($values as $value) {
    var_dump(mb_chr($value, 'UTF-8'));
    var_dump(mb_chr($value, 'ISO-8859-1'));
}
?>
```

Результат виконання наведеного прикладу:

```
string(1) "A"
string(1) "A"
string(1) "?"
string(1) "?"
string(3) "€"
bool(false)
string(4) "🐘"
bool(false)
```

### Дивіться також

-   [mb\_internal\_encoding()](function.mb-internal-encoding.md) \- Встановлює/отримує внутрішнє кодування скрипту
-   [mb\_ord()](function.mb-ord.md) \- Отримує кодову точку символу Unicode
-   [IntlChar::ord()](intlchar.ord.md) \- Отримати код символ Unicode
-   [chr()](function.chr.md) \- Генерує односимвольний рядок за заданим числом
