Install and run project (need installed npm 10.5.0 `npm -v`):
```bash
npm init vue@latest
cd VueCounterApp
npm install
npm run dev
```

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

При использовании `<script setup>` любые привязки верхнего уровня (в т.ч. переменные, объявления функций и импорты) объявленные внутри `<script setup>` будут доступны напрямую в шаблоне:

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
        // реактивность
        return this._value;
    }

    set value(newVal) {
        // реактивность
        this._value = newVal;
    }
}
```

