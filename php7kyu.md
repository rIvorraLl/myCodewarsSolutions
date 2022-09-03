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
