## Таблицы

**[Таблицы](TABLES.md)** - это реляционное хранилище данных. [Таблицы](TABLES.md) позволяют презентациям и внешним приложениям хранить структурированные данные на сервере, согласно схеме.

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













