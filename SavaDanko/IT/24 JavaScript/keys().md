The `keys()` method returns an Iterator with the keys from a [[DOMTokenList]].
```js
const list = document.body.childNodes;  
for (let x of list.keys()) {  
  text += x;  
}
```
