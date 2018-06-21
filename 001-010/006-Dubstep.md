[kata](https://www.codewars.com/kata/dubstep/train/javascript)

```javascript
function songDecoder(song){
    var str = song.replace(/WUB/g, " ");
    str = str.replace(/^\s+|\s+$/g, "");
    strs = str.split(" ");

    var old = "";
    strs.forEach(function(value, index, arr){
      if (value != ''){
        if (index != arr.length - 1){
            old += value + " ";
        } else {
            old += value;
        }
      }
    });

    return old;
}
```

```javascript
function songDecoder(song){
  return song.replace(/(WUB)+/g," ").trim()
}
```

```javascript
function songDecoder(song){
  return song.split('WUB').filter(Boolean).join(' ');
}
```

```javascript
var songDecoder = (song) => song.split('WUB').filter(x => x !== '').join(' ')
```