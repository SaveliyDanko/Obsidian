```css
--background-primary: #2e2e2e;
--background-primary-alt: #2e2e2e; 
  
--background-secondary: #232323;
--background-secondary-alt: #232323;

--background-modifier-border: #3e3e3e;

--cursor-line-background: #bda99012;

--bold-color: #eceff4;
```

```css
/* BreakLine*/

.cm-line hr,
.markdown-preview-view hr {
	margin-block-start: 4em;
	margin-block-end: 4em;
	border: none;
	height: 0;
	border-bottom: 1px solid;
	border-image-slice: 1;
	border-width: 1px;
	border-image-source: linear-gradient(to right, transparent, var(--text-accent), transparent);
}

  

.cm-line hr::after,
.markdown-preview-view hr::after {
	content: '§';
	display: inline-block;
	position: absolute;
	left: 50%;
	transform: translate(-50%, -50%) rotate(60deg);
	transform-origin: 50% 50%;
	padding: 0.5rem;
	color: var(--text-sub-accent);
	background-color: var(--background-primary);
}
```
