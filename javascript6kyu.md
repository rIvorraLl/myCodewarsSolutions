# 6 kyu

- Twin prime

```javascript
function isPrime(n) {
  let i = 2;
  result = true;
  while (i < n) {
      if (n % i == 0) {
          result = false;
          i = n;
      }
      i++;
  }
  return result;
}

function isTwinPrime(n){
  let result = false;
  if (n > 2) {
    let isNPrime = isPrime(n);
    let isNMinusPrime = isPrime(n-2);
    let isPlusPrime = isPrime(n+2);
    result = false;
    if (isNPrime && (isNMinusPrime || isPlusPrime)) {
      result = true;
    }    
  }
  return result;
}
