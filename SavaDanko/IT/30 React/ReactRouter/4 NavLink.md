[NavLink](https://reactrouter.com/api/components/NavLink)

---
`<NavLink>` — это специальный компонент React Router, обертка над `<Link>`.
Он может автоматически добавлять CSS-класс, когда ссылка совпадает с текущим URL.
```jsx
import { NavLink } from "react-router-dom";

<NavLink to="/about">About</NavLink>
```

###### **Параметр `to`**
`to` — обязательный параметр, указывающий путь, на который должна вести ссылка.
```jsx
<NavLink to="/about">About</NavLink>
```
