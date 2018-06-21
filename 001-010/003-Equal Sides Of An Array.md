[kata](http://www.codewars.com/kata/5679aa472b8f57fb8c000047/train/javascript)

```javascript
function findEvenIndex(arr){
    var lSum = 0;
    var rSum = 0;
    
    rSum = eval(arr.join("+"));
    
    for (var j = 0; j< arr.length; j++){
        rSum -= arr[j];
        if (lSum == rSum){
            return j;
        }
        lSum += arr[j];
    }
    return -1;
}
```

```javascript
function findEvenIndex(arr)
{
  for(var i=1; i<arr.length-1; i++) {
    if(arr.slice(0, i).reduce((a, b) =>  a+b) === arr.slice(i+1).reduce((a, b) =>  a+b)) {
      return i;
    }
  }
  return -1;
}
```

```javascript
function findEvenIndex(arr)
{
  var left = 0, right = arr.reduce(function(pv, cv) { return pv + cv; }, 0);
  for(var i = 0; i < arr.length; i++) {
      if(i > 0) left += arr[i-1];
      right -= arr[i];
      
      if(left == right) return i;
  }
  
  return -1;
}
```