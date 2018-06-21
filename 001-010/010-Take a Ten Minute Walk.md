[kata](https://www.codewars.com/kata/take-a-ten-minute-walk/train/javascript)

```javascript
function isValidWalk(walk) {
  var N = 0, W = 0;
  if (walk.length == 10) {
      walk.forEach(function(val, i, arr){
        switch (val) {
          case 'n':
            N++;
            break;
          case 's':
            N--;
            break;
          case 'w':
            W++;
            break;
          case 'e':
            W--;
            break;
        }
      });
      if (N == 0 && W == 0) {
        return true;
      }
  }
  return false;
}
```

```javascript
function isValidWalk(walk) {
  var dx = 0
  var dy = 0
  var dt = walk.length
  
  for (var i = 0; i < walk.length; i++) {
    switch (walk[i]) {
      case 'n': dy--; break
      case 's': dy++; break
      case 'w': dx--; break
      case 'e': dx++; break
    }
  }
  
  return dt === 10 && dx === 0 && dy === 0
}
```

```javascript
function isValidWalk(walk) {
  function count(val) {
    return walk.filter(function(a){return a==val;}).length;
  }
  return walk.length==10 && count('n')==count('s') && count('w')==count('e');
}
```