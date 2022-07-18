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
```

- Take a ten minutes walk

```javascript
function isValidWalk (walk) {
  let result = false;
  if (walk.length > 10 || walk.length < 10) {
    // pass
  } else {
    let coordinates = [5, 5];
    for (let i = 0; i < 10; i++) {
      if (walk[i] === 'n') {
        coordinates[0] = coordinates[0] + 1;
      } else if (walk[i] === 's') {
        coordinates[0] = coordinates[0] - 1;
      } else if (walk[i] === 'e') {
        coordinates[1] = coordinates[1] + 1;
      } else {
        coordinates[1] = coordinates[1] - 1;
      }
    }
    if (coordinates[0] === 5 && coordinates[1] === 5) {
      result = true;
    }
  }
  return result;
}
```
