**BEM** (Block–Element–Modifier) — это подход к написанию HTML и CSS, который делает код структурированным, читаемым и легко масштабируемым.

###### Общий синтаксис
```
.block {}
.block__element {}
.block--modifier {}
.block__element--modifier {}
```

###### **Пример 1 — Меню**
HTML:
```html
<ul class="menu">
  <li class="menu__item menu__item--active">Home</li>
  <li class="menu__item">About</li>
  <li class="menu__item">Contact</li>
</ul>
```

###### **CSS:**
```scss
.menu {
  list-style: none;
  padding: 0;
}

.menu__item {
  display: inline-block;
  padding: 10px;
}

.menu__item--active {
  font-weight: bold;
  color: blue;
}
```

###### **Пример 2 — Кнопка**
```html
<button class="button button--primary">Submit</button>
<button class="button button--secondary">Cancel</button>
```

```scss
.button {
  padding: 8px 16px;
  border: none;
  cursor: pointer;
}

.button--primary {
  background: blue;
  color: white;
}

.button--secondary {
  background: gray;
  color: black;
}
```
