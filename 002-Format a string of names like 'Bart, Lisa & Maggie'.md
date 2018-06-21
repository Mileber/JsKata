[kata](https://www.codewars.com/kata/53368a47e38700bd8300030d/train/javascript)

```javascript
function list(names){
    var str = "";

    if (names.length == 0){
        return str;
    } else {
        for (var key in names){
            str += names[key]["name"];
            if (key == names.length - 2){
                str += ' & ';
            } else if (key == names.length - 1){
                return str;
            } else {
                str += ', ';
            }
        }
    }
}
```

```javascript
function list(names){
  return names.reduce(function(prev, current, index, array){
    if (index === 0){
      return current.name;
    }
    else if (index === array.length - 1){
      return prev + ' & ' + current.name;
    } 
    else {
      return prev + ', ' + current.name;
    }
  }, '');
}
```

```javascript
function list(names) {
  var xs = names.map(p => p.name)
  var x = xs.pop()
  return xs.length ? xs.join(", ") + " & " + x : x || ""
}
```

```javascript
function list( names ){
  return names.reduce(function(prev, curr, i, arr){
    return prev + curr.name + (i<arr.length-2?', ':i==arr.length-2?' & ':'');
  }, '');
}
```

```javascript
var list = (names) =>  names.map(x => x.name).join(', ').replace(/(.*),(.*)$/, "$1 &$2")
```