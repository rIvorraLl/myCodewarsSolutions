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

- Where my anagrams at?

```php
function anagrams(string $word, array $words): array {
    $arr_word = str_split($word);
    sort($arr_word);
    implode($arr_word);
    $words_copy = $words;
    $result = [];
    foreach ($words_copy as $word) {
        $split_str = str_split($word);
        sort($split_str);
        implode($split_str);
        if ($arr_word == $split_str) {
            $result[] = $word;
        }
    }
    return $result;
}
```

- Human Readable Time

```php
function human_readable($seconds) {
    $result = '';
    if ($seconds > 0) {
        $hours = (integer)($seconds / 3600);
        $minutesLeft = (integer)($seconds % 3600);
        $minutes = (integer)($minutesLeft / 60);
        $secondsLeft = (integer)($seconds % 60);
        if ($hours < 10) {
            $result .= '0' . $hours . ':';
        } else {
            $result .= $hours . ':';
        }
        if ($minutes < 10) {
            $result .= '0' . $minutes . ':';
        } else {
            $result .= $minutes . ':';
        }
        if ($secondsLeft < 10) {
            $result .= '0' . $secondsLeft;
        } else {
            $result .= $secondsLeft;
        }
    } else {
        $result = '00:00:00';
    }
    return $result;
}
```
