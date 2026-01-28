The `entries()` method returns an Iterator with the key/value pairs from a [[DOMTokenList]].

```js
let list = document.getElementById("demo").classList;

for (let x of list.entries()) {  
  text += x[0] + " " + x[1];  
}
```