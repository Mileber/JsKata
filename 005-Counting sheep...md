[kata](http://www.codewars.com/kata/counting-sheep-dot-dot-dot)

```javascript
function countSheeps(arrayOfSheep) {
    var sum = 0;
    arrayOfSheep.forEach(function(value){
        if (value == true){
            sum++;
        }
    });
    return sum;
}
```

```javascript
function countSheeps(arrayOfSheeps) {
  return arrayOfSheeps.filter(Boolean).length;
}
```