[kata](http://www.codewars.com/kata/5547cc7dcad755e480000004/train/javascript)

```javascript
function removeNb (n) {
    var sum = (n+1)*n/2;

    var arr = [];
    for (var i=1; i<=n; i++) {
        var sum2 = sum - i;
        var b = sum2/(i+1);
        if (b>0 && b<=n && b%1==0){
            arr.push([i,b]);
        }
    }
    return arr;
}
```

```javascript
function removeNb (n) {
  // from the instruction:
  // a * b = S(n) - a - b
  
  // and the sum of all first n natural numbers is
  // S(n) = n * (n + 1) / 2
  
  // so we can refrase the first formula like this:
  // a * b = n * (n + 1) / 2 - a - b
  // a * b + b = n * (n + 1) / 2 - a
  // b * (a + 1) = n * (n + 1) / 2 - a
  // b = (n * (n + 1) / 2 - a) / (a + 1)
  
  // but a and b are natural and up to n
  
  var results = [];
  for (var a = 1; a <= n; a++) {
    var b = (n * (n + 1) / 2 - a) / (a + 1);
    if (b % 1 === 0 && b <= n) results.push([a, b]);
  }
  return results;
}
```