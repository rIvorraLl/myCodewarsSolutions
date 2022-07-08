# 6 kyu

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
