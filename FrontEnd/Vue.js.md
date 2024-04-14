Install and run project (need installed npm 10.5.0 `npm -v`):
```bash
npm init vue@latest
cd VueCounterApp
npm install // каждый раз при создании проекта
npm run dev
```

### Что такое script setup?
Чтобы код работал нужно добавить атрибут `setup` в секцию `<script>`:
```js
<script setup>
import { ref } from 'vue';
const count = ref(5);
console.log(count);

const plus = () => {
   count.value++;
};

const minus = () => {
   count.value--;
};
</script>

<template>
   <main>
      <div>
         <h4>The current count is...</h4>
         <h1>
            {{ count }}
         </h1>
         <button @click="minus()">-</button>
         <button @click="plus()">+</button>
      </div>
   </main>
</template>
```
Код внутри компилируется как содержимое функции компонента `setup()`. Это означает, что в отличие от обычного `<script>`, который выполняется только один раз при первом импорте компонента, код внутри `<script setup>` будет **выполняться каждый раз при создании экземпляра компонента**.

При использовании `<script setup>` любые привязки верхнего уровня (в т.ч. переменные, объявления функций и импорты) объявленные внутри `<script setup>` будут доступны напрямую в template

Во Vue.js 2 использовался такой подход:

```js
< script >
    export default {
        data() {
            return {
                count: 0,
            };
        },
        methods: {
            plus() {
                this.count++;
            },
            minus() {
                this.count--;
            },
        },
    }; <
/script>
```
### Что такое пакет vue?

```js
import { ref } from 'vue';
```

`'vue'` - это официальный пакет Vue.js. Предоставляет функционал для создания экземпляров Vue, определения компонентов, управления жизненным циклом приложения и многих других вещей.

Когда вы устанавливаете Vue.js через пакетный менеджер, например, npm или yarn, вы устанавливаете именно этот пакет 'vue'.

Например, вы можете установить Vue.js с помощью npm следующей командой:

`npm install vue`

### Что такое ref из пакета vue?

`ref` - создает реактивную ссылку на значение
```js
function ref(value) {
    return new RefImpl(value);
}

class RefImpl {
    constructor(value) {
        this._value = value;
    }

    get value() {
        / реактивность
        return this._value;
    }

    set value(newVal) {
        / реактивность
        this._value = newVal;
    }
}
```

Когда вы вызываете `ref(5)`, вы создаете реактивную ссылку на число 5.

Когда значение ссылки меняется, все зависимые от него элементы интерфейса автоматически обновляются. Это обеспечивает реактивность в Vue.js.

```js
import { ref } from 'vue'; 
/ Создаётся реактивная ссылка на значение 5, сохраняя ее в константе `count`.
const count = ref(5);
```

### Директивы

#### `v-if` 
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

#### `v-show` 
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