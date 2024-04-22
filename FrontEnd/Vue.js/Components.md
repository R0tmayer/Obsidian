### Глобальный компонент

Чтобы создать глобальный компонент, необходимо поместить его перед созданием экземпляра Vue
```js
<script type="text/javascript">
	Vue.component('my-component', {
	 template: '<div>Hello my component!</div>',
	});

	new Vue({
	el: "#app"
	}),
</script>

```

Использование компонента:
```html
<body>
	<div id="app">
		<my-component></my-component>
	</div>
</body>
```