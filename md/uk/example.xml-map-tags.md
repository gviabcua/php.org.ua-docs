---
navigation:
  - example.xml-structure.md: Приклад Структури Елементу XML
  - example.xml-external-entity.md: Приклад використання зовнішніх сутностей XML »
  - index.md: PHP Manual
  - xml.examples.md: Приклади
title: Приклад відображення тегів XML
---
## Приклад відображення тегів XML

**Приклад #1 Відображення XML у HTML**

Цей приклад відображає теги XML документа безпосередньо в тегах HTML. Елементи не знайдені у " масиві відображення " ігноруються. Звичайно, цей приклад працюватиме лише з певним типом документа XML.

```php
<?php
$file = "data.xml";
$map_array = array(
    "BOLD"     => "B",
    "EMPHASIS" => "I",
    "LITERAL"  => "TT"
);

function startElement($parser, $name, $attrs)
{
    global $map_array;
    if (isset($map_array[$name])) {
        echo "<$map_array[$name]>";
    }
}

function endElement($parser, $name)
{
    global $map_array;
    if (isset($map_array[$name])) {
        echo "</$map_array[$name]>";
    }
}

function characterData($parser, $data)
{
    echo $data;
}

$xml_parser = xml_parser_create();
// use case-folding so we are sure to find the tag in $map_array
xml_parser_set_option($xml_parser, XML_OPTION_CASE_FOLDING, true);
xml_set_element_handler($xml_parser, "startElement", "endElement");
xml_set_character_data_handler($xml_parser, "characterData");
if (!($fp = fopen($file, "r"))) {
    die("Невозможно произвести чтение XML");
}

while ($data = fread($fp, 4096)) {
    if (!xml_parse($xml_parser, $data, feof($fp))) {
        die(sprintf("XML error: %s at line %d",
                    xml_error_string(xml_get_error_code($xml_parser)),
                    xml_get_current_line_number($xml_parser)));
    }
}
xml_parser_free($xml_parser);
?>
```
