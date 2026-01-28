#### Vite + Tailwind + TS

###### **Create your project**
```bash
npm create vite@latest my-project
cd my-project
```
Select `Vanila` $\rightarrow$ `JS`

###### **Install Tailwind CSS**
```bash
npm install tailwindcss @tailwindcss/vite
```

###### **Configure the Vite plugin**
Add the `@tailwindcss/vite` plugin to your Vite configuration.
```ts
import { defineConfig } from 'vite'
import tailwindcss from '@tailwindcss/vite'

export default defineConfig({
	plugins: [
		tailwindcss(),  
	],
})
```

###### **Import Tailwind CSS**
Add an `@import` to your CSS file that imports Tailwind CSS.
```css
@import "tailwindcss";
```

###### **Start your build process**
```bash
npm run dev
```

###### **Start using Tailwind in your HTML**
```html
<!doctype html>
<html>
	<head>
		<meta charset="UTF-8">
		<meta name="viewport" content="width=device-width, initial-scale=1.0">
		<link href="/src/style.css" rel="stylesheet">
	</head>
	<body>
		<h1 class="text-3xl font-bold underline">
			Hello world!
		</h1>
	</body>
</html>
```

###### **Add CSS Hamburgers**
[Hamburgers](https://jonsuh.com/hamburgers/#usage)
[CSS File](https://github.com/jonsuh/hamburgers/blob/master/dist/hamburgers.css)
Copy css file and plug it into HTML 

###### **Install Tailwind VSCode Extension**
`Tailwind CSS IntelliSense`