
Осуществляет одностороннее связывание. Меняем input - data не меняется. Меняем data - input меняется.
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
