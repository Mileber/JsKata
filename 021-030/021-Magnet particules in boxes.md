[kata](https://www.codewars.com/kata/56c04261c3fcf33f2d000534/train/javascript)

```javascript
function doubles(maxk, maxn) {
  var sum = 0;
  for (var i=1; i<=maxk; i++) {
    var sum_n = 0;
    for (var j=1; j<=maxn; j++) {
      var n = simple(i, j);
      sum_n += n;
    }
    sum += sum_n;
  }
  
  return sum;
  
  function simple(k, n) {
    var b = k * Math.pow((n+1), (k*2));
    var result = Math.pow(b, -1);
    return result;
  }
}
```

```javascript
function doubles(maxk, maxn) {
  var s = 0;
  for (var k = 1; k <= maxk; ++k)
  for (var n = 1; n <= maxn; ++n) s += v(k, n);
  return s;
}

function v(k, n) {
  return 1/(k * Math.pow((n + 1), 2*k));
}
```

```javascript
function doubles(maxk, maxn) {
  var sum = 0;
  for(var i = 1; i <= maxk; i++)
    for(var j = 1; j <= maxn; j++)
      sum += 1 / (i * Math.pow(j + 1, 2 * i));
  return sum;
}
```