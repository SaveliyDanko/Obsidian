`ReactElement` — это объект, который React создаёт, когда вы пишете JSX.
Он описывает, что React должен отрендерить в DOM или в нативный UI.
Это не DOM-элемент, а чистый JS-объект.

###### **Пример**
```jsx
const element = <h1>Hello</h1>;
console.log(element);
```

Выведет примерно:
```js
{
  type: "h1",
  props: { children: "Hello" },
  key: null,
  ref: null,
  ...
}
```
Это и есть `ReactElement`.

###### **Как создаётся**
```jsx
// JSX
const element = <h1>Hello</h1>;

// Без JSX
const element = React.createElement("h1", null, "Hello");
```
Оба варианта дадут `ReactElement`.
