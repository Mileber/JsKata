[kata](https://www.codewars.com/kata/5629db57620258aa9d000014/train/javascript)


```javascript
function mix(s1, s2) {
    var regs = /[^a-z]/g;
    var arr1 = s1.replace(regs, "").split("").sort().join('').match(/([^])\1+/g) || [];
    var arr2 = s2.replace(regs, "").split("").sort().join('').match(/([^])\1+/g) || [];
    
    function sort2(a,b){
        if (a.length > b.length) {
          return -1;
        } else if (a.length < b.length) {
          return 1;
        } else {
          if (b<a) {
            return 1;          
          } else if (b>a) {
            return -1
          }
        }
    }
    
    arr1.sort(sort2);
    arr2.sort(sort2);
    
    var arrNew = [];
    arr1.forEach((element, i) => {
      var str1 = element.slice(0,1);
      var f = true;
      arr2.forEach((ele,i) => {
        var str2 = ele.slice(0,1);
        if (str1 == str2) {
          if (element.length > ele.length) {
            var obj = {
                ele: element,
                index: '1:'
            };
            arrNew.push(obj);
          } else if (element.length == ele.length) {
            var obj = {
                ele: element,
                index: '=:'
            };
            arrNew.push(obj);
          } else if (element.length < ele.length) {
            var obj = {
                ele: ele,
                index: '2:'
            };
            arrNew.push(obj);
          }
          arr2.splice(i, 1);
          f = false;
        }
      })
      if (f) {
        var obj = {
            ele: element,
            index: '1:'
        };
        arrNew.push(obj);
      }
    });
    
    arr2.forEach(ele2 => {
     var obj = {
            ele: ele2,
            index: '2:'
        };
        arrNew.push(obj);
    })
    
    arrNew.sort((a, b) => {
      if (a.ele.length > b.ele.length) {
        return -1;
      } else if (a.ele.length < b.ele.length) {
        return 1;
      } else {
        if (a.index > b.index) {
            return 1;
        } else if (a.index < b.index) {
            return -1;
        } else {
          var t1 = b.ele.slice(0,1);
          var t2 = a.ele.slice(0,1);
          return 0-(t1.charCodeAt(0)-t2.charCodeAt(0));
        }
      }
    })
    
    var result = "";
    arrNew.forEach(ele => {
      result += ele.index + ele.ele + '/';
    })
    
    return result.slice(0, result.length-1);
}
```

```javascript
function mix(s1, s2) {
  var counter = s => s.replace(/[^a-z]/g,'').split('').sort().reduce((x,y)=> (x[y] = 1 + (x[y]||0), x),{});
  s1 = counter(s1); s2 = counter(s2);
  var res = [], keys = new Set(Object.keys(s1).concat(Object.keys(s2)));
  keys.forEach(key => {
    var c1 = s1[key]||0, c2 = s2[key]||0, count = Math.max(c1, c2);
    if (count>1) {
      var from = [1, '=', 2][Math.sign(c2-c1)+1];
      var str = [...Array(count)].map(_=>key).join('');
      res.push(from+':'+str);
    }
  });
  return res.sort((x, y) => y.length - x.length || (x < y ? -1 : 1)).join('/');
}
```

```javascript
const alphabet = 'abcdefghijklmnopqrstuvwxyz'.split('');

function mix(s1, s2) {
  return alphabet
    .map(char => {
      const s1Count = s1.split('').filter(x => x === char).length,
            s2Count = s2.split('').filter(x => x === char).length,
            maxCount = Math.max(s1Count, s2Count);

      return {
        char: char,
        count: maxCount,
        src: maxCount > s1Count ? '2' : maxCount > s2Count ? '1' : '='
      };
    })
    .filter(c => c.count > 1)
    .sort((objA, objB) => objB.count - objA.count || (objA.src + objA.char > objB.src + objB.char ? 1 : -1))
    .map(c => `${c.src}:${c.char.repeat(c.count)}`)
    .join('/');
}
```

```javascript
const group = (a) => a.reduce((g, v) => Object.assign(g, { [v]: ++g[v] || 1 }), {})

const mix = (s1, s2) => {
  const s1_values = group(s1.match(/[a-z]/g))
  const s2_values = group(s2.match(/[a-z]/g))

  return Object.keys(Object.assign({}, s1_values, s2_values))
    .map((key) => {
      const s1len = s1_values[key] || 0
      const s2len = s2_values[key] || 0
      const l = Math.max(s1len, s2len)

      return l > 1 && `${s1len === s2len ? '=' : s1len > s2len && '1' || '2'}:${key.repeat(l)}`
    })
    .filter(Boolean)
    .sort((a, b) => a.length < b.length
      ? 1
      : a.length > b.length
        ? -1
        : a > b ? 1 : a < b ? -1 : 0
    )
    .join('/')
}
```