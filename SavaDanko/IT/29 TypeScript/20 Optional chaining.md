`?.` позволяет обращаться к свойствам/методам только если объект не `null` и не `undefined`.  
Если объект `null`/`undefined` → выражение вернёт `undefined` вместо ошибки.
```ts
interface User {
  profile?: {
    name?: string;
  };
}

const user: User = {};

// Без optional chaining:
console.log(user.profile.name); // ❌ Ошибка: Cannot read property 'name'

// С optional chaining:
console.log(user.profile?.name); // ✅ undefined
```

###### **Optional chaining with functions**
```ts
interface Config {
  log?: (msg: string) => void;
}

const config: Config = {};

config.log("Hello"); // ❌ Ошибка: log is undefined

config.log?.("Hello"); // ✅ ничего не вызовется
```

###### **Optional chaining with arrays**
Можно безопасно обращаться к элементам массива:
```ts
const arr: string[] | undefined = undefined;

console.log(arr[0]); // ❌ Ошибка: Cannot read property '0'

console.log(arr?.[0]); // ✅ undefined
```
