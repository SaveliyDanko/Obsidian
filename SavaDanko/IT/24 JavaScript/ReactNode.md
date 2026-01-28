`ReactNode` — это всё, что React может отрендерить.  
В отличие от `ReactElement`, `ReactNode` — это широкий тип.

###### **Что может быть `ReactNode`:**
- `ReactElement` — `<div>Hello</div>`
- строка — `"Hello"`
- число — `42`
- `null`
- `undefined`
- `boolean` — `true` / `false` (не рендерятся)
- массив других `ReactNode`

###### **Пример**
```tsx
import { ReactNode } from "react";

type Props = {
  children: ReactNode;
};

function Wrapper({ children }: Props) {
  return <div className="wrapper">{children}</div>;
}

export default function App() {
  return (
    <Wrapper>
      <h1>Hello</h1>
      World
      {123}
    </Wrapper>
  );
}
```
Здесь `children` — это ReactNode, потому что внутри `<Wrapper>` могут быть:
- элементы (`<h1>Hello</h1>`)
- текст (`"World"`)
- числа (`123`)
- массивы элементов.