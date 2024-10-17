
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
