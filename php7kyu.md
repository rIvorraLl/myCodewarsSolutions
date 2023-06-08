# PHP 7 kyu

- Largest 5 digit number in a series

```php
function solution(string $s) : int
{
    $provNum = null;
    $result = null;
    for ($i = 0; $i < strlen($s) - 4; $i ++) {
        $provNum = $s[$i] . $s[$i + 1] . $s[$i + 2] . $s[$i + 3] . $s[$i + 4];
        if ($provNum > $result) {
            $result = $provNum;
        }
    }
    return (int)$result;
}
```

- Geometric Progression Sequence

```php
function geometric_sequence_elements(int $a, int $r, int $n): string {
  $incremented = $a;
  $result = $a . ', ';
  for ($i = 1; $i < $n; $i++) {
    $incremented = $incremented * $r;
    $i < $n - 1 ? $result = $result . $incremented . ', ' : $result = $result . $incremented;
  }
  return $result;
}
```

- Exes and Ohs

```php
function XO($s) {
    $x = 0;
    $o = 0;
    $s = strtolower($s);
    for ($i = 0; $i < strlen($s); $i++) {
        if (substr($s, $i, 1) == 'o') {
            $o++;
        } else if (substr($s, $i, 1) == 'x') {
            $x++;
        }
    }
    return $x == $o;
}
```

- Return the closest multiple of 10

```php
function closest_multiple_10($n) {
  $result;
  $n % 10 < 5
    ? $result = $n - ($n % 10)
    : $result = $n + (10 - $n % 10);
  return $result;
}
```


- Simple remove duplicates

```php
function solve($arr)
{
    $sorted = [];
    for (($i = count($arr) - 1); $i > -1; $i--) {
        if (!in_array($arr[$i], $sorted)) {
            $sorted[$i] = $arr[$i];
        }
    }
    $result = array_reverse($sorted);
    return $result;
}
```

- Bubblesort Once

```php
function bubblesort_once($a) {
  $b = $a;
  for ($i = 0; $i < count($b) - 1; $i++) {
    if ($b[$i] > $b[$i + 1]) {
      $prov = $b[$i];
      $b[$i] = $b[$i + 1];
      $b[$i + 1] = $prov;
    }
  }
  return $b;
}
```


