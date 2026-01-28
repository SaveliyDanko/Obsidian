---
tags:
  - review
sr-due: 2026-02-26
sr-interval: 69
sr-ease: 250
---

---
[State](https://tailwindcss.com/docs/hover-focus-and-other-states#hover-focus-and-active)

---
В Tailwind любому утилитарному классу можно задать условное поведение, добавив вариант (variant) — префикс, который описывает состояние, при котором должен применяться этот класс.

Например, чтобы применить класс `bg-sky-700` при наведении курсора,  
достаточно написать `hover:bg-sky-700`:
```html
<button class="bg-sky-500 hover:bg-sky-700 ...">
  Save changes
</button>
```

###### **Типы состояний и вариантов, поддерживаемые Tailwind**
Tailwind имеет встроенные варианты практически для любых случаев:
- Псевдоклассы — `:hover`, `:focus`, `:first-child`, `:required`
- Псевдоэлементы — `::before`, `::after`, `::placeholder`, `::selection`
- Медиа запросы — адаптивные брейкпоинты (`sm:`, `md:`, `lg:`), тёмная тема (`dark:`)
- Селекторы атрибутов — `[dir="rtl"]`, `[open]`
- Дочерние селекторы — `& > *`, `& *`

###### **Комбинирование (стек) вариантов**
Варианты можно комбинировать, чтобы задать стили для более специфичных ситуаций. Например, изменить цвет фона в тёмной теме, на среднем брейкпоинте и при наведении одновременно:
```html
<button class="dark:md:hover:bg-fuchsia-600 ...">
  Save changes
</button>
```

---
`:hover`
Style an element when the user hovers over it with the mouse cursor using the 
```html
<div class="bg-black hover:bg-white ...">  <!-- ... --></div>
```

---
`:focus`
Style an element when it has focus using the `focus` variant:
```html
<input class="border-gray-300 focus:border-blue-400 ..." />
```

---
`:active`
Style an element when it is being pressed using the `active` variant:
```html
<button class="bg-blue-500 active:bg-blue-600 ...">Submit</button>
```

---
`:visited`
Style a link when it has already been visited using the `visited` variant:
```html
<a href="https://seinfeldquotes.com" class="text-blue-600 visited:text-purple-600 ..."> Inspiration </a>
```

---
`:target`
Style an element if its ID matches the current URL fragment using the `target` variant:
```html
<div id="about" class="target:shadow-lg ...">
	<!-- ... -->
</div>
```

---
`:first-child`
Style an element if it's the first child using the `first` variant:
```html
<ul>
	{#each people as person}
		<li class="py-4 first:pt-0 ...">
			<!-- ... -->
		</li>
	{/each}
</ul>
```

---
`:last-child`
Style an element if it's the last child using the `last` variant:
```html
<ul>
	{#each people as person}
		<li class="py-4 last:pb-0 ...">
			<!-- ... -->
		</li>
	{/each}
</ul>
```

---
`:nth-child()`
Style an element at a specific position using the `nth` variant:
```html
<nav>
	<img src="/logo.svg" alt="Vandelay Industries" />
		{#each links as link}
			<a href="#" class="mx-2 nth-3:mx-6 nth-[3n+1]:mx-7 ...">
				<!-- ... -->
			</a>
		{/each}
	<button>More</button>
</nav>
```