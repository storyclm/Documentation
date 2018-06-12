# CLM Аналитика

Данный раздел аналитики относится к демонстрации презентаций и данным, которые собираются во время показа. Работа с аналитикой осуществляется в рамках клиента, в котором созданы учетные данные.

Выборка производится по локальному времени демонстрации презентаций, а не по дате поступления данных в хранилище. Если нужно производить выборки по дате добавления в хранилище, то нужно использовать "Feed" методы, которые позволяют делать обход хранилища по порядку от первых записей и до последних.

Стоит отметить, что большую часть времени устройство работает офлайн и хранит данные о визитах локально. Это означает, что данные о визитах могут появляться значительно позже фактического показа после того, как у устройства появится доступ к интернет. Стоит учитывать это при выгрузке аналитики.


* **Сервер** - api.storyclm.com
* **Поддерживаемые клиенты** - работающие от имени пользователя, работающие от имени сервиса.
* **Scopes** - CLMAnalitycs-R.

### Sessions

Получение статистики визитов для клиента по презентациям и пользователям за период.

**Модель:**
  * **SessionId** - Идентификатор сессии.
  * **PresentationId** - Идентификатор презентации.
  * **ClientId** - Идентификатор клиента.
  * **Complete** - Завершенная демонстрация.
  * **UserId** - Иднетификатор пользователя.
  * **Latitude** - Широта места проведения демонстрации.
  * **Longtitude** - Долгота места проведения демонстрации.
  * **DateTime** - Дата демонстрации. Считается от начала демонстрации.
  * **Duration** - Продолжительность демонстрации в секундах.
  * **Address** - Адрес, где производилась демонстрация.
  * **SlidesCount** - Количество слайдов которые были показаны во время демонстрации.
  * **TimeZoneOffset** - Часой пояс.

**Запрос**

* **Method:** GET
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/analitycs/clm/sessions?start={start}&finish={finish}&pids={pIds}&pids={pIds}&uids={uIds}&completeOnly={completeOnly}&skip={skip}&take={take}
* **URL параметры:**
  * **{ pIds:int[] }** - Коллекция идентификаторов презентаций. Если презентации не указаны, то выборка будет произведенная по всем презентациям клиента. Необязательный параметр.
  * **{ uIds:string[] }** - Коллекция идентификаторов пользователей клиента. Если пользователи не указаны, то выборка будет произведена по всем пользователям клиента. Необязательный параметр.
  * **{ start:unixdate }** - Дата после которой будет произведена выборка. Если дата не указана то выборка будет произведена с начала коллекции. дата в формате Unix Date. Необязательный параметр.
  * **{ finish:unixdate }** - Дата до которой будет произведена выборка. Если дата не указана то выборка будет произведена до конца коллекции. дата в формате Unix Date. Необязательный параметр.
  * **{ completeOnly:bool }** - Учитывать только завершенные визиты. Необязательный параметр. По умолчанию будут выбраны все.
  * **{ skip:int }** - количество записей, которые нужно пропустить. По умолчанию 0.
  * **{ take:int }** - количество записей, которые нужно выбрать. По умолчанию 100. Максимум 1000.

**Пример:** https://api.storyclm.com/v1/analitycs/clm/sessions?skip=0&take=100

**Пример:** https://api.storyclm.com/v1/analitycs/clm/sessions?start=1514764800&finish=1522540800&skip=0&take=100

**Пример:** https://api.storyclm.com/v1/analitycs/clm/sessions?start=1514764800skip=0&take=100

**Пример:** https://api.storyclm.com/v1/analitycs/clm/sessions?uids=b1ae249b-22c4-4b0b-a9ec-66f0521a4715&uids=fe84233b-0f47-

**Пример:** https://api.storyclm.com/v1/analitycs/clm/sessions?pids=17&pids=4&uids=b1ae249b-22c4-4b0b-a9ec-66f0521a4715&uids=fe84233b-0f47-4a7e-9ad8-bec78f4b5857&skip=0&take=100

**Пример ответа:**

* **Content Type:** application/json; charset=utf-8
* **Тело ответа:**
``` json
[
    {
        "sessionId": "C228CF45-B4F6-4ADB-89A2-E422F037AD52",
        "presentationId": 0,
        "clientId": 0,
        "complete": false,
        "userId": null,
        "latitude": null,
        "longtitude": null,
        "dateTime": "2015-01-29T18:50:42.169Z",
        "duration": 152,
        "address": null,
        "slidesCount": 1,
        "timeZoneOffset": 0
    },
    {
        "sessionId": "1929DEDA-D52A-457A-A674-F8F1DC24FAA6",
        "presentationId": 2144,
        "clientId": 18,
        "complete": false,
        "userId": "c9f3f4b0-db64-4d6e-adcd-128281af737f",
        "latitude": "55.88483141",
        "longtitude": "37.65572020",
        "dateTime": "2015-01-29T18:49:18.75Z",
        "duration": 1,
        "address": "Tikhomirova ulitsa 14к1,Moscow,Moscow,Russia,127282",
        "slidesCount": 1,
        "timeZoneOffset": 0
    }
]
```

### Sessions Feed

Получение статистики визитов для клиента по презентациям и пользователем после указанной даты. 

Данные выбираются не по фактическим дата проведения демонстрации, а по поступлению данных на сервер.

**Модель:**
  * **SessionId** - Идентификатор сессии.
  * **PresentationId** - Идентификатор презентации.
  * **ClientId** - Идентификатор клиента.
  * **Complete** - Завершенная демонстрация.
  * **UserId** - Иднетификатор пользователя.
  * **Latitude** - Широта места проведения демонстрации.
  * **Longtitude** - Долгота места проведения демонстрации.
  * **DateTime** - Дата демонстрации. Считается от начала демонстрации.
  * **Duration** - Продолжительность демонстрации в секундах.
  * **Address** - Адрес, где производилась демонстрация.
  * **SlidesCount** - Колличество слайдов которые были показаны во время демонстрации.
  * **TimeZoneOffset** - Часовой пояс.

**Запрос**

* **Method:** GET
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/analitycs/clm/sessions/feed?date={date}&pids={pIds}&pids={pIds}&uids={uIds}&completeOnly={completeOnly}&skip={skip}&take={take}
* **URL параметры:**
  * **{ pIds:int[] }** - Коллекция идентификаторов презентаций. Если презентации не указаны, то выборка будет произведенная по всем презентациям клиента. Необязательный параметр.
  * **{ uIds:string[] }** - Коллекция идентификаторов пользователей клиента. Если пользователи не указаны, то выборка будет произведена по всем пользователям клиента. Необязательный параметр.
  * **{ date:unixdate }** - Дата после которой будет произведена выборка. Если дата не указана, то выборка будет произведена с начала коллекции. дата в формате Unix Date. Необязательный параметр.
  * **{ completeOnly:bool }** - Учитывать только завершенные визиты. Необязательный параметр. По умолчанию будут выбраны все.
  * **{ skip:int }** - количество записей, которые нужно пропустить. По умолчанию 0.
  * **{ take:int }** - количество записей, которые нужно выбрать. По умолчанию 100. Максимум 1000.

**Пример:** https://api.storyclm.com/v1/analitycs/clm/sessions/feed?skip=0&take=100

**Пример:** https://api.storyclm.com/v1/analitycs/clm/sessions/feed?date=1514764800&skip=0&take=100

**Пример:** https://api.storyclm.com/v1/analitycs/clm/sessions/feed?uids=b1ae249b-22c4-4b0b-a9ec-66f0521a4715&uids=fe84233b-0f47-

**Пример:** https://api.storyclm.com/v1/analitycs/clm/sessions/feed?pids=17&pids=4&uids=b1ae249b-22c4-4b0b-a9ec-66f0521a4715&uids=fe84233b-0f47-4a7e-9ad8-bec78f4b5857&skip=0&take=100

**Пример ответа:**

* **Content Type:** application/json; charset=utf-8
* **Тело ответа:**
``` json
[
    {
        "sessionId": "C228CF45-B4F6-4ADB-89A2-E422F037AD52",
        "presentationId": 0,
        "clientId": 0,
        "complete": false,
        "userId": null,
        "latitude": null,
        "longtitude": null,
        "dateTime": "2015-01-29T18:50:42.169Z",
        "duration": 152,
        "address": null,
        "slidesCount": 1,
        "timeZoneOffset": 0
    },
    {
        "sessionId": "1929DEDA-D52A-457A-A674-F8F1DC24FAA6",
        "presentationId": 2144,
        "clientId": 18,
        "complete": false,
        "userId": "c9f3f4b0-db64-4d6e-adcd-128281af737f",
        "latitude": "55.88483141",
        "longtitude": "37.65572020",
        "dateTime": "2015-01-29T18:49:18.75Z",
        "duration": 1,
        "address": "Tikhomirova ulitsa 14к1,Moscow,Moscow,Russia,127282",
        "slidesCount": 1,
        "timeZoneOffset": 0
    }
]
```

### Sessions Count

Получение количества визитов для клиента по презентациям и пользователям за период времени.

**Запрос**

* **Method:** GET
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/analitycs/clm/sessions/count?start={start}&finish={finish}&pids={pIds}&pids={pIds}&uids={uIds}&completeOnly={completeOnly}
* **URL параметры:**
  * **{ pIds:int[] }** - Коллекция идентификаторов презентаций. Если презентации не указаны, то выборка будет произведенная по всем презентациям клиента. Необязательный параметр.
  * **{ uIds:string[] }** - Коллекция идентификаторов пользователей клиента. Если пользователи не указаны, то выборка будет произведена по всем пользователям клиента. Необязательный параметр.
  * **{ start:unixdate }** - Дата после которой будет произведена выборка. Если дата не указана, то выборка будет произведена с начала коллекции. дата в формате Unix Date. Необязательный параметр.
  * **{ finish:unixdate }** - Дата до которой будет произведена выборка. Если дата не указана, то выборка будет произведена до конца коллекции. дата в формате Unix Date. Необязательный параметр.
  * **{ completeOnly:bool }** - Учитывать только завершенные визиты. Необязательный параметр. По умолчанию будут выбраны все.

**Пример:** https://api.storyclm.com/v1/analitycs/clm/sessions/count

**Пример:** https://api.storyclm.com/v1/analitycs/clm/sessions/count?start=1514764800&finish=1522540800

**Пример:** https://api.storyclm.com/v1/analitycs/clm/sessions/count?start=1514764800

**Пример:** https://api.storyclm.com/v1/analitycs/clm/sessions/count?uids=b1ae249b-22c4-4b0b-a9ec-66f0521a4715&uids=fe84233b-0f47

**Пример:** https://api.storyclm.com/v1/analitycs/clm/sessions/count?pids=17&pids=4&uids=b1ae249b-22c4-4b0b-a9ec-66f0521a4715&uids=fe84233b-0f47-4a7e-9ad8-bec78f4b5857

**Пример ответа:**

* **Content Type:** application/json; charset=utf-8
* **Тело ответа:**
``` json
{
    "count": 2822
}
```

### Custom Events

Получение кастомных событий презентаций по пользователям за период.

**Модель:**
  * **SessionId** - Идентификатор сессии.
  * **PresentationId** - Идентификатор презентации.
  * **ClientId** - Идентификатор клиента.
  * **UserId** - Иднетификатор пользователя.
  * **Key** - Ключ.
  * **Value** - Значение.
  * **Created** - Дата демонстрации. Считается от начала демонстрации.
  * **TimeZoneOffset** - Часой пояс.

**Запрос**

* **Method:** GET
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/analitycs/clm/customevents?start={start}&finish={finish}&pids={pIds}&pids={pIds}&uids={uIds}&completeOnly={completeOnly}&skip={skip}&take={take}
* **URL параметры:**
  * **{ pIds:int[] }** - Коллекция идентификаторов презентаций. Если презентации не указаны, то выборка будет произведенная по всем презентациям клиента. Необязательный параметр.
  * **{ uIds:string[] }** - Коллекция идентификаторов пользователей клиента. Если пользователи не указаны, то выборка будет произведена по всем пользователям клиента. Необязательный параметр.
  * **{ start:unixdate }** - Дата после которой будет произведена выборка. Если дата не указана, то выборка будет произведена с начала коллекции. дата в формате Unix Date. Необязательный параметр.
  * **{ finish:unixdate }** - Дата до которой будет произведена выборка. Если дата не указана, то выборка будет произведена до конца коллекции. дата в формате Unix Date. Необязательный параметр.
  * **{ completeOnly:bool }** - Учитывать только завершенные визиты. Необязательный параметр. По умолчанию будут выбраны все.
  * **{ skip:int }** - количество записей, которые нужно пропустить. По умолчанию 0.
  * **{ take:int }** - количество записей, которые нужно выбрать. По умолчанию 100. Максимум 1000.

**Пример:** https://api.storyclm.com/v1/analitycs/clm/customevents?skip=0&take=100

**Пример:** https://api.storyclm.com/v1/analitycs/clm/customevents?start=1514764800&finish=1522540800&skip=0&take=100

**Пример:** https://api.storyclm.com/v1/analitycs/clm/customevents?start=1514764800skip=0&take=100

**Пример:** https://api.storyclm.com/v1/analitycs/clm/customevents?uids=b1ae249b-22c4-4b0b-a9ec-66f0521a4715&uids=fe84233b-0f47-

**Пример:** https://api.storyclm.com/v1/analitycs/clm/customevents?pids=17&pids=4&uids=b1ae249b-22c4-4b0b-a9ec-66f0521a4715&uids=fe84233b-0f47-4a7e-9ad8-bec78f4b5857&skip=0&take=100

**Пример ответа:**

* **Content Type:** application/json; charset=utf-8
* **Тело ответа:**
``` json
[
    {
        "sessionId": "8927B33AA7A74295BD2D9C5B750390F8",
        "clientId": 18,
        "presentationId": 5361,
        "userId": "2118ce7d-4a4b-4893-9419-b9b42366de9d",
        "key": "specialnost",
        "value": "neanat",
        "created": "2018-02-04T13:50:36Z",
        "timeZoneOffset": 180
    },
    {
        "sessionId": "8927B33AA7A74295BD2D9C5B750390F8",
        "clientId": 18,
        "presentationId": 5361,
        "userId": "2118ce7d-4a4b-4893-9419-b9b42366de9d",
        "key": "specialnost",
        "value": "neanat",
        "created": "2018-02-04T13:50:41Z",
        "timeZoneOffset": 180
    }
]
```

### Custom Events Feed

Получение кастомных событий презентаций по пользователям после указанной даты.
Данные выбираются не по фактическим датам проведения демонстрации, а по поступлению данных на сервер.

**Модель:**
  * **SessionId** - Идентификатор сессии.
  * **PresentationId** - Идентификатор презентации.
  * **ClientId** - Идентификатор клиента.
  * **UserId** - Иднетификатор пользователя.
  * **Key** - Ключ.
  * **Value** - Значение.
  * **Created** - Дата демонстрации. Считается от начала демонстрации.
  * **TimeZoneOffset** - Часой пояс.

**Запрос**

* **Method:** GET
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/analitycs/clm/customevents/feed?date={date}&pids={pIds}&pids={pIds}&uids={uIds}&completeOnly={completeOnly}&skip={skip}&take={take}
* **URL параметры:**
  * **{ pIds:int[] }** - Коллекция идентификаторов презентаций. Если презентации не указаны, то выборка будет произведенная по всем презентациям клиента. Необязательный параметр.
  * **{ uIds:string[] }** - Коллекция идентификаторов пользователей клиента. Если пользователи не указаны, то выборка будет произведена по всем пользователям клиента. Необязательный параметр.
  * **{ date:unixdate }** - Дата после которой будет произведена выборка. Если дата не указана, то выборка будет произведена с начала коллекции. дата в формате Unix Date. Необязательный параметр.
  * **{ completeOnly:bool }** - Учитывать только завершенные визиты. Необязательный параметр. По умолчанию будут выбраны все.
  * **{ skip:int }** - количество записей, которые нужно пропустить. По умолчанию 0.
  * **{ take:int }** - количество записей, которые нужно выбрать. По умолчанию 100. Максимум 1000.

**Пример:** https://api.storyclm.com/v1/analitycs/clm/customevents/feed?skip=0&take=100

**Пример:** https://api.storyclm.com/v1/analitycs/clm/customevents/feed?date=1514764800&skip=0&take=100

**Пример:** https://api.storyclm.com/v1/analitycs/clm/customevents/feed?uids=b1ae249b-22c4-4b0b-a9ec-66f0521a4715&uids=fe84233b-0f47-

**Пример:** https://api.storyclm.com/v1/analitycs/clm/customevents/feed?pids=17&pids=4&uids=b1ae249b-22c4-4b0b-a9ec-66f0521a4715&uids=fe84233b-0f47-4a7e-9ad8-bec78f4b5857&skip=0&take=100

**Пример ответа:**

* **Content Type:** application/json; charset=utf-8
* **Тело ответа:**
``` json
[
    {
        "sessionId": "8927B33AA7A74295BD2D9C5B750390F8",
        "clientId": 18,
        "presentationId": 5361,
        "userId": "2118ce7d-4a4b-4893-9419-b9b42366de9d",
        "key": "specialnost",
        "value": "neanat",
        "created": "2018-02-04T13:50:36Z",
        "timeZoneOffset": 180
    },
    {
        "sessionId": "8927B33AA7A74295BD2D9C5B750390F8",
        "clientId": 18,
        "presentationId": 5361,
        "userId": "2118ce7d-4a4b-4893-9419-b9b42366de9d",
        "key": "specialnost",
        "value": "neanat",
        "created": "2018-02-04T13:50:41Z",
        "timeZoneOffset": 180
    }
]
```

### Custom Events Count

Получение количества визитов для клиента по презентациям и пользователям за период.

**Запрос**

* **Method:** GET
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/analitycs/clm/customevents/count?start={start}&finish={finish}&pids={pIds}&pids={pIds}&uids={uIds}&completeOnly={completeOnly}
* **URL параметры:**
  * **{ pIds:int[] }** - Коллекция идентификаторов презентаций. Если презентации не указаны, то выборка будет произведенная по всем презентациям клиента. Необязательный параметр.
  * **{ uIds:string[] }** - Коллекция идентификаторов пользователей клиента. Если пользователи не указаны, то выборка будет произведена по всем пользователям клиента. Необязательный параметр.
  * **{ start:unixdate }** - Дата после которой будет произведена выборка. Если дата не указана, то выборка будет произведена с начала коллекции. дата в формате Unix Date. Необязательный параметр.
  * **{ finish:unixdate }** - Дата до которой будет произведена выборка. Если дата не указана, то выборка будет произведена до конца коллекции. дата в формате Unix Date. Необязательный параметр.
  * **{ completeOnly:bool }** - Учитывать только завершенные визиты. Необязательный параметр. По умолчанию будут выбраны все.

**Пример:** https://api.storyclm.com/v1/analitycs/clm/customevents/count

**Пример:** https://api.storyclm.com/v1/analitycs/clm/customevents/count?start=1514764800&finish=1522540800

**Пример:** https://api.storyclm.com/v1/analitycs/clm/customevents/count?start=1514764800

**Пример:** https://api.storyclm.com/v1/analitycs/clm/customevents/count?uids=b1ae249b-22c4-4b0b-a9ec-66f0521a4715&uids=fe84233b-0f47

**Пример:** https://api.storyclm.com/v1/analitycs/clm/customevents/count?pids=17&pids=4&uids=b1ae249b-22c4-4b0b-a9ec-66f0521a4715&uids=fe84233b-0f47-4a7e-9ad8-bec78f4b5857

**Пример ответа:**

* **Content Type:** application/json; charset=utf-8
* **Тело ответа:**
``` json
{
    "count": 91
}
```

### Slides Demonstrations

Получение статистики демонстраций слайдов для клиента по презентациям и пользователям за период.

**Модель:**
  * **SessionId** - Идентификатор сессии.
  * **PresentationId** - Идентификатор презентации.
  * **ClientId** - Идентификатор клиента.
  * **SlideName** - Название слайда.
  * **UserId** - Идентификатор пользователя.
  * **Duration** - Продолжительность в секундах.
  * **Navigation** - Тип навигации.
  * **DateTime** - Дата демонстрации. Считается от начала демонстрации.

**Запрос**

* **Method:** GET
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/analitycs/clm/slidesdemonstrations?start={start}&finish={finish}&pids={pIds}&pids={pIds}&uids={uIds}&skip={skip}&take={take}
* **URL параметры:**
  * **{ pIds:int[] }** - Коллекция идентификаторов презентаций. Если презентации не указаны, то выборка будет произведенная по всем презентациям клиента. Необязательный параметр.
  * **{ uIds:string[] }** - Коллекция идентификаторов пользователей клиента. Если пользователи не указаны, то выборка будет произведена по всем пользователям клиента. Необязательный параметр.
  * **{ start:unixdate }** - Дата после которой будет произведена выборка. Если дата не указана, то выборка будет произведена с начала коллекции. дата в формате Unix Date. Необязательный параметр.
  * **{ finish:unixdate }** - Дата до которой будет произведена выборка. Если дата не указана, то выборка будет произведена до конца коллекции. дата в формате Unix Date. Необязательный параметр.
  * **{ skip:int }** - количество записей, которые нужно пропустить. По умолчанию 0.
  * **{ take:int }** - количество записей, которые нужно выбрать. По умолчанию 100. Максимум 1000.

**Пример:** https://api.storyclm.com/v1/analitycs/clm/slidesdemonstrations?skip=0&take=100

**Пример:** https://api.storyclm.com/v1/analitycs/clm/slidesdemonstrations?start=1514764800&finish=1522540800&skip=0&take=100

**Пример:** https://api.storyclm.com/v1/analitycs/clm/slidesdemonstrations?start=1514764800skip=0&take=100

**Пример:** https://api.storyclm.com/v1/analitycs/clm/slidesdemonstrations?uids=b1ae249b-22c4-4b0b-a9ec-66f0521a4715&uids=fe84233b-0f47-

**Пример:** https://api.storyclm.com/v1/analitycs/clm/slidesdemonstrations?pids=17&pids=4&uids=b1ae249b-22c4-4b0b-a9ec-66f0521a4715&uids=fe84233b-0f47-4a7e-9ad8-bec78f4b5857&skip=0&take=100

**Пример ответа:**

* **Content Type:** application/json; charset=utf-8
* **Тело ответа:**
``` json
[
    {
        "userId": "20f1aa83-cde2-4854-9560-455bdf269c31",
        "clientId": 18,
        "presentationId": 2144,
        "sessionID": "5D978293-7371-433B-AEE0-33097A583A17",
        "slideName": "index.html",
        "duration": 4,
        "navigation": "in",
        "dateTime": "2015-01-29T18:29:13.466Z"
    },
    {
        "userId": "c9f3f4b0-db64-4d6e-adcd-128281af737f",
        "clientId": 18,
        "presentationId": 2144,
        "sessionID": "AB6B1D43-854F-4925-8DBC-4E68027D50F9",
        "slideName": "index.html",
        "duration": 112,
        "navigation": "in",
        "dateTime": "2015-01-29T18:44:18.353Z"
    }
]
```

### Slides Demonstrations Feed

Получение статистики демонстраций слайдов для клиента по презентациям и пользователям после указанной даты.
Данные выбираются не по фактическим дата проведения демонстрации, а по поступлению данных на сервер.

**Модель:**
  * **SessionId** - Идентификатор сессии.
  * **PresentationId** - Идентификатор презентации.
  * **ClientId** - Идентификатор клиента.
  * **SlideName** - Название слайда.
  * **UserId** - Идентификатор пользователя.
  * **Duration** - Продолжительность в секундах.
  * **Navigation** - Тип навигации.
  * **DateTime** - Дата демонстрации. Считается от начала демонстрации.

**Запрос**

* **Method:** GET
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/analitycs/clm/slidesdemonstrations/feed?date={start}&pids={pIds}&pids={pIds}&uids={uIds}&completeOnly={completeOnly}&skip={skip}&take={take}
* **URL параметры:**
  * **{ pIds:int[] }** - Коллекция идентификаторов презентаций. Если презентации не указаны, то выборка будет произведенная по всем презентациям клиента. Необязательный параметр.
  * **{ uIds:string[] }** - Коллекция идентификаторов пользователей клиента. Если пользователи не указаны, то выборка будет произведена по всем пользователям клиента. Необязательный параметр.
  * **{ date:unixdate }** - Дата после которой будет произведена выборка. Если дата не указана, то выборка будет произведена с начала коллекции. дата в формате Unix Date. Необязательный параметр.
  * **{ skip:int }** - количество записей, которые нужно пропустить. По умолчанию 0.
  * **{ take:int }** - количество записей, которые нужно выбрать. По умолчанию 100. Максимум 1000.

**Пример:** https://api.storyclm.com/v1/analitycs/clm/slidesdemonstrations/feed?skip=0&take=100

**Пример:** https://api.storyclm.com/v1/analitycs/clm/slidesdemonstrations/feed?date=1514764800&skip=0&take=100

**Пример:** https://api.storyclm.com/v1/analitycs/clm/slidesdemonstrations/feed?uids=b1ae249b-22c4-4b0b-a9ec-66f0521a4715&uids=fe84233b-0f47-

**Пример:** https://api.storyclm.com/v1/analitycs/clm/slidesdemonstrations/feed?pids=17&pids=4&uids=b1ae249b-22c4-4b0b-a9ec-66f0521a4715&uids=fe84233b-0f47-4a7e-9ad8-bec78f4b5857&skip=0&take=100

**Пример ответа:**

* **Content Type:** application/json; charset=utf-8
* **Тело ответа:**
``` json
[
    {
        "userId": "20f1aa83-cde2-4854-9560-455bdf269c31",
        "clientId": 18,
        "presentationId": 2144,
        "sessionID": "5D978293-7371-433B-AEE0-33097A583A17",
        "slideName": "index.html",
        "duration": 4,
        "navigation": "in",
        "dateTime": "2015-01-29T18:29:13.466Z"
    },
    {
        "userId": "c9f3f4b0-db64-4d6e-adcd-128281af737f",
        "clientId": 18,
        "presentationId": 2144,
        "sessionID": "AB6B1D43-854F-4925-8DBC-4E68027D50F9",
        "slideName": "index.html",
        "duration": 112,
        "navigation": "in",
        "dateTime": "2015-01-29T18:44:18.353Z"
    }
]
```

### Slides Demonstrations Count

Получение количества демонстраций слайдов для клиента по презентациям и пользователям за период.

**Запрос**

* **Method:** GET
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/analitycs/clm/slidesdemonstrations/count?start={start}&finish={finish}&pids={pIds}&pids={pIds}&uids={uIds}
* **URL параметры:**
  * **{ pIds:int[] }** - Коллекция идентификаторов презентаций. Если презентации не указаны, то выборка будет произведенная по всем презентациям клиента. Необязательный параметр.
  * **{ uIds:string[] }** - Коллекция идентификаторов пользователей клиента. Если пользователи не указаны, то выборка будет произведена по всем пользователям клиента. Необязательный параметр.
  * **{ start:unixdate }** - Дата после которой будет произведена выборка. Если дата не указана, то выборка будет произведена с начала коллекции. дата в формате Unix Date. Необязательный параметр.
  * **{ finish:unixdate }** - Дата до которой будет произведена выборка. Если дата не указана, то выборка будет произведена до конца коллекции. дата в формате Unix Date. Необязательный параметр.

**Пример:** https://api.storyclm.com/v1/analitycs/clm/slidesdemonstrations/count

**Пример:** https://api.storyclm.com/v1/analitycs/clm/slidesdemonstrations/count?start=1514764800&finish=1522540800

**Пример:** https://api.storyclm.com/v1/analitycs/clm/slidesdemonstrations/count?start=1514764800

**Пример:** https://api.storyclm.com/v1/analitycs/clm/slidesdemonstrations/count?uids=b1ae249b-22c4-4b0b-a9ec-66f0521a4715&uids=fe84233b-0f47

**Пример:** https://api.storyclm.com/v1/analitycs/clm/slidesdemonstrations/count?pids=17&pids=4&uids=b1ae249b-22c4-4b0b-a9ec-66f0521a4715&uids=fe84233b-0f47-4a7e-9ad8-bec78f4b5857

**Пример ответа:**

* **Content Type:** application/json; charset=utf-8
* **Тело ответа:**
``` json
{
    "count": 100
}
```