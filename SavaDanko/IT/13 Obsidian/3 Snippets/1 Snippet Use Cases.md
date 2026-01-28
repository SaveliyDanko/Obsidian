**Snippets (CSS snippets)** — это небольшие пользовательские фрагменты CSS-кода, которые позволяют менять внешний вид Obsidian без написания полноценных тем.

##### ==Использование snippets==
###### 1. Создаём папку `.obsidian/snippets/`

###### 2. Создаём файл, например: `highlight-color.css`

###### 3. Добавляем CSS-код:
```css
.markdown-preview-view mark {
  background-color: #a8d8ea !important;
  color: black !important;
}

.cm-s-obsidian span.cm-highlight {
  background-color: #a8d8ea !important;
  color: black !important;
}
```

###### 4. Включаем snippets в настройках:
`Settings → Appearance → CSS snippets`


