[kata](https://www.codewars.com/kata/vigenere-autokey-cipher-helper/train/javascript)

```javascript
function VigenèreAutokeyCipher(key, abc) {
  this.encode = function (str) {
    var arrABC = abc.split("");
    var arrStr = str.split("");
    var arrKeyList = key.split("");
    
    var arrStrNoSpace = [];
    arrStr.forEach(el=>{
      if (el != " ") {
        arrStrNoSpace.push(el);
      }    
    })
    
    if (key.length < str.length) {
      for (var i=0;i<str.length;i++){
        var index = arrABC.indexOf(arrStrNoSpace[i]);
        if (index !== -1) {
          arrKeyList.push(arrStrNoSpace[i]);
        }
      }
    }

    var arrResult = [];
    for (var j=0, k=0;j<arrStr.length;j++){
      if (arrStr[j] != " ") {
        var indexStr = arrABC.indexOf(arrStr[j]);
        var indexKey = arrABC.indexOf(arrKeyList[k]);
        
        if (indexStr == -1) {
          arrResult.push(arrStr[j]);
        } else {
          var index = indexStr+indexKey;
          
          if (index < arrABC.length) {
            arrResult.push(arrABC[index]);
            index = -1;
          } else {
            index = (index-1)%(arrABC.length-1)
            arrResult.push(arrABC[index]);
          }
          k++;
        }
      } else {
        arrResult.push(arrStr[j]);
      }
    }
    return arrResult.join("");
  };
  this.decode = function (str) {
    var arrABC = abc.split("");
    var arrStr = str.split("");
    var arrKeyList = key.split("");
    
    var arrResult = [];
    for (var j=0, k=0;j<arrStr.length;j++){
      if (arrStr[j] != " ") {
        var indexStr = arrABC.indexOf(arrStr[j]);
        var indexKey = arrABC.indexOf(arrKeyList[k]);
        if (indexStr == -1) {
          arrResult.push(arrStr[j]);
        } else {
          var index = indexStr-indexKey;
          if (index>=0) {
            arrResult.push(arrABC[index]);
            index = -1;
          } else {
            index = (index+arrABC.length)%(arrABC.length-1)
            if (index == 0) {
              arrResult.push(arrABC[arrABC.length-1]);
            } else {
              arrResult.push(arrABC[index]);
            }
          }
          arrKeyList.push(arrResult[j]);
          k++;
        }
      } else {
        arrResult.push(arrStr[j]);
      }
    }
    return arrResult.join("");
  };
}
```

```javascript
function VigenèreAutokeyCipher(origKey, abc) {
  this.encode = function(str) {
    var ignore = 0, key = origKey;
    return str.split('').map(function(v, i) {
      if(abc.indexOf(v) == -1) {ignore++; return v;}
      key = key.concat(v);
      return abc[(abc.indexOf(v) + abc.indexOf(key[i - ignore])) % abc.length];
    }).join('');
  };
  this.decode = function(str) {
    var ignore = 0, key = origKey;
    return str.split('').map(function(v, i) {
      if(abc.indexOf(v) == -1) {ignore++; return v;}
      var ind = abc.indexOf(v) - abc.indexOf(key[i - ignore]),
          out = abc[ind < 0 ? ind + abc.length : ind]
      key = key.concat(out);
      return out;
    }).join('');
  };
}
```