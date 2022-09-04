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
