[kata](http://www.codewars.com/kata/memoized-fibonacci)

```javascript
var fibonacci = function(n) {
    var arr = [];
    
    return function(n) {
        if(n == 0 || n == 1){
            arr[n] = n
            return n;
        }else {
            if (arr.length > n) {
                return arr[n];
            } else {
                arr[n] = fibonacci(n-1) + fibonacci(n-2);
                return arr[n];
            }
        }
    }
}();
```

```javascript
var fibonacci = (function () {
  var cache = {};
  
  return function(n) {
    
    // Base case
    if(n==0 || n == 1)
        return n;
    
    // Recurse only if necessary
    if(cache[n-2] === undefined)
      cache[n-2] = fibonacci(n-2);
    if(cache[n-1] === undefined)
      cache[n-1] = fibonacci(n-1);
    
    return cache[n-1] + cache[n-2];
  };
})(); // Immediately invoke to create a closure for the cache variable
```

```javascript
//TODO: refactor the function into a recursive Fibonacci function that using 
//a memoized data structure avoids the deficiencies of tree recursion
//Can you make it so the memoization cache is private to this function?
var memo = function(f) {
  var cache = {};
  return function(n) {
    if(!cache[n]) cache[n] = f(n);
    return cache[n];
  }
};
var fibonacci = memo(function(n) {
    if(n==0 || n == 1)
        return n;
    return fibonacci(n-1) + fibonacci(n-2);
});
```

```javascript
var fibonacci = (function () {
  var mem = [0, 1];
  return function (n) {
    if (mem[n] === undefined)
      mem[n] = fibonacci(n - 1) + fibonacci(n - 2);
    return mem[n];
  };
})();
```