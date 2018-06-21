[kata](http://www.codewars.com/kata/build-a-pile-of-cubes)

```javascript
function findNb(m) {
    let i = 1;
    while(1){
        m = m - i*i*i;
        if (m == 0) {
            return i;
        } else if (m < 0) {
            return -1;
        }
        i++;
    }
}
```

```javascript
function findNb(m) {
  var n = 0
  while (m > 0) m -= ++n**3
  return m ? -1 : n
}
```

```javascript
function findNb(m) {
  let n = 0;
  let sum = 0;
  while (sum < m) {
    n++;
    sum += Math.pow(n, 3);
  }
  return sum === m ? n : -1;
}
```

```javascript
// this is based on the formula that the sum of the first n cubes equals (n * (n + 1) / 2) ^ 2
// also, the sum of the first n cubes is always a square
function findNb(m) {
    m = Math.sqrt(m) * 2;
    if (m != parseInt(m)){
      return -1;
    }
    var result = parseInt(Math.sqrt(m));
    return (result * (result + 1) == m) ? result : -1;
}
```