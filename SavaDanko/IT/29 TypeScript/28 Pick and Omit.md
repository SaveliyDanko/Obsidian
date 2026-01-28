#### **`Pick<Type, Keys>`**
Constructs a type by picking the set of properties `Keys` (string literal or union of string literals) from `Type`.
```ts
interface Todo {
  title: string;
  description: string;
  completed: boolean;
}

type TodoPreview = Pick<Todo, "title" | "completed">;
 
const todo: TodoPreview = {
  title: "Clean room",
  completed: false,
};
```

#### **`Omit<Type, Keys>`**
Constructs a type by picking all properties from `Type` and then removing `Keys` (string literal or union of string literals).
```ts
interface Todo {
  title: string;
  description: string;
  completed: boolean;
  createdAt: number;
}
 
type TodoPreview = Omit<Todo, "description">;
 
const todo: TodoPreview = {
  title: "Clean room",
  completed: false,
  createdAt: 1615544252770,
};
```