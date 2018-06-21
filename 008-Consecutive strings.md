[kata](http://www.codewars.com/kata/consecutive-strings)

```javascript
function longestConsec(strarr, k) {
    var n = strarr.length;
    if (n == 0 || k > n || k <= 0) {
        return "";
    } else {
        var str_max = "";
        for (var i = 0; i < strarr.length; i++) {
            var str = "";
            for (var j = 0; j < k; j++) {
                str = str + strarr[j + i];
            }
            if (str.length > str_max.length) {
                str_max = str;
            }
            if (strarr.length - i - k == 0 ){
                break;
            }
        }
        return str_max;
    }
}
```

```javascript
function longestConsec(strarr, k) {
    var longest = "";
    for(var i=0;k>0 && i<=strarr.length-k;i++){
      var tempArray = strarr.slice(i,i+k);
      var tempStr = tempArray.join("");
      if(tempStr.length > longest.length){
        longest = tempStr;
      }
    }
    return longest;
}
```

```javascript
function longestConsec(strarr, k) {
  if (k <= 0 || k > strarr.length) {
    return '';
  }
  
  return strarr.reduce((long, item, i) => {
    const currString = strarr.slice(i, i + k).join('');
    return (currString.length > long.length)
      ? currString
      : long;
  }, '');
}
```

```javascript
function longestConsec(strarr, k) {
  if( strarr.length==0 || k> strarr.length || k <1 ) return "";
  let lens = strarr.map( (_,i,arr) => arr.slice(i,i+k).join('').length ),
      i = lens.indexOf( Math.max(...lens) );
  return strarr.slice(i,i+k).join('')
}
```