[kata](http://www.codewars.com/kata/5263c6999e0f40dee200059d/train/javascript)

```javascript
function getPINs(observed) {
  return combineArr(observed.split(""));
  function po(a) {
      switch(a) {
          case "1":
              return ["2", "4", '1'];
              break;
          case "2":
              return ["1", "3", "5", '2'];
              break;
          case '3':
              return ['2', '6', '3'];
              break;
          case '4':
              return ['1', '5', '7', '4'];
              break;
          case '5':
              return ['2', '4', '6', '8', '5'];
              break;
          case '6':
              return ['3', '5', '9', '6'];
              break;
          case '7':
              return ['4', '8', '7'];
              break;
          case '8':
              return ['5', '7', '9', '0', '8'];
              break;
          case '9':
              return ['6', '8', '9'];
              break;
          case '0':
              return ['8', '0'];
              break;
      }
  }
  function combineArr(arr) {
      if (arr.length == 1) {
          return po(arr[0]);
      } else if (arr.length == 2) {
          var arr1 = po(arr[0]);
          var arr2 = po(arr[1]);
          
          var result = [];
          for (var i=0; i<arr1.length; i++) {
              for (var j=0; j<arr2.length; j++) {
                  result.push(arr1[i] + arr2[j]);
              }
          }
          return result;
      } else if (arr.length > 2) {
          var arr3 = po(arr[0]);
          arr.shift()
          var arr4 = combineArr(arr);
          var result = [];
          for (var m=0; m<arr3.length; m++) {
              for (var n=0; n<arr4.length; n++) {
                  result.push(arr3[m] + arr4[n]);
              }
          }
          return result;
      }
  }
}
```

```javascript
function getPINs(observed) {
  var adjacent = [
    /* 0 */ [0, 8],
    /* 1 */ [1, 2, 4],
    /* 2 */ [1, 2, 3, 5],
    /* 3 */ [2, 3, 6],
    /* 4 */ [1, 4, 5, 7],
    /* 5 */ [2, 4, 5, 6, 8],
    /* 6 */ [3, 5, 6, 9],
    /* 7 */ [4, 7, 8],
    /* 8 */ [5, 7, 8, 9, 0],
    /* 9 */ [6, 8, 9]
  ];
  
  return observed
    .split('')
    .map(function(d) { return adjacent[d|0]; })
    .reduce(function(pa, da) {
      return da.reduce(function(pv, d) {
        return pv.concat(pa.map(function(p) {
          return '' + p + d;
        }));
      }, []);
    }, ['']);
}
```

```javascript
function getPINs(observed) {
  return observed.split('')
  .map( t => ({
    '0': [ '0', '8' ],
    '1': [ '1', '2', '4' ],
    '2': [ '1', '2', '3', '5' ],
    '3': [ '2', '3', '6' ],
    '4': [ '1', '4', '5', '7' ],
    '5': [ '2', '4', '5', '6', '8' ],
    '6': [ '3', '5', '6', '9' ],
    '7': [ '4', '7', '8' ],
    '8': [ '5', '7', '8', '9', '0' ],
    '9': [ '6', '8', '9' ]
  }[t]))
  .reduce((pre, cur)=> [].concat.apply([], pre.map(t => cur.map(g => t + g))));
}
```

```javascript
function mixNMatch(add, addTo) {
  var out = [];
  add.forEach(function(v, i) {addTo.forEach(function(w, j) {out.push(v + w);});});
  return out;
}

function getPINs(observed) {
  var map = {1:['1','2','4'], 2:['1','2','3','5'], 3:['2','3','6'], 4:['1','4','5','7'], 5:['2','4','5','6','8'],
             6:['3','5','6','9'], 7:['4','7','8'], 8:['5','7','8','9','0'], 9:['6','8','9'], 0:['8','0']};
  return observed.length == 1 ? map[observed[0]] : mixNMatch(map[observed[0]], getPINs(observed.slice(1)));
}
```