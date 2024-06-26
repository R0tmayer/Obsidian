#### `v-if v-else-if v-else` 
Удаляется из DOM
Подходит в ситуациях, когда содержимое показывается/отрисовывается большую часть времени или когда видимость элемента меняется несколько раз на протяжении жизненного цикла страницы.

Директива v-else всегда должна идти сразу за `v-if` или `v-else-if`. Если нарушить правило, то директивы не будут распознаны.
```html
<div v-if="count === 0">All is out!</div>
<div v-else-if="count < 5">Only {{count}} left!</div>
<div v-else>Buy now!</div>
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
Всегда присутствует в DOM.
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

[[Bindind directive]]
#### `v-model`
Осуществляет двустороннее привязывание. Меняем input - меняется data. Меняем data - меняется input.

Под капотом выглядит так:
```html
<input 
	v-bind:value="message" 
	v-on:input="message = $event.target.value"
>
```
Может быть применён модификатор [[Modificators Vue.js#`.lazy`]]
#### `v-for`
Перебор массива без ключа
```js
<div v-for="state in states">{{state}}</div>

states: {
'Alabama',
'Arizona',
'California',
'Nevada',
},
```

Перебор массива с ключом
```js
<div v-for="(state, key) in states" v-bind:value="state">{{key}}</div>

states: {
AL: 'Alabama',
AR: 'Arizona',
CA: 'California',
NV: 'Nevada',
},
```
Особенность в том, что по логике`v-for` (цикл) должен быть снаружи компонента. То есть как бы отрисовываем компонент в цикле. Но по факту `v-for` внутри компонента. Немного ломаем понимание, но нужн запомнить