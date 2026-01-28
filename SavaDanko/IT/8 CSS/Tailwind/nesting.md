Внутри Tailwind используется [Lightning CSS](https://lightningcss.dev/) для обработки вложенного CSS. Например:
`typography.css`
```css
.typography {
  p {
    font-size: var(--text-base);
  }
  img {
    border-radius: var(--radius-lg);
  }
}
```

Tailwind преобразует такой код в плоский CSS, понятный всем современным браузерам:
`output.css`
```css
.typography p {
  font-size: var(--text-base);
}

.typography img {
  border-radius: var(--radius-lg);
}
```
Современные браузеры уже достаточно хорошо поддерживают нативную вложенность CSS, так что препроцессор для этого часто не требуется, даже если вы не используете Tailwind.