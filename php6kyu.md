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
