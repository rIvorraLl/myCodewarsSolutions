# PHP 6 kyu

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
