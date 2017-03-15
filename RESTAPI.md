# REST API

## Таблицы

**[Таблицы](TABLES.md)** - это релиационное хранилище данных.

[Таблицы](TABLES.md) позволяют презентациям и внешним приложениям хранить структурированные данные на сервере, согласно схеме.



### API requests

Название                                                               |      HTTP Verb     |             Описание
-----------------------------------------------------------------------|--------------------|----------------------------------------------------------------
tables/{tableid:int}/tables                                            |        GET         |    Получает список таблиц доаступных пользователю
tables/{tableid:int}/insert                                            |        POST        |    Добавляет сущность в таблицу
tables/{tableid:int}/insertmany                                        |        POST        |    Добавляет коллекцию сущностей с таблицу
tables/{tableid:int}/update                                            |        PUT         |    Перезаписывает запись целиком
tables/{tableid:int}/updatemany                                        |        PUT         |    Перезаписывает группу записей
tables/{tableid:int}/count                                             |        GET         |    Получает количество записей в таблице
tables/{tableid:int}/countbyquery/{query:tablesquery}                  |        GET         |    Получает количество записей в таблице по запросу
tables/{tableid:int}/logcount                                          |        GET         |    Получает количество записей в логе таблицы
tables/{tableid:int}/logcountbydate/{date:unixdate}                    |        GET         |    Получает количество записей лога таблицы после указанной даты
tables/{tableid:int}/log/{skip:int}/{take:int}                         |        GET         |    Получает все записи лога таблицы
tables/{tableid:int}/logbydate/{skip:int}/{take:int}/{date:unixdate}   |        GET         |    Получает все записи лога таблицы после указанной даты
tables/{tableid:int}/findall/{skip:int}/{take:int}                     |        GET         |    Получает постранично все данные таблицы
tables/{tableid:int}/find...                                           |        GET         |    Получает постранично данные по запросу
tables/{tableid:int}/findbyid/{id:int}                                 |        GET         |    Получает запись по идентификатору в таблице
tables/{tableid:int}/findbyids                                         |        GET         |    Получает коллекцию записей по списку идентификаторов в таблице
tables/{tableid:int}/delete/{id:int}                                   |        DELETE      |    Удалить запись в таблице по идентификатору
tables/{tableid:int}/deletemany                                        |        DELETE      |    Удаляет записи таблицы по списку идентификаторов

#### Tables

Получает список таблиц доступных пользователю по идентификатору клиента.
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

Добавляет сущность в таблицу.
Сущность должна соответствовать схеме таблицы.

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

Добавляет коллекцию сущностей с таблицу.
Каждая сущность должна соответствовать схеме таблицы.

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

Перезаписывает запись целиком.
Идентификатор записи остается неизменным.

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

Перезаписывает группу записей.
Идентификатор записи остатеся неизменным.

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

Получает количество записей в таблице.

**Запрос:**

* **Method:** GET
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/tables/{tableid:int}/count
* **URL параметры:**
  * **{ tableid:int }** - идентификатор таблицы

**Пример:** https://api.storyclm.com/v1/tables/6/count

**Пример ответа:**

* **Content Type:** application/json; charset=utf-8
* **Тело ответа:**
``` json
{
  "count": 4
}
```

#### CountByQuery

Получает количество записей в таблице по запросу.
Формат запроса - [TablesQuery](TABLESQUERY.md).

**Запрос:**

* **Method:** GET
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/tables/{tableid:int}/countbyquery/{query}
* **URL параметры:**
  * **{ tableid:int }** - идентификатор таблицы
  * **{ query:tablesquery }** - запрос в формате [TablesQuery](./TABLESQUERY.md)

**Пример:**https://api.storyclm.com/v1/tables/6/countbyquery/W2FnZV1bZ3RdWzMwXQ==

**Пример ответа:**

* **Content Type:** application/json; charset=utf-8
* **Тело ответа:**
``` json
{
  "count": 4
}
```

#### LogCount

Получает количество записей в логе таблицы.

**Запрос:**

* **Method:** GET
* **Accept:** application/json
* **URL:**: https://api.storyclm.com/v1/tables/{tableid:int}/logcount
* **URL параметры:**
  * **{ tableid:int }** - идентификатор таблицы

**Пример**: https://api.storyclm.com/v1/tables/6/logcount

**Пример ответа:**

* **Content Type:** application/json; charset=utf-8
* **Тело ответа:**
``` json
{
  "count": 4
}
```

#### LogCountByDate

Получает количество записей лога таблицы после указанной даты.

**Запрос:**

* **Method:** GET
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/tables/{tableid:int}/logcountbydate/{date}
* **URL параметры:**
  * **{ tableid:int }** - идентификатор таблицы
  * **{ date:unixdate }** - дата в формате Unix Date

**Пример**: https://api.storyclm.com/v1/tables/6/logcountbydate/1476486547

**Пример ответа:**

* **Content Type:** application/json; charset=utf-8
* **Тело ответа:**
``` json
{
  "count": 4
}
```


#### FindAll

Получает постранично все данные таблицы.

**Запрос:**

* **Method:** GET
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/tables/{tableid:int}/findall/{skip:int}/{take:int}
* **URL параметры:**
  * **{ tableid:int }** - идентификатор таблицы
  * **{ skip:int }** - количество записей которые нужно пропустить 
  * **{ take:int }** - количество записей которые нужно выбрать

**Пример**: https://api.storyclm.com/v1/tables/6/findall/0/100

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

#### Find

Получает постранично данные по запросу.
Формат запроса - [TablesQuery](./TABLESQUERY.md).

[TablesQuery](./TABLESQUERY.md) - это язык запросов, разработанного специально для StoryCLM. 
Запрос в данном формате легко транслируется в любы другие языки запросов.

Параметры из которых создается запрос могут быть двух типов: Comparison и Logical.

**Запрос**

* **Method:** GET
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/tables/{tableid:int}/find/{query}/{sortfield}/{sort:int}/{skip:int}/{take:int}
* **URL параметры:**
  * **{ tableid:int }** - идентификатор таблицы
  * **{ sortfield:string }** - поле, по которому будет произведена сортировка
  * **{ sort:int }** - тип сортировки
  * **{ skip:int }** - количество записей которые нужно пропустить 
  * **{ take:int }** - количество записей которые нужно выбрать
  * **{ query:tablesquery }** - запрос в формате [TablesQuery](./TABLESQUERY.md)

**Пример:**https://api.storyclm.com/v1/tables/6/find/[age][gt][30]/age/1/0/100

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

Получает запись по идентификатору в таблице.

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

Получает коллекцию записей по списку идентификаторов в таблице.

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

**Пример:**https://api.storyclm.com/v1/tables/6/findbyids?ids=582230dff3afce8b106ba438&ids=582230e0f3afce8b106ba43a&ids=582230e0f3afce8b106ba43b&ids=582230e0f3afce8b106ba43c

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

Получает все записи лога таблицы.

**Запрос:**

* **Method:** GET
* **Accept:** application/json
* **URL**: https://admin.storyclm.com/{tableid:int}/log/{skip:int}/{take:int}
* **URL параметры:**
  * **{ tableid:int }** - идентификатор таблицы
  * **{ skip:int }** - количество записей которые нужно пропустить 
  * **{ take:int }** - количество записей которые нужно выбрать

**Пример:**https://api.storyclm.com/v1/tables/6/log/0/100

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

#### LogByDate

Получает все записи лога таблицы после указанной даты.

**Запрос:**

* **Method:** GET
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/tables/{tableid:int}/logbydate/{date}/{skip:int}/{take:int}
* **URL параметры:**
  * **{ tableid:int }** - идентификатор таблицы
  * **{ date:unixdate }** - дата в формате Unix Date
  * **{ skip:int }** - количество записей которые нужно пропустить 
  * **{ take:int }** - количество записей которые нужно выбрать

**Пример**: https://api.storyclm.com/v1/tables/6/logbydate/1476486560/0/100

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
    "id": "582230eff3afce8b106ba444",
    "tableEntityid": "582230dff3afce8b106ba438",
    "created": "2016-11-08T23:09:19.5603053+03:00",
    "operationType": 2
}
```

#### DeleteMany

Удаляет записи таблицы по списку идентификаторов.

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
      "id": "582230f0f3afce8b106ba445",
      "tableEntityid": "582230dff3afce8b106ba438",
      "created": "2016-11-08T23:09:20.1791615+03:00",
      "operationType": 2
    },
    {
      "id": "582230f0f3afce8b106ba446",
      "tableEntityid": "582230e0f3afce8b106ba43a",
      "created": "2016-11-08T23:09:20.1791615+03:00",
      "operationType": 2
    },
    {
      "id": "582230f0f3afce8b106ba447",
      "tableEntityid": "582230e0f3afce8b106ba43b",
      "created": "2016-11-08T23:09:20.1791615+03:00",
      "operationType": 2
    },
    {
      "id": "582230f0f3afce8b106ba448",
      "tableEntityid": "582230e0f3afce8b106ba43c",
      "created": "2016-11-08T23:09:20.1791615+03:00",
      "operationType": 2
    }
]
```

















