- Human readable duration format

```php
 function format_duration($seconds) {
    $result = [];
    if ($seconds == 0) {
        $result = 'now';
    } else {

        $yrs = (($seconds / 31536000) | 0);
        $yrs > 1 ? $result[0] = $yrs . ' years' : $result[0] = $yrs . ' year';
        $days = ((($seconds % 31536000) / 86400) | 0);
        $days > 1 ? $result[1] = $days . ' days' : $result[1] = $days . ' day';
        $hrs = (((($seconds % 31536000) % 86400) / 3600) | 0);
        $hrs > 1 ? $result[2] = $hrs . ' hours' : $result[2] = $hrs . ' hour';
        $min = (((((($seconds % 31536000) % 86400) % 3600) / 60)) | 0);
        $min > 1 ? $result[3] = $min . ' minutes' : $result[3] = $min . ' minute';
        $sec = ((((($seconds % 31536000) % 86400) % 3600) % 60) | 0);
        $sec > 1 ? $result[4] = $sec . ' seconds' : $result[4] = $sec . ' second';

        for ($i = 0; $i < count($result); $i++) {
            if (substr($result[$i], 0, 1) == '0') {
                $result[$i] = '';
            }
        }
        
        $final = [];
        foreach ($result as $value) {
            if (!(empty($value))) {
                array_push($final, $value);
            }
        }
        if (count($final) > 1) {
            for ($i = 0; $i < count($final) - 2; $i++) {
                if (!empty($final[$i])) {
                    $final[$i] .= ', ';
                }
            }
            $final[count($final) - 1] = ' and ' . $final[count($final) - 1];
        }
    }
    if (!(empty($final))) {
        return implode($final);
    }
}
```
