### Глобальный компонент

Чтобы создать глобальный компонент, необходимо поместить его перед созданием экземпляра Vue
```js
<script type="text/javascript">
	Vue.component('my-component', {
	 template: '<div>Hello my global component!</div>',
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

### Локальный компонент

Такой компонент будет доступен только экземпляру Vue, который его зарегистрировал
```js
<script type="text/javascript">
	const Component = {
		template: '<div>Hello my local component!</div>'
	}

	new Vue({
	el: "#app",
	components: {'myComponent': Component}
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
