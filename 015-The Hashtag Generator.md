[kata](http://www.codewars.com/kata/the-hashtag-generator/train/javascript)

```javascript
function generateHashtag (str) {
    if (str.length == 0) {
        return false;
    } else {
        var arr = str.split(" ");
        var arr2 = [];
        arr.forEach((el,i) => {
            el = el.substring(0,1).toUpperCase() + el.substring(1);
            arr2[i] = el;
        })
        var result = arr2.join("");
        result = "#" + result;
        if (result.length > 140) {
            return false;
        } else {
            return result;
        }
    }
}
```

```javascript
function generateHashtag (str) {
  return str.length > 140 || str === '' ? false :
    '#' + str.split(' ').map(capitalize).join('');
}

function capitalize(str) {
  return str.charAt(0).toUpperCase() + str.slice(1);
}
```

```javascript
function generateHashtag (str) {
   if(!str || str.length < 1) return false;
   
   var r = '#' + str.split(' ').map(function(el) {
     return el.charAt(0).toUpperCase() + el.slice(1).toLowerCase();
   }).join('');
   return r.length > 140?false:r;
}
```

```javascript
function generateHashtag (str) { 
    var s = "#" + str.replace(/\w\S*/g, function(txt){return txt.charAt(0).toUpperCase() + txt.substr(1).toLowerCase()}).split(" ").join("");
    if(str && s.length <= 140){
      return s;
    } return false; 
}
```