# модуль defineUserRole - документация

## Описание
	Модуль возвращает функцию. Эта функция определит роль пользователя,
	затем выполнит действие, если передать callback.

## Параметры
- token - ключ авторизованного пользователя;
- UserEntity - ссылка на объект;
    этот объект является mongoose-моделью и содержит
    методы mongoose'а для проведения операций над пользователем в MongoDB,
    например, операция чтения;
- callback - анонимная функция, внутри которой можно выполнить действие
	после того, как определилась роль пользователя.

## Пример использоваия
```javascript
const defineUserRole = require('./defineUserRole');

/* ! Для начала создайте mongoose-модель User */
let params = {
	token: '137ba15ee22037b539c5a1f01321539c59',
	UserEntity: User
}
defineUserRole(params, (role, user) => {
	if(role === 'admin' || user._id === userId) {
		// do something
	}
});
```

