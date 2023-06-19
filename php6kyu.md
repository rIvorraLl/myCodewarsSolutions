# PHP 6 kyu

- Matrix Addition

```php
function matrix_addition(array $a, array $b): array {
    $result = [];
    $tempArray = [];
    for ($i = 0; $i < count($a); $i++) {
        for ($j = 0; $j < count($a[$i]); $j++) {
            $sum = $a[$i][$j] + $b[$i][$j];
            $tempArray[] = $sum;
        }
        $result[] = $tempArray;
        $tempArray = [];
    }
    return $result;
}
```

- Find the missing term in an Arithmetic Progression

```php
function findMissing($list)
{
    $difference = ($list[sizeof($list) - 1] - $list[0]) / sizeof($list);
    $result = null;
    for ($i = 1; $i < sizeof($list); $i++) {
        if ($list[$i] - $difference != $list[$i-1]) {
            $result = $list[$i] - $difference;
            $i = sizeof($list);
        }
    }
    return $result;
}
```

- IP Validation

```php
function isValidIP(string $str): bool
{
    $ip_regex = "/^((25[0-5]|(2[0-4]|1\d|[1-9]|)\d)\.?\b){4}$/";
    return preg_match($ip_regex, $str);
}

```

- Find the parity outlier

```php
function find($integers)
{
    $count = null;
    $result = null;
    for ($i = 0; $i < 3; $i ++) {
        if ($integers[$i] % 2 == 0) {
            $count ++;
        }
    }
    if ($count < 2) {
        foreach ($integers as $integer) {
            if ($integer % 2 == 0) {
                $result = $integer;
                break;
            }
        }
    } else {
        foreach ($integers as $integer) {
            if ($integer % 2 != 0) {
                $result = $integer;
                break;
            }
        }
    }
    return $result;
}
```

- Does my number look big in this?

```php
<?php
function narcissistic(int $value): bool {
    $value = (string)$value;
    $provNum = null;
    $result = false;
    for ($i = 0; $i < strlen($value); $i++) {
        $provNum = $provNum + pow((int)$value[$i], strlen($value));
    }
    if ($value == $provNum) {
        $result = true;
    }
    return $result;
}
```

- Detect pangram


```php
function detect_pangram($string)
{
    $result = false;
    $letters = 'abcdefghijklmnopqrstuvwxyz';
    for ($i = 0; $i < strlen($string); $i ++) {
        for ($j = 0; $j < strlen($letters); $j ++) {
            if ($string[$i] >= 'a' && $string[$i] <= 'z' || $string[$i] >= 'A' && $string[$i] <= "Z") {
                // echo "Value string: $string[$i] Value letters: $letters[$j]\n";
                if (strtolower($string[$i]) == $letters[$j]) {
                    $char = $letters[$j];
                    $letters = substr_replace($letters, '', $j, 1);
                    $j = strlen($letters);
                }
            }
        }
    }
    if (strlen($letters) == 0) {
        $result = true;
    }
    echo $letters;
    return $result ? 'true' : 'false';
    // return $result;
}
````

- Make the Deadfish Swim

```php
function parse($data)
{
    $result = [];
    $value = 0;
    if (strlen($data) !== 0) {
        for ($i = 0; $i < strlen($data); $i ++) {
            $char = substr($data, ($i), 1);
            switch ($char) {
                case 'i':
                    $value ++;
                    break;
                case 'd':
                    $value --;
                    break;
                case 's':
                    $value = $value * $value;
                    break;
                case 'o':
                    $result[] = $value;            }
        }
    }
    return $result;
}
```

- Find the missing letter

```php
function find_missing_letter(array $array): string {
    $letters = array('a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z',
        'A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z');
    $returnLetter = '';
    for ($i = 0; $i < count($array); $i++) {
        for ($j = 0; $j < count($letters); $j++) {
            if ($array[$i] == $letters[$j] && $array[$i + 1] != $letters[$j + 1]) {
                $returnLetter = $letters[$j + 1];
                $j = count($letters);
                $i = count($array);
            }
        }
    }
    return $returnLetter;
}
```

- Replace With Alphabet Position

```php
function alphabet_position(string $s): string {
    $letters = 'abcdefghijklmnopqrstuvwxyz';
    $result = '';
    for ($i = 0; $i < strlen($s); $i++) {
        for ($j = 0; $j < strlen($letters); $j++) {
            if (strtolower($s[$i]) === $letters[$j]) {
                $result .= $j + 1 . ' ';
                $j = strlen($letters);               
            }
        }
    }
    return rtrim($result);
}
```

- Unique In Order

```php
function uniqueInOrder($iterable){
  if (empty($iterable)) {
    return array();
  }
  $len = (gettype($iterable) == 'array') ? count($iterable) : strlen($iterable);
  $resultArr = [$iterable[0]];
  for ($i = 1; $i < $len; $i++) {
    if ($iterable[$i] != $iterable[$i-1]) {
      array_push($resultArr, $iterable[$i]);
    }
  }
  return $resultArr;
}
```

- Exclamation marks series #17: Put the exclamation marks and question marks on the balance - are they balanced?

```php
function add(string $str) {
    $total = 0;
    $strArr = str_split($str);
    foreach ($strArr as $letter) {
      if ($letter === '!') {
        $total += 2;
      } else if ($letter === '?') {
        $total += 3;
      }
    }
    return $total;
}

function balance(string $l, string $r): string {
  $left = add($l);
  $right = add($r);
  $result = '';
  if ($left === $right) {
    $result = 'Balance';
  } else {
    ($left > $right) ? $result = 'Left' : $result = 'Right';
  }
  return $result;
}
```

- Convert string to camel case

```php
function toCamelCase($str) {
  $result = '';
  if (strlen($str) > 0) {
    for ($i = 0; $i < strlen($str); $i++) {
      if ($str[$i] == '-' || $str[$i] == '_') {
        $result .= strtoupper($str[$i+1]);
        $i++;
      } else {
        $result .= $str[$i];
      }
    }
  }
  return $result;
}
```

- Character with longest consecutive repetition

```php
function longestRepetition($s)
{
    $provCounter = 1;
    $counter = 0;
    $char = '';
    $len = strlen($s);
    if (strlen($s) === 0) {
        return ["", 0];
    } else {
        for ($i = 0; $i < $len; $i++) {
            for ($j = $i+1; $j < $len; $j++) {
                if ($s[$i] === $s[$j]) {
                    $provCounter++;
                } else {
                    break;
                }
            }
            if ($provCounter > $counter) {
                $counter = $provCounter;
                $char = $s[$i];
            }
            $provCounter = 1;
        }
    }
    return [$char, $counter];
}
```

- Consonant value

```php
function solve($s)
{
    $letters = ['a', 'b', 'c', 'd', 'e', 'f', 'g',
    'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q',
    'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z',
    ];
    $vowels = ['a', 'e', 'i', 'o', 'u'];
    $replaced = str_replace($vowels, ',', $s);
    $string_to_arr = explode(',', $replaced);
    $provisional_value = 0;
    $higher = 0;
    foreach($string_to_arr as $item) {
        for ($i = 0; $i < strlen($item); $i++) {
            $provisional_value += array_search($item[$i], $letters) + 1;
        }
        if ($provisional_value > $higher) {
            $higher = $provisional_value;
        }
        $provisional_value = 0;
    }
    return $higher;
}
```


