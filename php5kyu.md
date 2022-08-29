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

- The Hashtag Generator

```php
function generateHashtag($str) {
  $result = null;
  if (strlen($str) == 0 || strlen(str_replace(' ', '', $str)) == 0) {
    $result = false;
  } else if (strlen($str) > 0 ) {
    $result = '#' . ucwords($str);
    $result = str_replace(' ', '', $result);
  }
  if (strlen($result) > 140) {
    $result = false;
  }
  return $result;
}
```
