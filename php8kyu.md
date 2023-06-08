- Pillars

```
function pillars($numberOfPillars, $dist, $width)
{
  if ($numberOfPillars > 1)
  {
    return ($numberOfPillars - 1) * $dist * 100  + $width * ($numberOfPillars - 2);
  } 
  return 0;
}
