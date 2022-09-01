---
navigation:
  - rar.constants.md: « Обумовлені константи
  - ref.rar.md: Rar »
  - index.md: PHP Manual
  - book.rar.md: Rar
title: Приклади
---
# Приклади

Також дивіться приклади за посиланням [`rar://`wrapper](wrappers.rar.md)

**Приклад #1 Декомпресія на льоту**

```php
<?php

if (!array_key_exists("i", $_GET) || !is_numeric($_GET["i"]))
    die("Индекс не указан или не числовой");
$index = (int) $_GET["i"];

$arch = RarArchive::open("example.rar");
if ($arch === FALSE)
    die("Невозможно открыть example.rar");

$entries = $arch->getEntries();
if ($entries === FALSE)
    die("Невозможно получить записи");

if (!array_key_exists($index, $entries))
    die("Нет такого индекса: $index");

$orfilename = $entries[$index]->getName(); //Кодировка UTF-8

$filesize = $entries[$index]->getUnpackedSize();

/* Вы можете здесь проверить константу HTTP_IF_MODIFIED_SINCE и сравнить с
 * $entries[$index]->getFileTime(). Также возможно отослать заголовок
 * "Last modified" */

$fp = $entries[$index]->getStream();
if ($fp === FALSE)
    die("Невозможно открыть файл с индексом $index внутри архива.");

$arch->close(); // Больше не нужен. Поток является независимым

function detectUserAgent() {
    if (!array_key_exists('HTTP_USER_AGENT', $_SERVER))
        return "Other";

    $uas = $_SERVER['HTTP_USER_AGENT'];
    if (preg_match("@Opera/@", $uas))
        return "Opera";
    if (preg_match("@Firefox/@", $uas))
        return "Firefox";
    if (preg_match("@Chrome/@", $uas))
        return "Chrome";
    if (preg_match("@MSIE ([0-9.]+);@", $uas, $matches)) {
        if (((float)$matches[1]) >= 7.0)
            return "IE";
    }

    return "Other";
}

/*
 * Действуют 3 опции:
 * - Для FF и Opera, с поддержкой RFC 2231, используется этот формат.
 * - Для IE и Chrome, используется attwithfnrawpctenclong
 *   (http://greenbytes.de/tech/tc2231/#attwithfnrawpctenclong)
 * - Для других браузеров, перекодируется в ISO-8859-1, если возможно
 */
$formatRFC2231 = 'Content-Disposition: attachment; filename*=UTF-8\'\'%s';
$formatDef = 'Content-Disposition: attachment; filename="%s"';

switch (detectUserAgent()) {
    case "Opera":
    case "Firefox":
        $orfilename = rawurlencode($orfilename);
        $format = $formatRFC2231;
        break;

    case "IE":
    case "Chrome":
        $orfilename = rawurlencode($orfilename);
        $format = $formatDef;
        break;
    default:
        if (function_exists('iconv'))
            $orfilename =
                @iconv("UTF-8", "ISO-8859-1//TRANSLIT", $orfilename);
        $format = $formatDef;
}

header(sprintf($format, $orfilename));
//Невозможна дальнейшая отсылка сообщений об ошибках (заголовки уже отправлены)

//Замена на реальный content type, возможно определённый по расширению файла
$contentType = "application/octet-stream";
header("Content-Type: $contentType");

header("Content-Transfer-Encoding: binary");

header("Content-Length: $filesize");

if ($_SERVER['REQUEST_METHOD'] == "HEAD")
    die();

while (!feof($fp)) {
    $s = @fread($fp, 8192);
    if ($s === false)
        break; //тут бесполезно отправлять сообщения об ошибках

    echo $s;
}
?>
```

Цей приклад відкриває файл RAR і надає запитаний файл поза RAR-архівом для завантаження клієнтом.

**Приклад #2 Приклад вилучення переліку файлів та директорій з RAR-архіву**

```php
<?php

$rar_file = rar_open('example.rar') or die("Невозможно открыть RAR архив");

$entries = rar_list($rar_file);

foreach ($entries as $entry) {
    echo 'Имя файла: ' . $entry->getName() . "\n";
    echo 'Упакованный размер: ' . $entry->getPackedSize() . "\n";
    echo 'Распакованный размер: ' . $entry->getUnpackedSize() . "\n";

    $entry->extract('/dir/extract/to/');
}

rar_close($rar_file);

?>
```

Цей приклад відкриває RAR-файл та витягує кожен об'єкт у вказану директорію.
