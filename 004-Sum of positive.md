[kata](http://www.codewars.com/kata/sum-of-positive)

```javascript
function positiveSum(arr) {
    var sum = 0;
    for (var i=0; i<arr.length; i++ ){
        if (arr[i] > 0){
            sum += arr[i];
        }
    }
    return sum;
}
```

```javascript
function positiveSum(arr) {
   return arr.reduce((a,b)=> a + (b > 0 ? b : 0),0);
}
```