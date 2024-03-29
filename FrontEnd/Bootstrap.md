Идея строится на манипуляции 3 компонентов: 
- `container`
- `row`
- `column`

### Container

Это родительский div для всей страницы. Автоматом добавляет margin по бокам. 

`.container` - по умолчанию подойдет для большинства случаев

> [!note]- Размерная сетка
> 
|                    | Extra small<br><br><576px | Small<br><br>≥576px | Medium<br><br>≥768px | Large<br><br>≥992px | X-Large<br><br>≥1200px | XX-Large<br><br>≥1400px |
| ------------------ | ------------------------- | ------------------- | -------------------- | ------------------- | ---------------------- | ----------------------- |
| `.container`       | 100%                      | 540px               | 720px                | 960px               | 1140px                 | 1320px                  |
| `.container-sm`    | 100%                      | 540px               | 720px                | 960px               | 1140px                 | 1320px                  |
| `.container-md`    | 100%                      | 100%                | 720px                | 960px               | 1140px                 | 1320px                  |
| `.container-lg`    | 100%                      | 100%                | 100%                 | 960px               | 1140px                 | 1320px                  |
| `.container-xl`    | 100%                      | 100%                | 100%                 | 100%                | 1140px                 | 1320px                  |
| `.container-xxl`   | 100%                      | 100%                | 100%                 | 100%                | 100%                   | 1320px                  |
| `.container-fluid` | 100%                      | 100%                | 100%                 | 100%                | 100%                   | 100%                    |

### Row

Теперь нет смысла писать `display: flexbox`. Достаточно написать 
`div class="row"` и `container` поделится на 12 равных колонок (под капотом применяется flexbox). 

> [!NOTE]- Колонки разной ширины
> ```html
> <div class="container text-center">
>   <div class="row">
>     <div class="col-1">
>       Column
>     </div>
>     <div class="col-2">
>       Column
>     </div>
>     <div class="col-3">
>       Column
>     </div>
> 	<div class="col-4">
>       Column
>     </div>
>   </div>
> </div>
> ```
> ![[bs_col_1.png]]

`<div class="col-auto>TEST</div>` - автоширина по длине текста 


> [!NOTE]- Ширина колонки под конкретный лейаут
> 
> ```html
> <div class="col-4 col-sm-5 col-md-6 col-lg-7 col-xl-8">
>   Column
> </div>
> ```
> ![[bs_col_2.png]]
> ![[bs_col-sm-5.png]]
> ![[bs_col-md-6.png]]
> ![[bs_col-xl-8.png]]


> [!NOTE]- Сдвиг колонок
> ```html
> <div class="container">
> 	<div class="row" style="margin-top: 10px;">
> 		<div class="col offset-2">
> 		</div>
> 		<div class="col">
> 		</div>
> 		<div class="col offset-3">
> 		</div>
> 		<div class="col">
> 		</div>
> 	</div>
> </div>
> ```
> ![[bs_offset-2.png]]

`gy-5` - gap по Y
`gx-5` - gap по X

> [!NOTE]- Вложенные колонки
> ```html
> <div class="container">
> 	<div class="row" style="margin-top: 10px;">
> 		<div class="col">
> 			<div class="row gx-0">
> 				<div class="col">
> 				</div>
> 				<div class="col">
> 				</div>
> 			</div>
> 		</div>
> 		<div class="col">
> 		</div>
> 		<div class="col">
> 		</div>
> 		<div class="col">
> 		</div>
> 	</div>
> </div>
> ```
> ![[bs_col-nested.png]]


### Tables

```html
<table class="table table-info">
	<thead>
		<tr>
			<td>Name</td>
			<td>Price</td>
		</td>
	</thead>
	<tbdoy>
		<tr>
			<td>Horizon</td>
			<td>49.99</td>
		</tr>
		<tr>
			<td>God of War</td>
			<td>39.99</td>
		</tr>
		<tr>
			<td>FIFA 2023</td>
			<td>29.99</td>
		</tr>
```

`table` - bootstrap таблица

```html
<table class="table table-info"></table> // покрасить таблицу
```

```html
<tr class="table-warning"></tr> // покрасить строку
```

```html
<td class="table-info">Horizon</td> // покрасить ячейку
```

```html
<table class="table table-hover"></table> // активируется при наведении
```