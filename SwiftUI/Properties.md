
#### Stored property
Это обычные поля let и const в структуре или классе

#### Computed property
Это обычное свойство с get и set

Не хранится в памяти

![[Pasted image 20241017205713.png]]
#### Observer property
Необычное свойство, имеющее willSet и didSet

Как я понял, хранится в памяти

![[Pasted image 20241017205514.png]]

#### Property Wrapper

Некий атрибут, который вешается на структуру, класс или енам.

![[Pasted image 20241017211221.png]]

Далее эту структуру можно использовать как непосредственно propertyWrapper для любого поля:

![[Pasted image 20241017211305.png]]

Аналог на computed свойствах:
![[Pasted image 20241017211343.png]]

#### @State

**!!! State прекрасно подходит для хранения локального состояния внутри одного представления**

`@State private var isOn: Bool = false`

- Создаёт состояние поля на уровне вью.
- При изменении состояние re-рендерятся компоненты, использующие это состояние.
- Состояние можно изменить только на уровне вью:
	- `Button("AnyText"){ self.isOn = true }`
	- `Toggle(isOn: $isOn)`
- Можно передать для чтения в дочерний вью `ChildView(anyBool: isOn)`
- При попытке прокинуть это свойство внутрь другого вью, необходимо указать `$`, значит скастовать в `Binding<T>`

> [!NOTE]
> Когда вы используете **$** перед переменной, вы получаете Binding к ее значению, что позволяет вам читать и изменять это значение из других представлений или внутри замыканий.
> 
> `@Binding` трансформирует тип в `Binding<T>`
> 
> Получается у дочернего объекта поле `Binding<T>`, значит и при вызове дочернего надо тоже передать `Binding<T>`
> 

^18cf94

А что, я не могу изменять поле без этого врапера? Можно, наложив mutable, но структура все равно не позволит это сделать. Поэтому `@State` - это некое читерство чтобы управлять состоянием поля.

![[Pasted image 20241017215811.png]]

#### @Binding

**!!! Binding идеально подходит для передачи данных между различными представлениями.**

Что если нужно изменить состояние поля в дочернем вью? Тогда `@State` уже не поможет.

В дочернем вью указывается `@Binding var isOn: Bool`. Это значит что входной параметр передаётся по ссылке и его можно изменять, даже если передаётся `@State` из родителя.

- Поле не может быть `private`, иначе при вызове вью нельзя к нему обратиться

Подробнее про `@Binding`: [[#^18cf94]]

![[Pasted image 20241017222435.png]]

#### @Observable

^2d60d5

Реализует паттерн Observer (когда подписчики трекают объект и реагируют если в этом объекте что-то поменялось)

- Вешается на обычную модель (класс) чтобы изменять значение инстанса в дочерних вью
- Применяется к классам, структурам, енамам.
- Работает в связке с `@Bindable` [[#^ffabf0]]

![[Pasted image 20241018135757.png]]

> [!NOTE]
> Ранее, для реализации этой фичи использовались `ObservableObject`, `@Published` и `@StateObject`

![[Pasted image 20241020094835.png]]
#### @Bindable

^ffabf0

Работает как `@Binding`, только биндит `@Observable` свойство [[#^2d60d5]]