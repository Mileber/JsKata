[kata](https://www.codewars.com/kata/55f89832ac9a66518f000118/train/javascript)

```javascript
function simplify(poly){
    var arr = poly.split("");
    var temp = "";
    var count = "";
    var arrNum = [];
    var arrWord = [];
    if (arr[0] != '-') {
        arr.unshift('+')
    } 
    for (var i=0;i<arr.length;i++) {
        if (arr[i] == '-') {
            if (temp != "") {
                arrWord.push(temp);
            temp = "";
            }
            if (!isNaN(arr[i+1])) {
              count = "-";
            }else {
              count = "-1";
            }
        } else if (arr[i] == '+') {
            if (temp != "") {
                arrWord.push(temp);
            temp = "";
            }
            if (!isNaN(arr[i+1])) {
              count = "+";
            }else {
              count = "+1";
            }
        }else if (!isNaN(arr[i])) {
            if (count == "" & temp != "") {
                arrWord.push(temp);
            }
            count = count + arr[i];
        } else if (i == arr.length-1){
            if (count != "") {
              arrNum.push(count);
              count = "";
            } 
          temp = temp + arr[i];
          arrWord.push(temp);
        } else {
            if (count != "") {
              arrNum.push(count);
              count = "";
            }
            temp = temp + arr[i];
        }
    }
    
    for (var j=0;j<arrWord.length;j++) {
      var word = arrWord[j].split("");
      word.sort();
      arrWord[j] = word.join("");
    }
    
    var arrResult = [];
    for(var k=0;k<arrWord.length;k++) {
      if (arrResult[arrWord[k]] == null) {
        arrResult[arrWord[k]] = parseInt(arrNum[k]);
      } else {
        arrResult[arrWord[k]] = arrResult[arrWord[k]] + parseInt(arrNum[k]);
      }
    }
    
    var keys = [];
    for (var r in arrResult) {
      if (r != 'shuffle')
        keys.push(r);
    }

    keys.sort();
    keys.sort(function(a,b) {
      if (a.length > b.length) {
        return 1;
      } else if (a.length < b.length) {
        return -1;
      } 
    });
    
    var result = "";
    var num = 0;
    keys.forEach(key => {
      if (arrResult[key] != 0) {
        if (num == 0) {
          num = 1;
          if (arrResult[key] == "-1") {
            result = result + "-" + key;
          } else if (arrResult[key] == "1") {
            result = result + key;
          } else {
            result = result + arrResult[key] + key;
          }
        } else {
          if (arrResult[key] == "-1") {
            result = result + "-" + key;
          } else if (arrResult[key] == "1") {
            result = result + "+" +key;
          } else {
            if ( arrResult[key] < 0 ) {
              result = result + arrResult[key] + key;
            } else {
              result = result + "+" + arrResult[key] + key;
            }
          }
        }
      }
      
    })
    
    return result
}
```

```javascript
function simplify(poly){
  var h = {};
  poly.match(/[+-]?[^+-]+/g).forEach(x => {
    var m = x.match(/[a-z]+/)[0],
        k = x.replace(m, '');
    m = m.split('').sort().join('');
    k = Number(/\d/.test(k) ? k : k+'1');
    h[m] = (h[m]||0) + k;
  });
  return Object.keys(h)
    .filter(m => h[m])
    .sort((x, y) => x.length - y.length || (x < y ? -1 : 1))
    .map((m, i) => ({
      sign : h[m] < 0 ? '-' : i > 0 ? '+' : '',
      k : Math.abs(h[m]),
      m : m
    }))
    .map(o => o.sign + (o.k == 1 ? '' : o.k) + o.m).join('');
}
```

```javascript
function Monomial({coef, vars = ''}) {
  return {
    coef,
    vars,
    length: vars.length,
    combine(other) {
      if (vars !== other.vars) {
        throw new Error(`Can't combine 2 monomials with different variables: ${vars} != ${other.vars}`)
      }
      return Monomial({coef: coef + other.coef, vars})
    },
    toString() {
      if (coef === 0) {
        return ''
      }
      let str = `${coef > 0 ? '+' : ''}${coef}${vars}`
      if (Math.abs(coef) === 1) {
        str = str.replace('1', '')
      }
      return str
    }
  }
}

Monomial.fromExpr = (expr) => {
  const sign = ['+', '-'].includes(expr[0]) ? expr[0] : '+'
  const coefMatch = expr.match(/\d+/)
  const coef = coefMatch ? parseInt(`${sign}${coefMatch[0]}`, 10) : parseInt(`${sign}1`)
  const varsMatch = expr.match(/[a-z]+$/)
  const vars = Array.from(varsMatch ? varsMatch[0] : '').sort().join('')

  return Monomial({coef, vars})
}

function Polynomial({monomials}) {
  return {
    monomials,
    simplify: () => {
      const monomialsByVars = new Map()
      monomials.forEach((monomial) => {
        const group = monomialsByVars.get(monomial.vars) || []
        monomialsByVars.set(monomial.vars, group.concat([monomial]))
      })

      const nextMonomials = Array.from(monomialsByVars).map(([vars, monomials]) => {
        const zero = Monomial({coef: 0, vars})
        return monomials.reduce((acum, monomial) => monomial.combine(acum), zero)
      })
      .sort((m1, m2) => {
        if (m1.length === m2.length) {
          return m1.vars.localeCompare(m2.vars)
        }
        return m1.length < m2.length ? -1 : 1
      })

      return Polynomial({
        monomials: nextMonomials,
      })
    },
    toString: () => {
      const str = monomials.map((m) => m.toString()).join('')
      if (str.startsWith('+')) {
        return str.slice(1)
      }
      return str
    }
  }
}

Polynomial.fromExpr = (expr) => {
  const expressions = expr.match(/([\+\-]?\d*[a-z]+)/gi)
  const monomials = expressions.map(Monomial.fromExpr)

  return Polynomial({monomials})
}

function simplify(poly) {
  const polynomial = Polynomial.fromExpr(poly)
  return polynomial.simplify().toString()
}
```