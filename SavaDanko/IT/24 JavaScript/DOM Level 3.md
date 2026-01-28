###### **Фазы события**
Событие в DOM проходит три фазы (см. спецификацию DOM Level 3 Events):
1. Capturing — событие идёт сверху вниз (`window → document → html → ... → target`), срабатывают обработчики с `{ capture: true }`.
2. Target — событие достигает целевого элемента (`target`).
3. Bubbling — событие поднимается вверх (`target → parent → ... → document → window`), срабатывают обработчики без `capture`.
```js
element.addEventListener('click', handler, true); // capture
element.addEventListener('click', handler); // bubble
```