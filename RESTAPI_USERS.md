# Пользователи

Независимо от того работает ли клиент от имени пользователя или от имени сервиса, управление пользователями осуществляется в рамках кдиента в котором созданы учетные данные. 

Роли пользователей в клиенте: 0 - пользователь, 1 - менеджер, 2 - аккаунт менеджер.

API позволяет манипулировать пользователями в роли "пользователь".

* **Сервер** - api.storyclm.com
* **Поддерживаемы клиенты** - работающие от имени пользователя, работающие от имени сервиса. 


#### Create User

Создает пользователя и добавляет его в текущий клиент.
Пользователь создается в роли "User".
Поля "Username" и "Password" обязательны.

**Запрос:**

* **Method:** POST
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/users

**Тело запроса:**
``` json
{
  "Username": "test@test.com",
  "Email": "test@test.com",
  "Phone": "79190001095",
  "Name": "Владимир Титов",
  "Location": "Ставрополь",
  "BirthDate": "",
  "Gender": true,
  "password": "1234"
}
```
**Пример**: https://api.storyclm.com/v1/users

**Ответ:**

* **Content Type**: application/json; charset=utf-8
* **Тело ответа**:
``` json
{
  "id": "2f94a899-7059-4bac-beb1-a3708c8938f3",
  "password": "1234",
  "username": "test@test.com",
  "email": "test@test.com",
  "phone": "79190001095",
  "name": "Владимир Титов",
  "location": "Ставрополь",
  "birthDate": null,
  "gender": true
}
```
#### Update User

Редактирует пользователя.
Обновляются все поля объекта кроме "Username".
Объект обновляется целиком.
Поля "Id" обязательно.

**Запрос:**

* **Method:** PUT
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/users

**Тело запроса:**
``` json
{
  "id": "2f94a899-7059-4bac-beb1-a3708c8938f3",
  "Email": "test@testtest.com",
  "Phone": "79197900000",
  "Name": "Кирилл Титов",
  "Location": "Черкесск",
  "BirthDate": "",
  "Gender": false
}
```
**Пример**: https://api.storyclm.com/v1/users

**Ответ:**

* **Content Type**: application/json; charset=utf-8
* **Тело ответа**:
``` json
{
  "id": "2f94a899-7059-4bac-beb1-a3708c8938f3",
  "username": null,
  "email": "test@testtest.com",
  "phone": "79197900000",
  "name": "Кирилл Титов",
  "location": "Черкесск",
  "birthDate": null,
  "gender": false
}
```
#### Get Users

Получает список пользователей клиента.
Каждый объект списка состоит из идентификатора пользователя и идентификатор роли.

**Запрос:**

* **Method:** GET
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/users

**Пример**: https://api.storyclm.com/v1/users

**Ответ:**

* **Content Type**: application/json; charset=utf-8
* **Тело ответа**:
``` json
[
  {
    "id": "a4be8f4a-96c5-49b8-87c9-51b0de7c869b",
    "role": 2
  },
  {
    "id": "1f6f7f74-3407-4521-a19d-42fd0b85a8b9",
    "role": 0
  },
  {
    "id": "abf8bc0e-3f65-4e06-8f98-43986ede5dd3",
    "role": 1
  },
  {
    "id": "fe84233b-0f47-4a7e-9ad8-bec78f4b5857",
    "role": 0
  },
  {
    "id": "b1ae249b-22c4-4b0b-a9ec-66f0521a4715",
    "role": 0
  },
  {
    "id": "2f94a899-7059-4bac-beb1-a3708c8938f3",
    "role": 0
  }
]
```
#### Get User

Получает профиль пользователя по идентификатору.

**Запрос:**

* **Method:** GET
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/users/{userId:string}
* **URL параметры:**
  * **\{ userId:string }** - идентификатор пользователя;

**Пример**: https://api.storyclm.com/v1/users/2f94a899-7059-4bac-beb1-a3708c8938f3

**Ответ:**

* **Content Type**: application/json; charset=utf-8
* **Тело ответа**:
``` json
{
  "id": "2f94a899-7059-4bac-beb1-a3708c8938f3",
  "username": "test@test.com",
  "email": "test@testtest.com",
  "phone": "79197900000",
  "name": "Кирилл Титов",
  "location": "Черкесск",
  "birthDate": null,
  "gender": false
}
```
#### Password

Обновляет текущий пароль. Пароль должен быть не меньше четырех символов.

**Запрос:**

* **Method:** PUT
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/users/{userId:string}/password?password={password:string}
* **URL параметры:**
  * **\{ userId:string }** - идентификатор пользователя;
  * **\{ password:string }** - новый пароль;

**Пример**: https://api.storyclm.com/v1/users/73f329f8-50b4-414b-9b71-8f760b6dab8a/password?password=test

**Ответ:**

* **Тело ответа**:
``` json

```
#### Add user to group

Добавляет пользователя в группу текущего клиента.

**Запрос:**

* **Method:** PUT
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/users/{userId:string}/group/{groupId:int}
* **URL параметры:**
  * **\{ userId:string }** - идентификатор пользователя;
  * **\{ groupId:int }** - идентификатор группы;

**Пример**: https://api.storyclm.com/v1/users/2f94a899-7059-4bac-beb1-a3708c8938f3/group/57

**Ответ:**

* **Тело ответа**:
``` json

```
#### Remove user from group

Удаляет пользователя из группу текущего клиента.

**Запрос:**

* **Method:** DELETE
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/users/{userId:string}/group/{groupId:int}
* **URL параметры:**
  * **\{ userId:string }** - идентификатор пользователя;
  * **\{ groupId:int }** - идентификатор группы;

**Пример**: https://api.storyclm.com/v1/users/2f94a899-7059-4bac-beb1-a3708c8938f3/group/57

**Ответ:**

* **Тело ответа**:
``` json

```
#### Add user to presentation

Добавляет пользователя в презентацию текущего клиента.

**Запрос:**

* **Method:** PUT
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/users/{userId:string}/presentation/{presentationId:int}
* **URL параметры:**
  * **\{ userId:string }** - идентификатор пользователя;
  * **\{ presentationId:int }** - идентификатор презентации;

**Пример**: https://api.storyclm.com/v1/users/2f94a899-7059-4bac-beb1-a3708c8938f3/presentation/57

**Ответ:**

* **Тело ответа**:
``` json

```
#### Remove user from presentation

Удаляет пользователя из презентации текущего клиента.

**Запрос:**

* **Method:** DELETE
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/users/{userId:string}/presentation/{groupId:int}
* **URL параметры:**
  * **\{ userId:string }** - идентификатор пользователя;
  * **\{ presentationId:int }** - идентификатор презентации;

**Пример**: https://api.storyclm.com/v1/users/2f94a899-7059-4bac-beb1-a3708c8938f3/presentation/57

**Ответ:**

* **Тело ответа**:
``` json

```

#### Presentations

Возвращает список презентаций в которые пользователь добавлен.

**Запрос:**

* **Method:** DELETE
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/users/{userId:string}/presentations
* **URL параметры:**
  * **\{ userId:string }** - идентификатор пользователя;

**Пример**: https://api.storyclm.com/v1/users/2f94a899-7059-4bac-beb1-a3708c8938f3/presentations

**Ответ:**

* **Тело ответа**:
``` json
[
  {
    "id": 32,
    "name": "Как улучшить качество жизни при хрони\u00adческой обструк\u00adтивной болезни легких"
  }
]
```

#### Groups

Возвращает список групп в которые пользователь добавлен.

**Запрос:**

* **Method:** DELETE
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/users/{userId:string}/groups
* **URL параметры:**
  * **\{ userId:string }** - идентификатор пользователя;

**Пример**: https://api.storyclm.com/v1/users/2f94a899-7059-4bac-beb1-a3708c8938f3/groups

**Ответ:**

* **Тело ответа**:
``` json
[
  {
    "id": 57,
    "name": "Группа3"
  }
]
```
