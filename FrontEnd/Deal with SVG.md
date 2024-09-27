В SVG есть viewbox и viewport

```html
<div>
	<svg ..... width="32" height="32" viewBox="0 0 32 32">
</div>
```

#### Viewbox

```css
viewBox="0 0 32 32"
         ↓ ↓ ↓  ↓
         x y w  h
```

- x – минимальная координата x
- y – минимальная координата y
- w – ширина в координатах пользователя/пикселях
- h – высота в координатах пользователя/пикселях
#### Viewport
Родительский элемент (div) является viewport-ом.
 Viewport – по сути это то, что мы видим.

Хороший гайд: https://www.8host.com/blog/kak-rabotaet-svg-atribut-viewbox/

