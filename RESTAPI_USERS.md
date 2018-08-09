# Users

User management is carried out within the client in which user accounts were created. Roles of users in the client: 0 - user, 1 - manager, 2 - account manager. The API allows to manipulate users in the role of a "user". Server - api.storyclm.com.

* **Server** - api.storyclm.com.
* **Supported clients** - working on behalf of the user, working on behalf of the service. 

### Create User

Creates and adds a new user to the client. 
The user is assigned the role of "User". 
The "username" and "password" fields are mandatory. 

**Request:**

* **Method:** POST
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/users

**Response body:**
``` json
{
  "username": "test@test.com",
  "email": "test@test.com",
  "phone": "79190001095",
  "name": "Владимир Титов",
  "location": "Ставрополь",
  "birthDate": "",
  "gender": true,
  "password": "1234"
}
```
**Example:** https://api.storyclm.com/v1/users

**Response:**

* **Content Type**: application/json; charset=utf-8

**Response body:**
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
### Update User

Updates all the user profile fields except "Username". 
The object is updated entirely. 
The "id" field is mandatory.

**Request:**

* **Method:** PUT
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/users

**Response body :**
``` json
{
  "id": "2f94a899-7059-4bac-beb1-a3708c8938f3",
  "email": "test@testtest.com",
  "phone": "79197900000",
  "name": "Кирилл Титов",
  "location": "Черкесск",
  "birthDate": "",
  "gender": false
}
```
**Example:** https://api.storyclm.com/v1/users

**Response:**

* **Content Type**: application/json; charset=utf-8

**Response body:**
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
### Get Users

Gets a list of client users. 
Every object on the list consists of a user id, a username, and a role identifier.

**Request:**

* **Method:** GET
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/users

**Example:** https://api.storyclm.com/v1/users

**Response:**

* **Content Type**: application/json; charset=utf-8

**Response body:**
``` json
[
  {
    "id": "a4be8f4a-96c5-49b8-87c9-51b0de7c869b",
    "username": "eklesia@gmail.com",
    "role": 2
  },
  {
    "id": "1f6f7f74-3407-4521-a19d-42fd0b85a8b9",
    "username": "wtselofan@yandex.ru",
    "role": 0
  },
  {
    "id": "abf8bc0e-3f65-4e06-8f98-43986ede5dd3",
    "username": "tselkofan1@yandex.ru",
    "role": 1
  },
  {
    "id": "fe84233b-0f47-4a7e-9ad8-bec78f4b5857",
    "username": "test@mail.com",
    "role": 0
  },
  {
    "id": "b1ae249b-22c4-4b0b-a9ec-66f0521a4715",
    "username": "rst-k169@ya.ru",
    "role": 0
  },
  {
    "id": "8b23dfb9-cfd7-4521-95a8-c9649ecf2d27",
    "username": "test@test.com",
    "role": 0
  }
]
```
### Get User

Gets the user profile via ID.

**Request:**

* **Method:** GET
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/users/{userId:string}
* **URL parameters:**
  * **\{ userId:string }** - user ID;

**Example:** https://api.storyclm.com/v1/users/2f94a899-7059-4bac-beb1-a3708c8938f3

**Response:**

* **Content Type**: application/json; charset=utf-8

**Response body:**
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
### Password

Updates the current password. The password must contain at least four characters.

**Request:**

* **Method:** PUT
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/users/{userId:string}/password
* **URL parameters:**
  * **\{ userId:string }** - user ID;

**Response body :**
``` json
{
  "password": "test",
}
```
**Example:** https://api.storyclm.com/v1/users/73f329f8-50b4-414b-9b71-8f760b6dab8a/password

**Response:**

**Response body:**
``` json

```
### Exists

Checks if the user exists in the system. 
Returns the profile if the user is registered and added to the client.

**Request:**

* **Method:** GET
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/users/exists?username={username}
* **URL parameters:**
  * **\{ username:string }** - username;

**Example:** https://api.storyclm.com/v1/users/exists?username=test@test.com

**Response:**

**Response body:**
``` json
{
  "id": "8b23dfb9-cfd7-4521-95a8-c9649ecf2d27",
  "username": "test@test.com",
  "email": "test@test.com",
  "phone": "79190001095",
  "name": "Владимир Титов",
  "location": "Ставрополь",
  "birthDate": null,
  "gender": true
}
```
### Add user to group

Добавляет пользователя в группу.

**Request:**

* **Method:** PUT
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/users/{userId:string}/group/{groupId:int}
* **URL parameters:**
  * **\{ userId:string }** - user ID;
  * **\{ groupId:int }** - идентификатор группы;

**Example:** https://api.storyclm.com/v1/users/2f94a899-7059-4bac-beb1-a3708c8938f3/group/57

**Response:**

**Response body:**
``` json

```
### Remove user from group

Adds the user to the group.

**Request:**

* **Method:** DELETE
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/users/{userId:string}/group/{groupId:int}
* **URL parameters:**
  * **\{ userId:string }** - user ID;
  * **\{ groupId:int }** - group ID;

**Example:** https://api.storyclm.com/v1/users/2f94a899-7059-4bac-beb1-a3708c8938f3/group/57

**Response:**

**Response body:**
``` json

```
### Add user to presentation

Gives the user access to the presentation. 

**Request:**

* **Method:** PUT
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/users/{userId:string}/presentation/{presentationId:int}
* **URL parameters:**
  * **\{ userId:string }** - user ID;
  * **\{ presentationId:int }** - presentation ID;

**Example:** https://api.storyclm.com/v1/users/2f94a899-7059-4bac-beb1-a3708c8938f3/presentation/57

**Response:**

**Response body:**
``` json

```
### Add User To Presentations

Gives the user access to a group of presentations. The group of presentation has to be a collection of presentation identifiers. Presentations must belong to the current client and be active. The user can not be "Accent Manager" and "Project Manager". Giving the user access to the group of presentations means that only the presentations which meet the said conditions will be accessible. As a result, a list of all presentations to which the user has access will be displayed. The list allows to check which presentations the user has been granted access to

**Request:**

* **Method**: POST
* **Accept**: application/json
* **URL**: https://api.storyclm.com/v1/users/{userId}/presentations
* **URL параметры**:
  * **\{ userId:int }** - user ID;

**Response body :**
``` json
[
	33,
	26,
	24
]
```
**Example:** https://api.storyclm.com/v1/users/b1ae249b-22c4-4b0b-a9ec-66f0521a4715/presentations

**Пример ответа:**

* **Content Type**: application/json; charset=utf-8
**Response body:**

```JSON
[
  24,
  26,
  33
]
```
### Remove user from presentation

Denies the user access to the presentation.

**Request:**

* **Method:** DELETE
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/users/{userId:string}/presentation/{presentationId:int}
* **URL parameters:**
  * **\{ userId:string }** - user ID;
  * **\{ presentationId:int }** - presentation ID;

**Example:** https://api.storyclm.com/v1/users/2f94a899-7059-4bac-beb1-a3708c8938f3/presentation/57

**Response:**

**Response body:**
``` json

```
### Remove User From Presentations

Denies the user access to the group of presentations. The group of presentation has to be a collection of presentation identifiers. Presentations must belong to the current client and be active. The user can not be "Accent Manager" and "Project Manager". As a result, a list of all presentations to which the user has access will be returned.

**Request:**

* **Method**: DELETE
* **Accept**: application/json
* **URL**: https://api.storyclm.com/v1/users/{userId}/presentations?ids={presentationId}&ids={presentationId}&ids={presentationId}
* **URL параметры**:
  * **\{ presentationId:int }** - presentation ID;
  * **\{ userId:string }** - user ID;

**Example:** https://api.storyclm.com/v1/users/b1ae249b-22c4-4b0b-a9ec-66f0521a4715/presentations?ids=24&ids=26&ids=33

* **Content Type**: application/json; charset=utf-8

**Response body:**

```JSON
[]
```
### Synchronize Presentations For User

Grants the user access to the presentation group. The presentation group should be a collection of presentation identifiers. Regardless of which presentations the user had before the synchronization, after synchronization he will have access only to those presentations that are in the list. Presentations should belong to the current client and be active. The user should not belong to the roles "Accent Manager" and "Project Manager". As a result, a list of all presentations to which the user has access will be returned.

**Request:**

* **Method**: PUT
* **Accept**: application/json
* **URL**: https://api.storyclm.com/v1/users/{userId}/presentations
* **URL параметры**:
  * **\{ presentationId:int }** - presentation ID;

**Response body :**
``` json
[
  24,
  33
]
```
**Example:** https://api.storyclm.com/v1/users/b1ae249b-22c4-4b0b-a9ec-66f0521a4715/presentations

* **Content Type**: application/json; charset=utf-8

**Response body:**
```JSON
[
  24,
  33
]
```
### Presentations

Returns the list of presentations the user has access to.

**Request:**

* **Method:** GET
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/users/{userId:string}/presentations
* **URL parameters:**
  * **\{ userId:string }** - user ID;

**Example:** https://api.storyclm.com/v1/users/2f94a899-7059-4bac-beb1-a3708c8938f3/presentations

**Response:**

**Response body:**
``` json
[
  {
    "id": 32,
    "name": "Как улучшить качество жизни при хрони\u00adческой обструк\u00adтивной болезни легких"
  }
]
```

### Groups

Returns the list of groups of which the user is a member.

**Request:**

* **Method:** GET
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/users/{userId:string}/groups
* **URL parameters:**
  * **\{ userId:string }** - user ID;

**Example:** https://api.storyclm.com/v1/users/2f94a899-7059-4bac-beb1-a3708c8938f3/groups

**Response:**

**Response body:**
``` json
[
  {
    "id": 57,
    "name": "Группа3"
  }
]
```
