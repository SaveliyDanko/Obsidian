Все современные браузеры поддерживают [нативные CSS-переменные](https://developer.mozilla.org/docs/Web/CSS/Using_CSS_custom_properties) без необходимости использования препроцессоров.

Пример (`typography.css`):
```css
.typography {
  font-size: var(--text-base);
  color: var(--color-gray-700);
}
```
Tailwind активно использует CSS-переменные во внутренней работе, поэтому если вы можете применять Tailwind в проекте, вы также можете использовать нативные CSS-переменные.