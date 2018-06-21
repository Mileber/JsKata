[kata](https://www.codewars.com/kata/vigenere-cipher-helper/train/javascript)

```javascript
function VigenèreCipher(key, abc) {
  
  this.encode = function (str) {
    var arrABC = abc.split("");
    var arrStr = str.split("");
    var arrKeyList = key.split("");
    if (key.length < str.length) {
      var p = str.length - key.length;
      for (var i=0;i<p;i++){
        arrKeyList.push(arrKeyList[i]);
      }
    }
    var arrResult = [];
    for (var j=0;j<arrStr.length;j++){
      var indexStr = arrABC.indexOf(arrStr[j]);
      var indexKey = arrABC.indexOf(arrKeyList[j]);
      
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
      }
    }
    return arrResult.join("");
  };
  this.decode = function (str) {
    var arrABC = abc.split("");
    var arrStr = str.split("");
    var arrKeyList = key.split("");
    if (key.length < str.length) {
      var q = str.length-key.length;
      for (var i=0;i<q;i++){
        arrKeyList.push(arrKeyList[i]);
      }
    }
    var arrResult = [];
    for (var j=0;j<arrStr.length;j++){
      var indexStr = arrABC.indexOf(arrStr[j]);
      var indexKey = arrABC.indexOf(arrKeyList[j]);
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
      }
    }
    return arrResult.join("");
  };
}
```

```javascript
function VigenèreCipher(key, alphabet) {
  function encode(direction, inStr) {
    var inChar, inIdx, outIdx, outChar, keyChar, offset;
    
    var outStr = '';
    
    // Process each character of the input string sequentially
    for (var pos = 0; pos < inStr.length; ++pos) {
      
      // Look up input character in the alphabet
      inChar = inStr.charAt(pos);
      inIdx = alphabet.indexOf(inChar);
      
      // If character isn't in alphabet, just copy it to output
      if (inIdx < 0)
        outChar = inChar;
      else {
        // Get the key character for the current position
        // and determine the shift distance
        keyChar = key.charAt(pos % key.length);
        offset = alphabet.indexOf(keyChar);
        
        // Shift the character forwards or backwards in
        // the alphabet, wrapping around if necessary
        outIdx = inIdx + direction * offset;
        if (outIdx >= alphabet.length)
          outIdx = outIdx - alphabet.length;
        else if (outIdx < 0)
          outIdx = outIdx + alphabet.length;
        
        outChar = alphabet.charAt(outIdx);
      }
      
      outStr += outChar;
    }
    
    return outStr;
  }

  // Encode by shifting characters forward in the alphabet
  this.encode = function(string) {
    return encode(1, string);
  };
  
  // Decode by shifting characters backwards in the alphabet
  this.decode = function(string) {
    return encode(-1, string);
  };
}
```

```javascript
function VigenèreCipher(key, abc) {
  var self = this;
  var size = abc.length;
    
  this.transform = function (str, getIndex) {
    return str.split('').map(function(ch, index) {
      return abc.indexOf(ch) >= 0 ? abc[getIndex(ch, index)] : ch;
    }).join('');
  }

  this.enocodeIndex = function(ch, index) {
    return (abc.indexOf(ch) + abc.indexOf(key.charAt(index % key.length)) + size) % size
  }

  this.decodeIndex = function(ch, index) {
    return (abc.indexOf(ch) - abc.indexOf(key.charAt(index % key.length)) + size) % size
  }

  this.encode = function (str) {
    return this.transform(str, this.enocodeIndex)
  };
  this.decode = function (str) {
    return this.transform(str, this.decodeIndex)
  };
}
```

```javascript
function VigenèreCipher(key, abc) {
  
  this.compute = function(str, dir) {
    var i = 0;
    var result = '';
    var kl = key.length;
    var al = abc.length;
    
    while(str[i]) {
      result += -1 === abc.indexOf(str[i]) ? str[i] : (abc[ (abc.indexOf(str[i]) + dir * abc.indexOf(key[i%kl]) + al) % al ]);
      i++;
    }
            
    return result;
    
  },

  this.encode = function (str) {
    return this.compute(str, 1);
  };
  this.decode = function (str) {
    return this.compute(str, -1);
  };
}
```

```javascript
function VigenèreCipher(key, abc) {
  this.encode = function(str) {
    return str.split('').map(function(v, i) {
      if(abc.indexOf(v) == -1) {return v;}
      return abc[(abc.indexOf(v) + abc.indexOf(key[i % key.length])) % abc.length];
    }).join('');
  };
  this.decode = function(str) {
    return str.split('').map(function(v, i) {
      if(abc.indexOf(v) == -1) {return v;}
      var ind = abc.indexOf(v) - abc.indexOf(key[i % key.length]);
      return abc[ind < 0 ? ind + abc.length : ind];
    }).join('');
  };
}
```