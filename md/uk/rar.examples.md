- [«Зумовлені константи](rar.constants.md)
- [Rar »](ref.rar.md)

- [PHP Manual](index.md)
- [Rar](book.rar.md)
- Приклади

# Приклади

Також дивіться приклади за посиланням [`rar://`wrapper](wrappers.rar.md).

**Приклад #1 Декомпресія на льоту**

` <?phpif (!array_key_exists("i", $_GET)||| !is_numeric($_GET["i"]))    die("Індекс не вказаний або не числовий");$index = (ET) "i"];$arch = RarArchive::open("example.rar");if ($arch === FALSE)    die("Неможливо відкрити example.rar");$entries = $arch->getEntries() ;if ($entries ====FALSE)   die("Неможливо одержати записи");if (!array_key_exists($index, $entries))    die("Нет такого індексу:$$index| index]->getName(); //Кодування UTF-8$filesize = $entries[$index]->getUnpackedSize();/* Ви можете тут перевірити константу HTTP_IF_MODIFIED_SINCE і порівняти з * $ent> Також можливо відіслати заголовок * "Last modified" */$fp = $entries[$index]->getStream();if ($fp === FALSE)    die("Неможливо відкрити і| ;$arch->close(); // Більше не потрібний. Потік є незалежнимfunction detectUserAgent() {   if (!array_key_exists('HTTP_USER_AGENT',$$SERVER))         return "Other"; $uas==$$SERVER['HTTP_USER_AGENT']; if (preg_match("@Opera/@", $uas))       return "Opera"; if (preg_match("@Firefox/@", $uas))       return "Firefox"; if (preg_match("@Chrome/@", $uas))       return "Chrome"; if (preg_match("@MSIE ([0-9.]+);@", $uas, $matches)) {        if (((float)$matches[1]) >= 7.0)             }   return "Other";}/* * Діють 3 опції: * - Для FF і Opera, з підтримкою RFC 2231, використовується этот формат. * - Для IE и Chrome, используется attwithfnrawpctenclong *   (http://greenbytes.de/tech/tc2231/#attwithfnrawpctenclong) * - Для других браузеров, перекодируется в ISO-8859-1, если возможно */$formatRFC2231 = 'Content- Disposition: attachment; filename*=UTF-8\'\'%s';$formatDef = 'Content-Disposition: attachment; filename="%s" '; $format = $formatRFC2231; break; case "IE":    case "Chrome":        $orfilename = rawurlencode($orfilename); $format = $formatDef; break; default:8|-8,8 $format==$$formatDef;}header(sprintf($format,$orfilename)); /octet-stream";header("Content-Type: $contentType");header("Content-Transfer-Encoding: binary");header("Content-Length: $filesize");if ($_SERVER['REQUEST_METHOD '] == "HEAD")   die();while(!feof($fp)) {   $s = @fread($fp, 8192); if ($s === false)         break; //тут безкорисно надсилати повідомлення про помилки   echo $s;}?> `

Цей приклад відкриває RAR-файл і надає запитаний файл поза
RAR-архів для завантаження клієнтом.

**Приклад #2 Приклад вилучення переліку файлів та директорій з
RAR-архіву**

` <?php$rar_file = rar_open('example.rar') or die("Неможливо відкрити RAR архів");$entries = rar_list($rar_file);foreach ($entries as $entry) {    . $entry->getName() . "
";   echo 'Упакований розмір: ' . $entry->getPackedSize() . "
";    echo 'Розпакований розмір: ' . $entry->getUnpackedSize() . "
";   $entry->extract('/dir/extract/to/');}rar_close($rar_file);?> `

Цей приклад відкриває RAR-файл та витягує кожен об'єкт у вказану
директорію.
