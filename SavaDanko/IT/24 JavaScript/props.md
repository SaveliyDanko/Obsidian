`props` (сокр. от properties) — это механизм передачи данных в компоненты React.
По сути, каждый компонент в React — это функция, которая принимает объект `props` и возвращает JSX.
    
В отличие от `state` (состояния), `props`:    
- передаются сверху вниз (от родителя к ребёнку);        
- неизменяемы внутри компонента (read-only).
        

###### **Пример**
```tsx
// Компонент, принимающий props
function Greeting(props: { name: string }) {
  return <h1>Hello, {props.name}!</h1>;
}

// Использование
export default function App() {
  return <Greeting name="Saveliy" />;
}
```
Здесь `Greeting` получает объект `props = { name: "Saveliy" }`.

###### **Деструктуризация props**
Чтобы не писать `props.name` каждый раз, можно деструктурировать:
```tsx
function Greeting({ name }: { name: string }) {
  return <h1>Hello, {name}!</h1>;
}
```

###### **Передача разных типов props**
```tsx
type User = {
  name: string;
  age: number;
};

function UserCard({ user, isOnline }: { user: User; isOnline: boolean }) {
  return (
    <div>
      <h2>{user.name} ({user.age})</h2>
      <p>Status: {isOnline ? "Online" : "Offline"}</p>
    </div>
  );
}

export default function App() {
  return <UserCard user={{ name: "Liza", age: 19 }} isOnline={true} />;
}
```

###### **Props по умолчанию (default props)**
Можно задать значения по умолчанию, если пропс не передали:
```tsx
type ButtonProps = {
  text?: string;
};

function Button({ text = "Click me" }: ButtonProps) {
  return <button>{text}</button>;
}

export default function App() {
  return (
    <>
      <Button /> {/* покажет "Click me" */}
      <Button text="Submit" /> {/* покажет "Submit" */}
    </>
  );
}
```

###### **Передача функций как props**
Очень важно — можно передавать колбэки:
```tsx
type ButtonProps = {
  onClick: () => void;
};

function Button({ onClick }: ButtonProps) {
  return <button onClick={onClick}>Click me</button>;
}

export default function App() {
  const handleClick = () => alert("Clicked!");
  return <Button onClick={handleClick} />;
}
```

###### **Передача `children`**
Специальный проп `children` используется для передачи JSX внутрь компонента:
```tsx
type CardProps = {
  children: React.ReactNode;
};

function Card({ children }: CardProps) {
  return <div className="border p-4">{children}</div>;
}

export default function App() {
  return (
    <Card>
      <h2>Hello</h2>
      <p>This is inside the card!</p>
    </Card>
  );
}
```