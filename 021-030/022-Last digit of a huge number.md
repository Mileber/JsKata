[kata](https://www.codewars.com/kata/5518a860a73e708c0a000027/train/javascript)

## 推广前

> 给出两个数字str1和str2，计算str1^str2的最后一位数字

```javascript
var lastDigit = function(str1, str2){
    var num1 = Number(str1.slice(-1));
    var num2 = Number(str2.slice(-2));
    var num2_last = num2 % 4 || 4;
    if (str2 == 0) return 1;
    return Math.pow(num1, num2_last) % 10;
}
```

## 推广后

```javascript
function lastDigit(as) {
  var n = 0;
  if (as.length > 1) {
    for (var i = as.length - 1; i > 0; i--) {
      as[i - 1] = last2Digit(as[i - 1], as[i]);
    }
  } else if (as.length == 0) {
    return 1;
  }
  return as[0] % 10;

  function last2Digit(str1, str2) {
    var num1 = str1;
    if (str1 >= 1000) {
      num1 = str1 % 100;
    }

    var num2 = str2;
    if (num2 > 4) {
      num2 = (num2 % 4) + 4;
    } else if (num2 == 0) {
      num2 = 4;
    }

    if (str2 == 0) return 1;
    return Math.pow(num1, num2);
  }
}
```
