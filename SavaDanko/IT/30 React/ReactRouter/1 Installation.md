You can start with a React template from Vite and choose "React", otherwise bootstrap your application however you prefer.
```bash
npx create-vite@latest
```
Next install React Router from npm:
```bash
npm i react-router
```
Finally, render a `<BrowserRouter>` around your application:
```jsx
import React from "react";
import ReactDOM from "react-dom/client";
import { BrowserRouter } from "react-router";
import App from "./app";

const root = document.getElementById("root");

ReactDOM.createRoot(root).render(
  <BrowserRouter>
    <App />
  </BrowserRouter>,
);
```