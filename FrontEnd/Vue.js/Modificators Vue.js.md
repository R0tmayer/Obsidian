#### `.lazy`
Позволяет модифицировать значение data при наступлении событий `change`. 
Флажки и переключатели - при щелчке
Текстовое поле - при потере фокуса
Например `<input v-model.lazy="order.firstName" class = "form-control" />` 