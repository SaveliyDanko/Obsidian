The `forEach()` method executes a callback function for each token in a [[DOMTokenList]].
```js
let list = document.getElementById("demo").classList;
list.forEach(  
  function(token, index) {  
    text += index + " " + token;  
  }  
);
```
