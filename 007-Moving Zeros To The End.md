[kata](http://www.codewars.com/kata/moving-zeros-to-the-end)

```javascript
var moveZeros = function (arr) {
    for (var i = 0; i < arr.length; i++) {
        if (arr[i] === 0) {
            for (var j = i + 1; j < arr.length; j++) {
                if (arr[j] !== 0) {
                    arr[i] = arr[j];
                    arr[j] = 0;
                    break;
                }
            }
        }
    }
    return arr;
}
```

```javascript
var moveZeros = function (arr) {
  return arr.filter(function(x) {return x !== 0}).concat(arr.filter(function(x) {return x === 0;}));
}
```

```javascript
var moveZeros = function (arr) {
  return arr.reduceRight(function(prev, curr) {
    if (curr !== 0) {
      prev.unshift(curr);
    }
    else {
      prev.push(curr);
    }
    return prev;
  }, []);
}
```