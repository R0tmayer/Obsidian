#### `v-if` 
Обычно используется в связке с `v-else`, причем эти директивы должны идти последовательно:
```html
<div v-if="showModal"></div>
<div v-else></div>
```

Если указать false, то весь div удалиться из DOM
Null will be cast to false
```js
<script setup>
import { ref } from 'vue';
const showModal = ref(false);
</script>
<template>
	<main>
		<div v-if="showModal">
			TEST
		</div>
		<button @click="showModal = true">show</button>
		<button @click="showModal = false">hide</button>
	</main>
</template>

/ false or null - удалиться весь div из DOM
```
Примеры использования: когда нужно отобразить что-то в зависимости от чего-то. 
1) Если США - то штат, иначе Провинция (Канада). 
2) Если не вошёл в систему - то кнопка "Войти", если залогиненнный - то кнопка "Выйти"
#### `v-show` 
Просто скрывает элемент из разметки
```js
<div v-show="true">
	TEST
</div>

/ По умолчанию добавляется `style=""`
/ false or null - `style="display: none;"`
/ true - `style=""`
```
#### `v-bind`
Осуществляет односторонее связываение. Меняем input - data не меняется. Меняем data - input меняется.
Иногда используется вместе с обработчиками, например `v-on:click="myFuntion"`
Сокращенно можно писать так `v-bind:count or :count`

Зачастую используется чтобы передать пропсы в дочерний компонент:
```js
<script setup>
	import Foo from './components/Foo.vue'
	import { ref } from 'vue'
	
	const count = ref(0)
</script>

<template>
	<Foo v-bind:count="count" />
	<Foo :count="count" />
</template>
```

#### `v-model`
Осуществляет двусторонее привязывание. Меняем input - меняется data. Меняем data - меняется input.
Под капотом выглядит так:
```html
<input 
	v-bind:value="message" 
	v-on:input="message = $event.target.value"
>
```