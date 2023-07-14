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

- Transpose a matrix

```javascript
function transpose(matrix) {
  const result = [];
  let row = [];
  for (let i = 0; i < matrix[0].length; i++) {
    for (let j = 0; j < matrix.length; j++) {
      row.push(matrix[j][i]);
    }
    result.push(row);
    row = [];
  }
  return result;
}
```

- Persistent bugger

```javascript
function persistence (num) {
  num = '' + num;
  let counter = 0;
  let prov = num[0];
  let control = true;
  if (num.length > 1) {
    while (control) {
      for (let i = 1; i < num.length; i++) {
        prov = prov * num[i];
      }
      counter++;
      num = '' + prov;
      prov = num[0];
      if (num.length <= 1 || counter > 20) {
        control = false;
      }
    }
  }
  return counter;
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

- Break camelCase

```javascript
function solution(string) {
  let result = '';
  if (string.length != 0) {
    for (let index = 0; index < string.length; index++) {
      if (string.charAt(index) === string.charAt(index).toUpperCase()) {
        result += ' ' + string.charAt(index);
      } else {
        result += string.charAt(index);
      }
    }
  }
  return result;
}
```

- All Star Code Challenge # 15

```javascript
function rotate(str) {
  let exploded = str.split('');
  const result = [];
  let temp = '';
  for (let i = 0; i < str.length; i++) {
    exploded.push(exploded[0]);
    exploded[0] = '';
    temp = exploded.join('');
    result.push(temp);
    exploded = temp.split('');
  }
  return result;
}
```

- Find the mine!

```javascript
function mineLocation(field) {
  const result = [];
  for (let i = 0; i < field.length; i++) {
    for (let j = 0; j < field[i].length; j++) {
      if (field[i][j] === 1) {
        result[0] = i;
        result[1] = j;
      }
    }
  }
  return result;
}
```

- Duplicate Encoder

```javascript
function countLetters(word, index) {
  const wordLower = word.toLowerCase();
  let counter = 0;
  for (let i = 0; i < wordLower.length; i++) {
    if (wordLower.charAt(index) === wordLower.charAt(i)) {
      counter++;
    }
  }
  return counter;
}

function duplicateEncode(word) {
  let result = '';
  for (let i = 0; i < word.length; i++) {
    const counter = countLetters(word, i);
    counter === 1 ? result += '(' : result += ')';
  }
  return result;
}
```
