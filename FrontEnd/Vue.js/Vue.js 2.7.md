Как оказалось требуется Vite (или Nuxtjs или Webpack)

Создать проект можно так (need installed npm 10.5.0 `npm -v`):
```bash
npm create vue@^2
cd vue-project
npm install
npm run dev
```

Далее нам интересны файлы: 
- Index.html
- main.js
- App.vue

При открытии Index.html тянется файл main.js, который импортирует сам `Vue` и стартовый компонент `App` (можно назвать как угодно, это твой компонент, не системный как `Vue`). Далее создаём объект `Vue` , указываем что отрисовыввем `App` и монтируем этот объект в DOM к `div app`

```js
import Vue from 'vue';
import App from './App.vue';
import '../node_modules/bootstrap/dist/css/bootstrap.css';

new Vue({
   render: (h) => h(App),
}).$mount('#app');
```