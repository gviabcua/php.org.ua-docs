Отримує кодову точку символу Unicode

-   [« mb\_list\_encodings](function.mb-list-encodings.html)
    
-   [mb\_output\_handler »](function.mb-output-handler.html)
    
-   [PHP Manual](index.html)
    
-   [Функции для работы с многобайтовыми строками](ref.mbstring.html)
    
-   Отримує кодову точку символу Unicode
    

# мбord

(PHP 7> = 7.2.0, PHP 8)

мбord — Отримує кодову точку символу Unicode

### Опис

```methodsynopsis
mb_ord(string $string, ?string $encoding = null): int|false
```

Повертає значення кодової точки Unicode для цього символу.

Функція доповнює [mb\_chr()](function.mb-chr.html)

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
var_dump(mb_ord("A", "UTF-8"));
var_dump(mb_ord("🐘", "UTF-8"));
var_dump(mb_ord("\x80", "ISO-8859-1"));
var_dump(mb_ord("\x80", "Windows-1252"));
?>
```

Результат виконання цього прикладу:

int(65)  
int(128024)  
int(128)  
int(8364)

### Дивіться також

-   [mb\_internal\_encoding()](function.mb-internal-encoding.html) - Встановлення/отримання внутрішнього кодування скрипту
-   [mb\_chr()](function.mb-chr.html) - Повертає символ за значенням кодової точки Unicode
-   [IntlChar::ord()](intlchar.ord.html) - Отримати код символ Unicode
-   [ord()](function.ord.html) - Конвертує перший байт рядка до числа від 0 до 255