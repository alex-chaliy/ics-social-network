# REST API Документация (ICS Social Network)


## Сущности, по котрым можно получить данные:
	- Пользователь (User)
	- Пост (Post)
	- Вакансия (Vacancy)
	- Кафедра (Department)
	- Предмет (Subject)

### Entity Relationships
	Post - User --- many to one
	User - Vacancy --- one to many
	User - Department --- many to one
	Department - Subject --- one to many
	User - Subject --- many to many

### Роли пользователей: 
	- admin
	- moderator
	- user
	- невошедший - в поле role будет пустая строка
! Пользователь более низкокого ранга не может содавать пользователя более высокого ранга.
	Исключением является регистрация.


## Как проводить операции над данными по разным сущностям

### Пользователь (User)
#### Пример тела запроса со всеми возможными полями
```json
{
	"_id": "9132137b539c5a1f022015ee",
	"token": "37b539c5a1f9139132137b539c5a1022015ee1f022015ee2",
	"role": "admin",
	"verified": "false",
	"login": "user1",
	"password": "pass1",
	"name": "Борис",
	"secondName": "Григорьевич",
	"surName": "Довженко",
	"coverImg": "/uploads/img/users/user-1.png",
	"city": "Одесса",
	"contacts": {
		"skype": "b.dovjenko",
		"phone": "+380 (73) 134 1254",
		"email": "b.dovjenko@gmail.com"
	},
	"job": {
		"resume": {
			"link": "https://goo.gl/DOz5Z1",
			"title": "Resume. Boris Dovjenko"
		},
		"company": "Sigma",
		"position": "Javascript Developer",
		"skills": [
			"Node.js",
			"Javascript",
			"Express.js",
			"Angular.js"
		]
	},

	"teacherData": {
		"subject_ids": [
			"4a3a1d7b53eae5bb20205d2a"
			"5a3a1d7b531235bb2075ad7b"
		],
		"department_id": "8c3a17db53cc5abb0220153a",
	},
	"educations": [{
		"status": "student",
		"university": "Водный Университет",
		"institute": "Институт Кибернетики и Автоматизации",

		"department": "Название Кафедры",
		"department_id": "8c3a17db53cc5abb0220153a",

		"entryYear": "2014",
		"graduateYear": "2018"
	}],

	"token": "5a3a1d7b534a3a1d7b53eae5bb20205d2a1235bb2075ad7b",

	"registrationDate": "2016-11-01T22:13:36+02:00",

	"personalDatails": {
		"hobbies" : [ 
            "программирование", 
            "web разработка", 
            "рисование"
        ],
		"birthday": "1996-21-09T22:13:36+02:00"
	}
}
```
#### Операции чтения пользователей
- Получить данные одного пользователя: <br>
	выполнить GET запрос по адресу '/user/:id', где :id - это id пользователя

- Получить данные всех пользователей: <br>
	выполнить GET запрос по адресу '/users'

#### Операции изменения пользователей
- Изменить данные одного пользователя: <br>
	выполнить PUT запрос по адресу '/user/:id', где :id - это id пользователя <br>
	в запросе нужно указать тело запроса с данными в формате JSON, опираясь на "Пример тела запроса со всеми возможными полями" выше.

> доступ: `admin` или создатель данных пользователя

#### Операции создания пользователей
- Создать данные одного пользователя: <br>
	выполнить POST запрос по адресу '/user' <br>
	в запросе нужно указать тело запроса с данными в формате JSON, опираясь на "Пример тела запроса со всеми возможными полями" выше

#### Операции удаления пользователей
- Удалить данные одного пользователя: <br>
	выполнить DELETE запрос по адресу '/user/:id', где :id - это id пользователя

> доступ: `admin` или создатель данных пользователя


### Пост (Post)
#### Пример тела запроса со всеми возможными полями
```json
{
	"_id": "8132122015ee37b539c5a1f0",
	"token": "37b539c5a1f9139132137b539c5a1022015ee1f022015ee2",
	"creator_id": "9132137b539c5a1f022015ee",
	"creationDate": "2016-11-01T22:13:36+02:00",
	"language_id": "4534chfg",
	"title": "Відкриття 15-ї обласної науково-практичної конференції Одеського територіального відділення Малої академії наук",
	"coverImg": "http://ics.opu.ua/uploads/img/cover_56hk5gj.jpg",
	"tags": [
		"event",
		"ics"
	],
	"parts": [
		"Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
		"img=[image_title](http://ics.opu.ua/uploads/img/ghfghghfgh.jpg)",
		"link=[link_title](https://www.google.com)",
		"video=[video_title](https://www.youtube.com/watch?v=N4mEzFDjqtA)",
		"h1=Some First Level Header",
		"h2=Some Second Level Header",
		"h3=Some Third Level Header",
		"h4=Some Fourth Level Header",
		"h5=Some Fifth Level Header",
		"h6=Some Sixth Level Header"
	],
	"eventData": {
		"date": "2016-11-01T22:13:36+02:00",
		"place": "Одесса, ул. Генуезская, 12, 3-й этаж, офис 307а",
		"registrationLink": "https://googledocs"
	},
	"courseData": {
		"teachers": [
			"Ivan Shevchenko",
			"Miroslav Close"
		],
		"registrationLink": "https://googledocs"
	}
}
```
#### Операции создания постов
- Создать один пост: <br>
	выполнить POST запрос по адресу '/post' <br>
	в запросе нужно указать тело запроса с данными в формате JSON, опираясь на "Пример тела запроса со всеми возможными полями" выше

> доступ: `admin` или `moderator`

#### Операции чтения постов
- Получить один пост: <br>
	выполнить GET запрос по адресу '/post/:id', где :id - это id поста

- Получить все посты: <br>
	выполнить GET запрос по адресу '/posts'

#### Операции изменения постов
- Изменить один пост: <br>
	выполнить PUT запрос по адресу '/post/:id', где :id - это id поста <br>
	в запросе нужно указать тело запроса с данными в формате JSON, опираясь на "Пример тела запроса со всеми возможными полями" выше

> доступ: `admin` или `moderator`

#### Операции удаления постов
- Удалить один пост: <br>
	выполнить DELETE запрос по адресу '/post/:id', где :id - это id поста

> доступ: `admin` или `moderator`