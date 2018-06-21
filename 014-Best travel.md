[kata](http://www.codewars.com/kata/55e7280b40e1c4a06d0000aa/train/javascript)

```javascript
function chooseBestSum(t, k, ls) {
  var biggestCount = 0;
  var recurseTowns = function(townsSoFar, lastIndex) {
    townsSoFar = townsSoFar || [];
    //base case
    if (townsSoFar.length === k) {
      var sumDistance = townsSoFar.reduce((a,b)=>a+b);
      if (sumDistance <= t && sumDistance > biggestCount) {
        biggestCount = sumDistance;
      }      
      return; //EJECT
    }
    //recursive case
    for (var i = lastIndex + 1 || 0; i < ls.length; i++) {
      recurseTowns(townsSoFar.concat(ls[i]), i);
    }
  }
  recurseTowns();
  
  return biggestCount || null;
}
```

```javascript
function chooseBestSum(t, k, ls) {
  if(ls.length < k)
    return null;
  ls.sort((a, b) => a - b);
  var comb = [];
  for(var i = 0; i < k; i++)
    comb[i] = i;
  var maxSum = comb.reduce((sum, cur) => sum + ls[cur], 0);
  if(maxSum > t)
    return null;
  while(true) {
    var j = k - 1;
    while(comb[j] == ls.length - k + j)
      j--;
    if(j < 0)
      break;
    comb[j]++;
    for(i = j + 1; i < comb.length; i++)
      comb[i] = comb[i - 1] + 1;
    
    var sum = comb.reduce((sum, cur) => sum + ls[cur], 0);
    if(sum > t) {
      comb[j] = ls.length - k + j;
      for(i = j + 1; i < comb.length; i++)
        comb[i] = comb[i - 1] + 1;
    } else if(sum > maxSum)
      maxSum = sum;
    if(maxSum == t)
      return t;
  }
  return maxSum;
}
```

```javascript
function chooseBestSum(t, k, ls) {
  if(k == 0) {
    return 0;
  }
  if(t <= 0 || k < 0 || ls.length < k) {
    return null;
  }
  var best = 0;
  for(var i = 0; i < ls.length; i++) {
    var l = ls.slice();
    l.splice(i, 1);
    var v = ls[i], c = chooseBestSum(t-v, k-1, l);
    if(c != null && c+v > best && c+v <= t) {
      best = c+v;
    }
  }
  return best > 0 ? best : null;
}
```

```javascript
function chooseBestSum(t, k, ls) {
      var possibles = function(arr, min) {
    var fn = function(n, src, got, all) {
        if (n == 0) {
            if (got.length > 0) {
                all[all.length] = got
            }
            return
        }
        for (var j = 0; j < src.length; j++) {
            fn(n - 1, src.slice(j + 1), got.concat([src[j]]), all)
        }
        return
    }
    var all = []
    for (var i = min; i < arr.length; i++) {
        fn(i, arr, [], all)
    }
    all.push(arr)
    return all
  }
  
  var arrComb = possibles(ls, k)

  var arrComb = arrComb.filter(function(item) {
    return item.length === k
  })

  var highNum = 0
  arrComb.forEach(function(item) {
    var arrSum = 0
    for(var i = 0; i < item.length; i++) {
      arrSum += item[i]
    }
    if ((arrSum > highNum) && (arrSum <= t)) highNum = arrSum
  })

  if (highNum >= t) {
    return (t)
  } else if (highNum < 1) {
    return null
  } else {
    return highNum
  }
}
```