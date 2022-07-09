# PHP 5 kyu

- Moving zeros to the end

```php
function moveZeros(array $items): array
{
    $noZerosArray = array();
    $zerosArray = array();
    foreach ($items as $item) {
        if (is_numeric($item) && $item == 0) {
            array_push($zerosArray, $item);
        } else {
            array_push($noZerosArray, $item);
        }
    }
    return array_merge($noZerosArray, $zerosArray);
}
```
