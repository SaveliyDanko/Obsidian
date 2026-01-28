`DOMContentLoaded` — это событие объекта `document`, которое срабатывает, когда HTML полностью загружен и разобран браузером, но ресурсы (картинки, стили, шрифты, iframe) могут ещё загружаться.

###### **Пример использования**
```js
document.addEventListener('DOMContentLoaded', () => {
  console.log('DOM готов!');
  const el = document.getElementById('app');
  el.textContent = 'Привет!';
});
```
Можно безопасно работать с DOM-элементами — они уже существуют.

###### **Когда не нужен `DOMContentLoaded`**
- Если твой `<script>` подключён внизу `<body>`.
- Если используешь `<script defer>` в `<head>` — код выполнится после парсинга HTML, до события `DOMContentLoaded`.
- Если `<script type="module">` — он ведёт себя как `defer` по умолчанию.
