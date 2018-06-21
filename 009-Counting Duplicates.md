[kata](https://www.codewars.com/kata/54bf1c2cd5b56cc47f0007a1/train/javascript)

```javascript
function duplicateCount(text){
    var count = 0;
    text = text.toLowerCase();
    for (var i = 0; i < text.length; i++) {
        var str = text.substr(i, 1);
        var other = text.substring(0, i) + text.substring(i+1, text.length);
        if (other.match(str)){
            count++;
            var reg = new RegExp(str, "g");
            text = text.replace(reg, "");
            i = 0;
        }
    }
    return count;
}
```

```javascript
function duplicateCount(text){
  return (text.toLowerCase().split('').sort().join('').match(/([^])\1+/g) || []).length;
}
```

```javascript
function duplicateCount(text){
  return text.toLowerCase().split('').filter(function(val, i, arr){
    return arr.indexOf(val) !== i && arr.lastIndexOf(val) === i;
  }).length;
}
```