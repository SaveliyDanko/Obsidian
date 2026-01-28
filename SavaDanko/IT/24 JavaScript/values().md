The `values()` method returns an Iterator with the values from a [[DOMTokenList]].
```js
const list = document.body.childNodes;  
for (let x of list.values()) {  
  text += x;  
}
```
