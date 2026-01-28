**Всплытие событий** — это процесс, при котором событие, произошедшее на вложенном элементе, передаётся вверх по дереву DOM через его родителей, вплоть до объекта `document` и `window`.

###### **Как это работает**
1. Ты кликаешь на элемент (например, `<button>`).
2. Сначала событие обрабатывается на самом элементе (`target`).
3. Потом оно всплывает вверх — идёт к родителю (`<div>`), потом выше (`<body>`), потом к `document`, и наконец к `window`.
    
###### **Этапы жизненного цикла события (DOM Level 3)**
Событие проходит три фазы:
1. Фаза погружения (capturing) — событие идёт сверху вниз: `window → document → html → body → … → target`.
2. Целевая фаза (target) — событие обрабатывается на самом элементе, где произошло (`event.target`).
3. Фаза всплытия (bubbling) — событие поднимается обратно: `target → parent → … → document → window`.

###### **Пример**
```html
<div id="parent" style="padding:20px; background:lightblue;">
  Parent
  <button id="child">Click me</button>
</div>

<script>
document.getElementById('parent').addEventListener('click', () => {
  console.log('Клик по PARENT');
});

document.getElementById('child').addEventListener('click', () => {
  console.log('Клик по CHILD');
});
</script>
```
Если кликнуть на кнопку:
```
Клик по CHILD
Клик по PARENT
```
Потому что `click` всплывает от кнопки к родительскому `<div>`.

###### **Как остановить всплытие**
```js
element.addEventListener('click', e => {
  e.stopPropagation(); // остановка дальнейшего всплытия
});
```
Можно полностью прервать и обработку других обработчиков:
```js
e.stopImmediatePropagation();
```

---

###### **Делегирование событий (практическое применение)**
Вместо того, чтобы вешать обработчик на каждую кнопку, можно повесить его на контейнер и определить цель клика:
```js
document.getElementById('parent').addEventListener('click', e => {
  if (e.target.tagName === 'BUTTON') {
    console.log('Клик по кнопке:', e.target.textContent);
  }
});
```
Это возможно только благодаря всплытию.
