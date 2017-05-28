
# [REST API](https://ru.wikipedia.org/wiki/REST)

## Аутентифкация и Авторизация

### Общая информация

Аутентифкация и авторизация на портале осуществляется по средствам двух протоколов: [OAuth 2](https://ru.wikipedia.org/wiki/OAuth)
и [OpenID Connect](https://ru.wikipedia.org/wiki/OpenID), работающих в тандеме.

[OAuth 2](https://ru.wikipedia.org/wiki/OAuth) — открытый протокол авторизации, который позволяет предоставить третьей стороне ограниченный доступ к защищенным ресурсам пользователя без необходимости передавать ей (третьей стороне) логин и пароль.

[OpenID Connect](https://ru.wikipedia.org/wiki/OpenID) - открытый стандарт децентрализованной системы аутентификации, предоставляющей пользователю возможность создать единую учётную запись для аутентификации на множестве не связанных друг с другом интернет-ресурсов, используя услуги третьих лиц.

Доступ к API StoryCLM предоставляется по [JWT токенам](https://jwt.io/introduction/). Токены выдает сервер - [auth.storyclm.com](https://auth.storyclm.com/).
На этом сервере можно получить конфигурацию OpenID Connect, выполнив запрос:

**Запрос:**

* **Method**: GET
* **URL**: https://auth.storyclm.com/.well-known/openid-configuration

**Ответ:**

```JSON
{
   "issuer":"https://auth.storyclm.com",
   "jwks_uri":"https://auth.storyclm.com/.well-known/openid-configuration/jwks",
   "authorization_endpoint":"https://auth.storyclm.com/connect/authorize",
   "token_endpoint":"https://auth.storyclm.com/connect/token",
   "userinfo_endpoint":"https://auth.storyclm.com/connect/userinfo",
   "end_session_endpoint":"https://auth.storyclm.com/connect/endsession",
   "check_session_iframe":"https://auth.storyclm.com/connect/checksession",
   "revocation_endpoint":"https://auth.storyclm.com/connect/revocation",
   "introspection_endpoint":"https://auth.storyclm.com/connect/introspect",
   "frontchannel_logout_supported":true,
   "frontchannel_logout_session_supported":true,
   "scopes_supported":[
      "api",
      "offline_access"
   ],
   "claims_supported":[

   ],
   "response_types_supported":[
      "code",
      "token",
      "id_token",
      "id_token token",
      "code id_token",
      "code token",
      "code id_token token"
   ],
   "response_modes_supported":[
      "form_post",
      "query",
      "fragment"
   ],
   "grant_types_supported":[
      "authorization_code",
      "client_credentials",
      "refresh_token",
      "implicit"
   ],
   "subject_types_supported":[
      "public"
   ],
   "id_token_signing_alg_values_supported":[
      "RS256"
   ],
   "token_endpoint_auth_methods_supported":[
      "client_secret_basic",
      "client_secret_post"
   ],
   "code_challenge_methods_supported":[
      "plain",
      "S256"
   ]
}
  ```
### Активация

Для того что бы получить доступ к REST API своего клиента нужно его активировать на панели администрирования.
Для этого в клиенте, к api которого нужно получить доступ, надо перейти в раздел "Интеграция".

![rest Image 1](./images/rest/1.png)

Панель доступа к API состоит из трех контролов:
* API - регулирует доступ к API.
* CLIENT ID - идентификатор клиента. Нужен для получения токена.
* KEY - ключ доступа к API. Нужен для получения токена.

![rest Image 1](./images/rest/3.png)

Контролл "API" нужно перевести в положение "ON".

![rest Image 1](./images/rest/2.png)

В этом режиме сервер начнет выдавать токены. Стоит отметить, что в режиме "OFF", сервер аутентификации просто перестает выдавать новые токины. 
Доступ к API по токенам, выданым раньше, будет предоставляться до истечения их срока действия. Так же при изменении режимов, поле "KEY" будет каждый раз меняться.
Необходимо это учитывать так как старый ключ доступа уже не будет работать.

### Получение токена

Что бы получить доступ к ресурсам API, нужно авторизоваться и получить токен.
В противном случае, без токена сервер будет отвечать сообщением с кодом 401 (Unauthorized).
Для того что бы получить токен нужно выполнить запрос:

**Запрос:**

* **Method:** POST
* **Content-Type:** multipart/form-data
* **URL**: https://auth.storyclm.com/connect/token

**Форма:**
``` 
grant_type=client_credentials&
client_id=client_20&
client_secret=b9daff3eb63a4c929bcdb774f82b48a892c57bee53834ec3bb8e741cd396393c
```

Где client_id это CLIENT ID:

![rest Image 4](./images/rest/4.png)

А client_secret это KEY:

![rest Image 5](./images/rest/5.png)

В случае успеха должен быть получен ответ типа:

**Ответ:**

* **Тело ответа**:
``` json
{
  "access_token": "eyJhbGciOiJSUzI1NiIsImtpZCI6ImJlMjcxZjEwYmVlZWQ5OTEyMDQyYWZhYzY1MzQ0MGVkIiwidHlwIjoiSldUIn0.eyJuYmYiOjE0ODk2NjIwNDAsImV4cCI6MTQ4OTY2NTY0MCwiaXNzIjoiaHR0cHM6Ly9hdXRoLnN0b3J5Y2xtLmNvbSIsImF1ZCI6WyJodHRwczovL2F1dGguc3RvcnljbG0uY29tL3Jlc291cmNlcyIsImFwaSJdLCJjbGllbnRfaWQiOiJjbGllbnRfMjAiLCJtYXN0ZXIiOiJmYWxzZSIsInNjb3BlIjpbImFwaSJdfQ.pkY_lT89YU232DcMdr5cu_zboqFRwfgLWzGQu-ujSTKwaICvRvIFOsyucy76_17a0ly4BgPwOuVP7U_DTqMnyxgr16MTI5w7SXi2qnhapP1KyRy1WGfcR1RbVnDHH7ysiuUpHfwI4-xDYwmc4M2gbtBu2dY-tNYXsifCvcVaUEhXPQ99uuKL_1M6iKw6B6fnBNYyljQmVb84qSPGZZ678UoehL9RjnLHUzvd8tvr-yD-uDhc4TBT0u6KY_usPxImKyHo_Ela8pUSJ--wi6Vg6uh2KNLZJwm3DNCJ4M4PeeABu8eaZ9saIocxPvxZXNLlG9g0aMiJi4SJJySLkCuAIg",
  "expires_in": 3600,
  "token_type": "Bearer"
}
```

Полученный объект содержит три поля:
* access_token - сам токен.
* expires_in - время жизни токена в секундах.
* token_type - тип токена.

Теперь в каждый запрос к сервису, в заголовок, нужно добавлять access_token в формате:
``` 
Authorization: Bearer eyJhbGciOiJSUzI1NiIsImtpZCI6ImJlMjcxZjEwYmVlZWQ5OTEyMDQ...
```
Следует отметить, что токен живет час. После чего от сервера будет приходить код 401 (Unauthorized).
Что бы избежать этого нужно получать новый токен до истечения срока действия текущего.


## Таблицы

**[Таблицы](TABLES.md)** - это реляционное хранилище данных.

[Таблицы](TABLES.md) позволяют презентациям и внешним приложениям хранить структурированные данные на сервере, согласно схеме.

#### Tables

Получает список таблиц, доступных пользователю, по идентификатору клиента.
Результат запроса - сущность таблица, которая содержит идентификатор таблицы, тип и схему.

**Запрос:**

* **Method**: GET
* **Accept**: application/json
* **URL**: https://api.storyclm.com/v1/tables/{clientid:int}/tables
* **URL параметры**:
  * **{ clientid:int }** - идентификатор клиента;

**Пример**: https://api.storyclm.com/v1/tables/1/tables

**Пример ответа:**

* **Content Type**: application/json; charset=utf-8
* **Тело ответа**:

```JSON
[
    {
      "id": 5,
      "name": "Contact",
      "schema": [
        {
          "k": "name",
          "t": "1"
        },
        {
          "k": "companyname",
          "t": "1"
        },
        {
          "k": "position",
          "t": "1"
        }
      ],
      "created": "2016-08-12T07:32:46.69"
    },
    {
      "id": 6,
      "name": "Profile",
      "schema": [
        {
          "k": "name",
          "t": "1"
        },
        {
          "k": "age",
          "t": "2"
        },
        {
          "k": "gender",
          "t": "4"
        },
        {
          "k": "rating",
          "t": "3"
        },
        {
          "k": "created",
          "t": "5"
        }
      ],
      "created": "2016-09-28T21:53:40.19"
    }
  ]

  ```

#### Insert

Добавляет объект в таблицу.
Объект должен соответствовать схеме таблицы.

**Запрос:**

* **Method:** POST
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/tables/{tableid:int}/insert
* **URL параметры:**
  * **{ tableid:int }** - идентификатор таблицы;

**Тело запроса:**
``` json
{
    "name": "Vladimir",
    "age": 22,
    "gender": true,
    "rating": 2.2,
    "created": "2016-11-08T20:09:03.293Z"
}
```

**Пример**: https://api.storyclm.com/v1/tables/6/insert

**Ответ:**

* **Content Type**: application/json; charset=utf-8
* **Тело ответа**:
``` json
{
    "name": "Vladimir",
    "age": 22,
    "gender": true,
    "rating": 2.2,
    "created": "2016-11-08T20:09:03.293Z",
    "_id": "582230dff3afce8b106ba438"
}
```


#### Insertmany

Добавляет коллекцию объектов с таблицу.
Каждый объект должен соответствовать схеме таблицы.

**Запрос:**

* **Method:** POST
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/tables/{tableid:int}/insertmany
* **URL параметры:**
  * **{ tableid:int }** - идентификатор таблицы;

**Тело запроса:**
``` json
[
    {
      "name": "Vladimir",
      "age": 22,
      "gender": true,
      "rating": 2.2,
      "created": "2016-11-08T20:09:03.963Z",
      "_id": "582230e0f3afce8b106ba43a"
    },
    {
      "name": "Vladimir",
      "age": 22,
      "gender": true,
      "rating": 2.2,
      "created": "2016-11-08T20:09:03.963Z",
      "_id": "582230e0f3afce8b106ba43b"
    },
    {
      "name": "Vladimir",
      "age": 22,
      "gender": true,
      "rating": 2.2,
      "created": "2016-11-08T20:09:03.963Z",
      "_id": "582230e0f3afce8b106ba43c"
    }
]
  ```

**Пример**: https://api.storyclm.com/api/v1/tables/6/insertmany

**Пример ответа**

* **Content Type:** application/json; charset=utf-8
* **Тело ответа:**
``` json
[
    {
      "name": "Vladimir",
      "age": 22,
      "gender": true,
      "rating": 2.2,
      "created": "2016-11-08T20:09:03.963Z"
    },
    {
      "name": "Vladimir",
      "age": 22,
      "gender": true,
      "rating": 2.2,
      "created": "2016-11-08T20:09:03.963Z"
    },
    {
      "name": "Vladimir",
      "age": 22,
      "gender": true,
      "rating": 2.2,
      "created": "2016-11-08T20:09:03.963Z"
    }
]
```

#### Update

Перезаписывает объект.
Идентификатор объектом остается неизменным.

**Запрос:**

* **Method:** PUT
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/tables/{tableid:int}/update
* **URL параметры:**
  * **{ tableid:int }** - идентификатор таблицы;

**Тело запроса:**
``` json
{
    "name": "Anna",
    "age": 33,
    "gender": false,
    "rating": 3.3,
    "created": "2016-11-08T20:09:04.592Z",
    "_id": "582230dff3afce8b106ba438"
}
```

**Пример:** https://api.storyclm.com/api/v1/tables/6/update

**Пример ответа:**

* **Content Type:** application/json; charset=utf-8
* **Тело ответа:**
``` json
{
    "name": "Anna",
    "age": 33,
    "gender": false,
    "rating": 3.3,
    "created": "2016-11-08T20:09:04.592Z",
    "_id": "582230dff3afce8b106ba438"
}
```

#### Updatemany

Перезаписывает группу объектов.
Идентификатор объекта остатеся неизменным.

**Запрос:**

* **Method:** PUT
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/tables/{tableid:int}/updatemany
* **URL параметры:**
  * **{ tableid:int }** - идентификатор таблицы

**Тело запроса:**
``` json
[
    {
      "name": "Anna",
      "age": 33,
      "gender": false,
      "rating": 3.3,
      "created": "2016-11-08T20:09:05.186Z",
      "_id": "582230e0f3afce8b106ba43a"
    },
    {
      "name": "Anna",
      "age": 33,
      "gender": false,
      "rating": 3.3,
      "created": "2016-11-08T20:09:05.186Z",
      "_id": "582230e0f3afce8b106ba43b"
    },
    {
      "name": "Anna",
      "age": 33,
      "gender": false,
      "rating": 3.3,
      "created": "2016-11-08T20:09:05.186Z",
      "_id": "582230e0f3afce8b106ba43c"
    }
]
```

**Пример**: https://api.storyclm.com/v1/tables/6/updatemany

**Пример ответа:**

* **Content Type:** application/json; charset=utf-8
* **Тело ответа:**
``` json
[
    {
      "name": "Anna",
      "age": 33,
      "gender": false,
      "rating": 3.3,
      "created": "2016-11-08T20:09:05.186Z",
      "_id": "582230e0f3afce8b106ba43a"
    },
    {
      "name": "Anna",
      "age": 33,
      "gender": false,
      "rating": 3.3,
      "created": "2016-11-08T20:09:05.186Z",
      "_id": "582230e0f3afce8b106ba43b"
    },
    {
      "name": "Anna",
      "age": 33,
      "gender": false,
      "rating": 3.3,
      "created": "2016-11-08T20:09:05.186Z",
      "_id": "582230e0f3afce8b106ba43c"
    }
]
```

#### Count

Получает количество объектов в таблице по запросу. Формат запроса - [TablesQuery](TABLES_QUERY.md). 
Если запрос отсутсвует то будет получено общее колличесво объектов в таблице.

**Запрос:**

* **Method:** GET
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/tables/{tableid:int}/count?query={query}
* **URL параметры:**
  * **{ tableid:int }** - идентификатор таблицы
  * **{ query:tablesquery }** - запрос в формате [TablesQuery](TABLES_QUERY.md). Необязательный параметр.

**Пример:** https://api.storyclm.com/v1/tables/6/count

**Пример:** https://api.storyclm.com/v1/tables/23/count?query=[Gender][eq][false]

**Пример ответа:**

* **Content Type:** application/json; charset=utf-8
* **Тело ответа:**
``` json
{
  "count": 4
}
```

#### LogCount

Получает количество записей в логе таблицы. Если указан параметр "date", то получает количество записей лога таблицы после указанной даты.

**Запрос:**

* **Method:** GET
* **Accept:** application/json
* **URL:**: https://api.storyclm.com/v1/tables/{tableid:int}/logcount?date={date}
* **URL параметры:**
  * **{ tableid:int }** - идентификатор таблицы
  * **{ date:unixdate }** - дата в формате Unix Date. Необязательный параметр.

**Пример**: https://api.storyclm.com/v1/tables/6/logcount

**Пример**: https://api.storyclm.com/v1/tables/23/logcount?date=1495461379

**Пример ответа:**

* **Content Type:** application/json; charset=utf-8
* **Тело ответа:**
``` json
{
  "count": 4
}
```
#### Find

Получает объекты таблицы по запросу.
Формат запроса - [TablesQuery](TABLES_QUERY.md).

**Запрос**

* **Method:** GET
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/tables/23/find?skip={skip}&take={take}&sort={sort}&sortfield={sortfield}&query={query}
* **URL параметры:**
  * **{ tableid:int }** - идентификатор таблицы
  * **{ sortfield:string }** - поле, по которому будет произведена сортировка. Необязательный параметр.
  * **{ sort:int }** - тип сортировки. Необязательный параметр. Используется вместе с параметром "sortfield".
  * **{ skip:int }** - количество записей, которые нужно пропустить. 
  * **{ take:int }** - количество записей, которые нужно выбрать.
  * **{ query:tablesquery }** - запрос в формате [TablesQuery](TABLES_QUERY.md). Необязательный параметр.

**Пример:** https://api.storyclm.com/v1/tables/23/find?skip=0&take=100&sort=1&sortfield=age&query=[Gender][eq][false]

**Пример:** https://api.storyclm.com/v1/tables/23/find?skip=0&take=100&sort=1&sortfield=age

**Пример:** https://api.storyclm.com/v1/tables/23/find?skip=0&take=100&sortfield=age

**Пример:** https://api.storyclm.com/v1/tables/23/find?skip=0&take=100

**Пример ответа:**

* **Content Type:** application/json; charset=utf-8
* **Тело ответа:**
``` json
[
    {
      "_id": "582230dff3afce8b106ba438",
      "name": "Anna",
      "age": 33,
      "gender": false,
      "rating": 3.3,
      "created": "2016-11-08T20:09:04.592Z"
    },
    {
      "_id": "582230e0f3afce8b106ba43a",
      "name": "Anna",
      "age": 33,
      "gender": false,
      "rating": 3.3,
      "created": "2016-11-08T20:09:05.186Z"
    },
    {
      "_id": "582230e0f3afce8b106ba43b",
      "name": "Anna",
      "age": 33,
      "gender": false,
      "rating": 3.3,
      "created": "2016-11-08T20:09:05.186Z"
    },
    {
      "_id": "582230e0f3afce8b106ba43c",
      "name": "Anna",
      "age": 33,
      "gender": false,
      "rating": 3.3,
      "created": "2016-11-08T20:09:05.186Z"
    }
]
```

#### FindByid

Получает объект по идентификатору в таблице.

**Запрос:**

* **Method:** GET
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/tables/{tableid:int}/findbyid/{id}
* **URL параметры:**
  * **{ tableid:int }** - идентификатор таблицы
  * **{ id:string }** - идентификатор записи в таблице 

**Пример**: https://api.storyclm.com/v1/tables/6/findbyid/582230dff3afce8b106ba438

**Пример ответа:**

* **Content Type:** application/json; charset=utf-8
* **Тело ответа:**
``` json
{
    "name": "Anna",
    "age": 33,
    "gender": false,
    "rating": 3.3,
    "created": "2016-11-08T20:09:04.592Z",
    "_id": "582230dff3afce8b106ba438"
}
```

#### FindByids

Получает коллекцию объектов по списку идентификаторов в таблице.

**Запрос:**

* **Method:** GET
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/tables/{tableid:int}/findbyids
* **URL параметры:**
  * **{ tableid:int }** - идентификатор таблицы

**Тело запроса:**
```
 ids=582230dff3afce8b106ba438&ids=582230e0f3afce8b106ba43a&ids=582230e0f3afce8b106ba43b&ids=582230e0f3afce8b106ba43c
```

**Пример:** https://api.storyclm.com/v1/tables/6/findbyids?ids=582230dff3afce8b106ba438&ids=582230e0f3afce8b106ba43a&ids=582230e0f3afce8b106ba43b&ids=582230e0f3afce8b106ba43c

**Пример ответа:**

* **Content Type:** application/json; charset=utf-8
* **Тело ответа:**
``` json
[
    {
      "name": "Anna",
      "age": 33,
      "gender": false,
      "rating": 3.3,
      "created": "2016-11-08T20:09:04.592Z",
      "_id": "582230dff3afce8b106ba438"
    },
    {
      "name": "Anna",
      "age": 33,
      "gender": false,
      "rating": 3.3,
      "created": "2016-11-08T20:09:05.186Z",
      "_id": "582230e0f3afce8b106ba43a"
    },
    {
      "name": "Anna",
      "age": 33,
      "gender": false,
      "rating": 3.3,
      "created": "2016-11-08T20:09:05.186Z",
      "_id": "582230e0f3afce8b106ba43b"
    },
    {
      "name": "Anna",
      "age": 33,
      "gender": false,
      "rating": 3.3,
      "created": "2016-11-08T20:09:05.186Z",
      "_id": "582230e0f3afce8b106ba43c"
    }
]
```

#### Log

Получает все записи лога таблицы после указанной даты постранично.

**Запрос:**

* **Method:** GET
* **Accept:** application/json
* **URL**: https://admin.storyclm.com/{tableid:int}/log?skip={skip}&take={take}date={date}
* **URL параметры:**
  * **{ tableid:int }** - идентификатор таблицы.
  * **{ skip:int }** - количество записей, которые нужно пропустить. 
  * **{ take:int }** - количество записей, которые нужно выбрать.
  * **{ date:unixdate }** - дата в формате Unix Date. Необязательный параметр.

**Пример:** https://api.storyclm.com/v1/tables/23/log?skip=0&take=900&date=1495461402

**Пример:** https://api.storyclm.com/v1/tables/23/log?skip=0&take=100

**Пример ответа:**

* **Content Type:** application/json; charset=utf-8
* **Тело ответа:**
``` json
[
    {
      "id": "582230dff3afce8b106ba439",
      "tableEntityid": "582230dff3afce8b106ba438",
      "created": "2016-11-08T20:09:03.839Z",
      "operationType": 0
    },
    {
      "id": "582230e0f3afce8b106ba43d",
      "tableEntityid": "582230e0f3afce8b106ba43a",
      "created": "2016-11-08T20:09:04.47Z",
      "operationType": 0
    },
    {
      "id": "582230e0f3afce8b106ba43e",
      "tableEntityid": "582230e0f3afce8b106ba43b",
      "created": "2016-11-08T20:09:04.47Z",
      "operationType": 0
    },
    {
      "id": "582230e0f3afce8b106ba43f",
      "tableEntityid": "582230e0f3afce8b106ba43c",
      "created": "2016-11-08T20:09:04.47Z",
      "operationType": 0
    },
    {
      "id": "582230e1f3afce8b106ba440",
      "tableEntityid": "582230dff3afce8b106ba438",
      "created": "2016-11-08T20:09:05.082Z",
      "operationType": 1
    },
    {
      "id": "582230e1f3afce8b106ba441",
      "tableEntityid": "582230e0f3afce8b106ba43a",
      "created": "2016-11-08T20:09:05.671Z",
      "operationType": 1
    },
    {
      "id": "582230e1f3afce8b106ba442",
      "tableEntityid": "582230e0f3afce8b106ba43b",
      "created": "2016-11-08T20:09:05.756Z",
      "operationType": 1
    },
    {
      "id": "582230e1f3afce8b106ba443",
      "tableEntityid": "582230e0f3afce8b106ba43c",
      "created": "2016-11-08T20:09:05.841Z",
      "operationType": 1
    },
    {
      "id": "582230eff3afce8b106ba444",
      "tableEntityid": "582230dff3afce8b106ba438",
      "created": "2016-11-08T20:09:19.56Z",
      "operationType": 2
    },
    {
      "id": "582230f0f3afce8b106ba445",
      "tableEntityid": "582230dff3afce8b106ba438",
      "created": "2016-11-08T20:09:20.179Z",
      "operationType": 2
    },
    {
      "id": "582230f0f3afce8b106ba446",
      "tableEntityid": "582230e0f3afce8b106ba43a",
      "created": "2016-11-08T20:09:20.179Z",
      "operationType": 2
    },
    {
      "id": "582230f0f3afce8b106ba447",
      "tableEntityid": "582230e0f3afce8b106ba43b",
      "created": "2016-11-08T20:09:20.179Z",
      "operationType": 2
    },
    {
      "id": "582230f0f3afce8b106ba448",
      "tableEntityid": "582230e0f3afce8b106ba43c",
      "created": "2016-11-08T20:09:20.179Z",
      "operationType": 2
    }
 ]
 ```
#### DeleteByid

Удалить запись в таблице по идентификатору.

**Запрос:**

* **Method:** DELETE
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/tables/{tableid:int}/delete/{id}
* **URL параметры:**
  * **{ tableid:int }** - идентификатор таблицы
  * **{ id:string }** - идентификатор записи в таблице 

**Пример**: https://api.storyclm.com/v1/tables/6/delete/582230dff3afce8b106ba438

**Ответ:**

* **Content Type:** application/json; charset=utf-8
* **Тело ответа:**
``` json
{
    "name": "Anna",
    "age": 33,
    "gender": false,
    "rating": 3.3,
    "created": "2016-11-08T20:09:04.592Z",
    "_id": "582230dff3afce8b106ba438"
}
```

#### DeleteMany

Удаляет объекты таблицы по списку идентификаторов.

**Запрос:**

* **Method:** DELETE
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/tables/{tableid:int}/deletemany
* **URL параметры:**
  * **{ tableid:int }** - идентификатор таблицы

**Тело запроса:**
```
 ids=582230dff3afce8b106ba438&ids=582230e0f3afce8b106ba43a&ids=582230e0f3afce8b106ba43b&ids=582230e0f3afce8b106ba43c
 ```

**Пример**: https://api.storyclm.com/v1/tables/6/deletemany?ids=582230dff3afce8b106ba438&ids=582230e0f3afce8b106ba43a&ids=582230e0f3afce8b106ba43b&ids=582230e0f3afce8b106ba43c

**Пример ответа:**

* **Content Type:** application/json; charset=utf-8
* **Тело ответа:**
``` json
[
    {
      "name": "Anna",
      "age": 33,
      "gender": false,
      "rating": 3.3,
      "created": "2016-11-08T20:09:04.592Z",
      "_id": "582230dff3afce8b106ba438"
    },
    {
      "name": "Anna",
      "age": 33,
      "gender": false,
      "rating": 3.3,
      "created": "2016-11-08T20:09:05.186Z",
      "_id": "582230e0f3afce8b106ba43a"
    },
    {
      "name": "Anna",
      "age": 33,
      "gender": false,
      "rating": 3.3,
      "created": "2016-11-08T20:09:05.186Z",
      "_id": "582230e0f3afce8b106ba43b"
    },
    {
      "name": "Anna",
      "age": 33,
      "gender": false,
      "rating": 3.3,
      "created": "2016-11-08T20:09:05.186Z",
      "_id": "582230e0f3afce8b106ba43c"
    }
]
```
#### Max

Возвращает максимальное значение для указанного поля.

**Запрос:**

* **Method:** GET
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/tables/23/max/{field}?query={query}
* **URL параметры:**
  * **{ tableid:int }** - идентификатор таблицы.
  * **{ field:any }** - название поля, по которому будет выполнена операция. Параметр должент соответсвовать схеме таблицы.
  * **{ query:tablesquery }** - запрос в формате [TablesQuery](TABLES_QUERY.md). Необязательный параметр.

**Пример**: https://api.storyclm.com/v1/tables/23/max/Age?query=[Gender][eq][false]

**Пример**: https://api.storyclm.com/v1/tables/23/max/Age

**Ответ:**

* **Content Type:** application/json; charset=utf-8
* **Тело ответа:**
``` json
{
  "result": 28
}
```
#### Min

Возвращает минимальное значение для указанного поля.

**Запрос:**

* **Method:** GET
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/tables/23/min/{field}?query={query}
* **URL параметры:**
  * **{ tableid:int }** - идентификатор таблицы.
  * **{ field:any }** - название поля, по которому будет выполнена операция. Параметр должент соответсвовать схеме таблицы.
  * **{ query:tablesquery }** - запрос в формате [TablesQuery](TABLES_QUERY.md). Необязательный параметр.

**Пример**: https://api.storyclm.com/v1/tables/23/min/Age?query=[Gender][eq][true]

**Пример**: https://api.storyclm.com/v1/tables/23/min/Age

**Ответ:**

* **Content Type:** application/json; charset=utf-8
* **Тело ответа:**
``` json
{
  "result": 1
}
```
#### Sum

Возвращает сумму всех значений для указанного поля. 
Актуально для полей типа: integer, double и boolean.

**Запрос:**

* **Method:** GET
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/tables/23/sum/{field}?query={query}
* **URL параметры:**
  * **{ tableid:int }** - идентификатор таблицы.
  * **{ field:any }** - название поля, по которому будет выполнена операция. Параметр должент соответсвовать схеме таблицы.
  * **{ query:tablesquery }** - запрос в формате [TablesQuery](TABLES_QUERY.md). Необязательный параметр.

**Пример**: https://api.storyclm.com/v1/tables/23/sum/Age?query=[Gender][eq][true]

**Пример**: https://api.storyclm.com/v1/tables/23/sum/Age

**Ответ:**

* **Content Type:** application/json; charset=utf-8
* **Тело ответа:**
``` json
{
  "result": 128
}
```
#### Avg

Возвращает среднее арифметическое группы значений для указанного поля. 
Актуально для полей типа: integer и double.

**Запрос:**

* **Method:** GET
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/tables/23/avg/{field}?query={query}
* **URL параметры:**
  * **{ tableid:int }** - идентификатор таблицы.
  * **{ field:any }** - название поля, по которому будет выполнена операция. Параметр должент соответсвовать схеме таблицы.
  * **{ query:tablesquery }** - запрос в формате [TablesQuery](TABLES_QUERY.md). Необязательный параметр.

**Пример**: https://api.storyclm.com/v1/tables/23/avg/Age?query=[Gender][eq][true]

**Пример**: https://api.storyclm.com/v1/tables/23/avg/Age

**Ответ:**

* **Content Type:** application/json; charset=utf-8
* **Тело ответа:**
``` json
{
  "result": 30
}
```
#### First

Получает первый объект из выборки. Если объект не найдет то сервер вернет статус код 204.

**Запрос:**

* **Method:** GET
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/tables/23/first?&sort={sort}&sortfield={sortfield}&query={query}
* **URL параметры:**
  * **{ tableid:int }** - идентификатор таблицы.
  * **{ sortfield:string }** - поле, по которому будет произведена сортировка. Необязательный параметр.
  * **{ sort:int }** - тип сортировки. Необязательный параметр. Используется вместе с параметром "sortfield".
  * **{ query:tablesquery }** - запрос в формате [TablesQuery](TABLES_QUERY.md). Необязательный параметр.

**Пример**: https://api.storyclm.com/v1/tables/23/first?&sort=1&sortfield=age&query=[Age][eq][33]

**Пример**: https://api.storyclm.com/v1/tables/23/first?&sort=1&sortfield=age

**Пример**: https://api.storyclm.com/v1/tables/23/first?&sortfield=age

**Пример**: https://api.storyclm.com/v1/tables/23/first

**Ответ:**

* **Content Type:** application/json; charset=utf-8
* **Тело ответа:**
``` json
{
  "Name": "Vladimir",
  "Age": 33,
  "Gender": true,
  "Rating": 2.2,
  "Created": "2017-05-27T10:56:22.032Z",
  "_id": "59295b6d5724531de07ae47e"
}
```
#### Last

Получает последний объект из выборки. Если объект не найдет то сервер вернет статус код 204.

**Запрос:**

* **Method:** GET
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/tables/23/last?&sort={sort}&sortfield={sortfield}&query={query}
* **URL параметры:**
  * **{ tableid:int }** - идентификатор таблицы.
  * **{ sortfield:string }** - поле, по которому будет произведена сортировка. Необязательный параметр.
  * **{ sort:int }** - тип сортировки. Необязательный параметр. Используется вместе с параметром "sortfield".
  * **{ query:tablesquery }** - запрос в формате [TablesQuery](TABLES_QUERY.md). Необязательный параметр.

**Пример**: https://api.storyclm.com/v1/tables/23/last?&sort=1&sortfield=age&query=[Age][eq][33]

**Пример**: https://api.storyclm.com/v1/tables/23/last?&sort=1&sortfield=age

**Пример**: https://api.storyclm.com/v1/tables/23/last?&sortfield=age

**Пример**: https://api.storyclm.com/v1/tables/23/last

**Ответ:**

* **Content Type:** application/json; charset=utf-8
* **Тело ответа:**
``` json
{
  "Name": "Vladimir",
  "Age": 33,
  "Gender": true,
  "Rating": 2.2,
  "Created": "2017-05-27T10:56:22.032Z",
  "_id": "59295b6d5724531de07ae47e"
}
```













