`<StrictMode>` позволяет находить распространённые ошибки в ваших компонентах на раннем этапе разработки.
```jsx
<StrictMode>
  <App />
</StrictMode>
```

Используйте `StrictMode`, чтобы включить дополнительные проверки и предупреждения во время разработки для дерева компонентов внутри него:
```jsx
import { StrictMode } from 'react';
import { createRoot } from 'react-dom/client';

const root = createRoot(document.getElementById('root'));
root.render(
  <StrictMode>
    <App />
  </StrictMode>
);
```
