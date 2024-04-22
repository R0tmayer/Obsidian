### Binding data
Осуществляет одностороннее связывание. Меняем input - data не меняется. Меняем data - input меняется.
Иногда используется вместе с обработчиками, например `v-on:click="myFuntion"`
Сокращенно можно писать так `v-bind:count or :count`

Зачастую используется чтобы передать пропсы в дочерний компонент:
```js  
// Vue3
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

### Binding class

```js
   <body>
      <div id="app">
         <div class="static" :class="{active: isActive, 'text-danger': hasError}">test1</div>
      </div>
   </body>
   <script type="module">
      new Vue({
         el: '#app',
         data: {
            isActive: false,
            hasError: true,
         },
      });
   </script>
```

Манипулируя переменными `isActive` или `hasError` - будем появляться\удаляться `active`, `text-danger`

![[Pasted image 20240423094041.png]]

Или с помощью [[Options#^065cfa]] 