You can create a JavaScript Set by:
- Passing an array to `new Set()`
- Create an empty set and use `add()` to add values

Pass an array to the `new Set()` constructor:
```js
// Create a Set  
const letters = new Set(["a","b","c"]);
```

Create a Set and add values:
```js
// Create a Set  
const letters = new Set();  
  
// Add Values to the Set  
letters.add("a");  
letters.add("b");  
letters.add("c");
```
If you add equal elements, only the first will be saved.

###### **size property**
```js
// Create a new Set  
const mySet = new Set(["a","b","c"]);  
  
// The number of elements are  
mySet.size;
```

###### **Listing Set Elements**
You can list all Set elements (values) with a `for..of` loop:
```js
// Create a Set  
const letters = new Set(["a","b","c"]);  
  
// List all Elements  
let text = "";  
for (const x of letters) {  
  text += x;  
}
```

###### **has()**
The `has()` method returns `true` if a specified value exists in a set.
```js
// Create a Set  
const letters = new Set(["a","b","c"]);  
  
// Does the Set contain "d"?  
answer = letters.has("d");
```

###### **forEach()**
The `forEach()` method invokes a function for each Set element:
```js
// Create a Set  
const letters = new Set(["a","b","c"]);  
  
// List all entries  
let text = "";  
letters.forEach (function(value) {  
  text += value;  
})
```

###### **values()**
The `values()` method returns an Iterator object with the values in a Set:
```js
// Create a Set  
const letters = new Set(["a","b","c"]);  
  
// Get all Values  
const myIterator = letters.values();  
  
// List all Values  
let text = "";  
for (const entry of myIterator) {  
  text += entry;  
}
```

###### **keys()**
A Set has no keys, so `keys()` returns the same as `values()`.
The `keys()` method returns an Iterator object with the values in a Set:
```js
// Create a Set  
const letters = new Set(["a","b","c"]);  
  
// Create an Iterator  
const myIterator = letters.keys();  
  
// List all Elements  
let text = "";  
for (const x of myIterator) {  
  text += x;  
}
```

###### **entries()**
The `entries()` method returns an Iterator with `[value,value]` pairs from a Set.
The `entries()` method is supposed to return a `[key,value]` pair from an object.
A Set has no keys, so the `entries()` method returns `[value,value]`.

```js
// Create a Set  
const letters = new Set(["a","b","c"]);  
  
// Get all Entries  
const myIterator = letters.entries();  
  
// List all Entries  
let text = "";  
for (const entry of myIterator) {  
  text += entry;  
}
```

###### **clear()**
The `clear()` method removes all values from a set.
```js
// Create a Set  
const letters = new Set(["a","b","c"]);  
  
// Clear Set  
letters.clear()
```

###### **delete()**
The `delete()` method removes a specified value from a set.
```js
// Create a Set
const letters = new Set(["a","b","c"]);

// Remove one Element
letters.delete("a");
```
Return Value:
Boolean	true if the value existed, otherwise false.

###### **difference()**
The `difference()` method returns the difference between two sets.
The `difference()` method returns a new set containing elements which are in this set but not in the argument set:
```js
const A = new Set(['a','b','c']);  
const B = new Set(['b','c','d']);  
  
const C = A.difference(B);
```
Parameters:
`set` - The set to return the difference between.

Return Value:
`Set` - A set object with the difference of the two sets.

###### **intersection()**
The `intersection()` method returns the intersection of two sets.
![[Pasted image 20250806142658.png]]
```js
const A = new Set(['a','b','c']);  
const B = new Set(['b','c','d']);  
  
const C = A.intersection(B);
```
Parameters:
`set` - The set to do the intersection operation with.

Return Value:
`Set` - A set object with the intersection of the two sets.

###### **isDisjointFrom()**
The `isDisjointFrom` method returns `true` if no elements in this set are elements in the argument set:
![[Pasted image 20250806143016.png]]
```js
const A = new Set(['a','b','c']);  
const B = new Set(['b','c','d']);  
  
let answer = A.isDisjointFrom(B);
```
Parameters:
`set` - The set to test against.

Return Value:
`Boolean` - `true` if no elements in this set are elements in the argument set, otherwise `false`.

###### **isSubsetOf()**
The `isSubsetOf()` method returns `true` if all elements in this set are elements in the argument set:
![[Pasted image 20250806143142.png]]
```js
const A = new Set(['a','b','c']);  
const B = new Set(['b','c','d']);  
  
let answer = A.isSubsetOf(B);
```
Parameters:
`set` - The set to test against.

Return Value:
`Boolean` - `true` if all elements in this set are elements in the argument set, otherwise `false`.

###### **isSupersetOf()**
The `isSupersetOf()` method returns `true` if all elements in the argument set are also in this set:
![[Pasted image 20250806143233.png]]
```js
const A = new Set(['a','b','c']);  
const B = new Set(['b','c','d']);  
  
let answer = A.isSupersetOf(B);
```

###### **symmetricDifference()**
The `symmetricDifference()` method returns the symmetric difference between two sets.
The `symmetricDifference()` method returns a new set containing elements which are in this set or in the argument set, but not in both:
![[Pasted image 20250806152128.png]]
```js
const A = new Set(['a','b','c']);  
const B = new Set(['b','c','d']);  
  
const C = A.symetricDifference(B);
```
Parameters:
`set` - The set to test for symmetric difference.

Return Value:
`Boolean` - A set object with the symmetric difference.

###### **union()**
The `union()` method returns the union of two sets.
The `union()` method returns a new set containing the elements which are in this set, or in the argument set, or in both.
![[Pasted image 20250806152454.png]]
Parameters:
`set` -  The set to union.

Return Value:
`Boolean` - A set object with the union of the two sets.
