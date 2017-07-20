# Контент

В основе понятия "контент" в StoryCLM лежит интерактивная презентация (приложение). Приложения для StoryCLM - это Web приложения создаваемые с использованием веб-технологий, таких как HTML, CSS, и JavaScript. Приложения состоят из слайдов, медиафайлов и пакета с ассетами. Каждое приложение находится в клиенте StoryCLM. Для того что бы получить доступ к контенту через API, нужно иметь необходимые права в клиенте к которому принадлежит приложение.  Помимо прав, клиент и приложение должно быть в активном состоянии.  

* **Сервер** - api.storyclm.com
* **Поддерживаемы клиенты** - работающие от имени пользователя, работающие от имени сервиса. 


### Clients

Список доступных клиентов.

**Запрос:**

* **Method**: GET
* **Accept**: application/json
* **URL**: https://api.storyclm.com/v1/clients

**Пример**: https://api.storyclm.com/v1/clients

**Пример ответа:**

* **Content Type**: application/json; charset=utf-8
* **Тело ответа**:

```JSON
[
  {
    "id": 1,
    "name": "Test",
    "lockoutEnabled": false,
    "shortDescription": "Тестовый Тест Тестович",
    "longDescription": "Полное описание Тестовый Тест Тестович",
    "thumbImgId": "https://stagingclmsstorage.blob.core.windows.net/images/0e08fdba685247cd90b3121775a344bcdfe886384d89409ea8247e2a5983f362.jpg",
    "imgId": "https://stagingclmsstorage.blob.core.windows.net/images/5ea031388a7e4e848e2209c7dc302efdfa2c96e964d349a28a54541f253687fd.jpg",
    "url": "https://mail.yandex.ru",
    "email": "test@test.ru",
    "created": "2016-09-06T14:49:51.01",
    "updated": "2017-03-11T14:39:27.577",
    "deviceLogTable": null,
    "baseStatisticsTable": null,
    "geolocationTable": null,
    "presentations": [
      {
        "debug": false,
        "skip": false,
        "lockout": false,
        "id": 4,
        "revision": 165
      },
      {
        "debug": false,
        "skip": false,
        "lockout": false,
        "id": 31,
        "revision": 1066
      }
    ],
    "users": [
      {
        "id": "a4be8f4a-96c5-49b8-87c9-51b0de7c869b",
        "role": 2
      },
      {
        "id": "fe84233b-0f47-4a7e-9ad8-bec78f4b5857",
        "role": 0
      },
      {
        "id": "b1ae249b-22c4-4b0b-a9ec-66f0521a4715",
        "role": 0
      }
    ],
    "groups": [
      {
        "users": [],
        "id": 53,
        "name": "group1"
      },
      {
        "users": [
          "1f6f7f74-3407-4521-a19d-42fd0b85a8b9"
        ],
        "id": 57,
        "name": "Группа3"
      }
    ],
    "tables": [
      {
        "id": 9,
        "name": "ContactBack"
      },
      {
        "id": 14,
        "name": "ContactNewEdition"
      }
    ]
  }
]
```
**Результат** - коллесция объектов "Клиент". Каждый объект коллекции содержит следующие поля:

* **id** - уникальный идентификатор клиента;
* **name** - название клиент;
* **lockoutEnabled** - блокировка;
* **shortDescription** - краткое описание;
* **longDescription** - описание;
* **thumbImgId** - URL картинки-подложки;
* **imgId** - URL логотипа;
* **url** - сайт компании;
* **email** - email контактного лица;
* **created** - дата создания;
* **updated** - дата последнего обновления;
* **deviceLogTable** - идентификатор таблицы в которую записывается системный лог;
* **baseStatisticsTable** - идентификатор таблицы в которую записывается статистика приложений;
* **geolocationTable** - идентификатор таблицы в которую записываются геоданные;
* **presentations** - список презентаций. Представляет из себя коллекцию упрощенных объектов описывающих презентацию;
  * **debug** - презентация в режиме разработки;
  * **skip** - не синхронизировать презентацию;
  * **lockout** - презентация заблокирована;
  * **id** - уникальный идентификатор;
  * **revision** - ревизия. Используется для синхронизации. При каждом изменении объекта поле увелицивается на еденицу;
* **users** - список пользователей. Представляет из себя коллекцию упрощенных объектов описывающих пользователя;
  * **id** - идентификатор пользователя;
  * **role** - роль пользователя в клиенте;
* **groups** - список групп. Представляет из себя коллекцию упрощенных объектов описывающих группу пользователей;
  * **users** - спискок идентификаторов пользователей состоящих в группе;
  * **id** - идентификатор группы;
  * **name** - название группы;
* **tables** - список таблиц. Представляет из себя коллекцию упрощенных объектов описывающих таблицу;
  * **id** - идентификатор таблицы;
  * **name** - название таблицы;



### Client

Получает клиент по идентификатору.

**Запрос:**

* **Method**: GET
* **Accept**: application/json
* **URL**: https://api.storyclm.com/v1/clients/{clientid}
* **URL параметры**:
  * **\{ clientid:int }** - идентификатор клиента;

**Пример**: https://api.storyclm.com/v1/clients/1

**Пример ответа:**

* **Content Type**: application/json; charset=utf-8
* **Тело ответа**:

```JSON
  {
    "id": 1,
    "name": "Test",
    "lockoutEnabled": false,
    "shortDescription": "Тестовый Тест Тестович",
    "longDescription": "Полное описание Тестовый Тест Тестович",
    "thumbImgId": "https://stagingclmsstorage.blob.core.windows.net/images/0e08fdba685247cd90b3121775a344bcdfe886384d89409ea8247e2a5983f362.jpg",
    "imgId": "https://stagingclmsstorage.blob.core.windows.net/images/5ea031388a7e4e848e2209c7dc302efdfa2c96e964d349a28a54541f253687fd.jpg",
    "url": "https://mail.yandex.ru",
    "email": "test@test.ru",
    "created": "2016-09-06T14:49:51.01",
    "updated": "2017-03-11T14:39:27.577",
    "deviceLogTable": null,
    "baseStatisticsTable": null,
    "geolocationTable": null,
    "presentations": [
      {
        "debug": false,
        "skip": false,
        "lockout": false,
        "id": 4,
        "revision": 165
      },
      {
        "debug": false,
        "skip": false,
        "lockout": false,
        "id": 31,
        "revision": 1066
      }
    ],
    "users": [
      {
        "id": "a4be8f4a-96c5-49b8-87c9-51b0de7c869b",
        "role": 2
      },
      {
        "id": "fe84233b-0f47-4a7e-9ad8-bec78f4b5857",
        "role": 0
      },
      {
        "id": "b1ae249b-22c4-4b0b-a9ec-66f0521a4715",
        "role": 0
      }
    ],
    "groups": [
      {
        "users": [],
        "id": 53,
        "name": "group1"
      },
      {
        "users": [
          "1f6f7f74-3407-4521-a19d-42fd0b85a8b9"
        ],
        "id": 57,
        "name": "Группа3"
      }
    ],
    "tables": [
      {
        "id": 9,
        "name": "ContactBack"
      },
      {
        "id": 14,
        "name": "ContactNewEdition"
      }
    ]
  }
```
### Presentation

Получает презентацию по идентификатору.

**Запрос:**

* **Method**: GET
* **Accept**: application/json
* **URL**: https://api.storyclm.com/v1/presentations/{presentationId}
* **URL параметры**:
  * **\{ presentationId:int }** - идентификатор клиента;

**Пример**: https://api.storyclm.com/v1/presentations/17

**Пример ответа:**

* **Content Type**: application/json; charset=utf-8
* **Тело ответа**:

```JSON
{
  "id": 17,
  "name": "CLM",
  "shortDescription": null,
  "longDescription": null,
  "thumbImgId": "",
  "imgId": "https://stagingclmsstorage.blob.core.windows.net/images/e7dadec975c3448893d36353484d3dfa1c2fd644f47749789a63ee1326a050bd.png",
  "order": 3,
  "revision": 14,
  "created": "2016-12-27T11:06:14.447",
  "updated": "2016-12-27T11:09:49.187",
  "clientId": 1,
  "debugModeEnabled": false,
  "skip": false,
  "mapEnabled": true,
  "mapType": 0,
  "needConfirmation": true,
  "previewMode": 1,
  "map": null,
  "visibility": true,
  "sourcesFolder": {
    "id": 16,
    "blobId": "b43e293b66c349309dd9b4fd38c540b39aaba6aba74f488c9538ce8a84864d5d",
    "fileSize": 9203268,
    "mimeType": "application/zip",
    "revision": 1,
    "created": "2016-12-27T11:06:53.22",
    "updated": "2016-12-27T11:09:25.12"
  },
  "mediaFiles": [
    {
      "fileSize": 721878,
      "id": 118,
      "revision": 0
    }
  ],
  "slides": [
    {
      "id": 2140,
      "revision": 0
    },
    {
      "id": 2141,
      "revision": 0
    },
    {
      "id": 2142,
      "revision": 0
    },
    {
      "id": 2143,
      "revision": 1
    }
  ],
  "presentations": [],
  "users": [
    {
      "revision": 14,
      "id": "fe84233b-0f47-4a7e-9ad8-bec78f4b5857",
      "role": 0
    },
    {
      "revision": 0,
      "id": "b1ae249b-22c4-4b0b-a9ec-66f0521a4715",
      "role": 0
    }
  ]
}
```
**Результат** - объект "Презентация". Объект содержит следующие поля:

* **id** - уникальный идентификатор презентации;
* **name** - название презентации;
* **shortDescription** - краткое описание;
* **longDescription** - описание;
* **thumbImgId** - иконка;
* **imgId** - логотип;
* **order** - "Вес", используется при выстраивании списка;
* **revision** - ревизия. Используется для синхронизации. При каждом изменении объекта поле увеличивается на единицу;
* **created** - дата создания;
* **updated** - дата редактирования;
* **clientId** - идентификатор клиента которому принадлежит презентация;
* **debugModeEnabled** - режим разработки;
* **skip** - режим пропуска синхронизации;
* **mapEnabled** - карта включена. Это означает, что презентация использует в своей работе карту;
* **mapType** - тип карты;
* **needConfirmation** - запрашивать подтверждение при выходе из презентации;
* **previewMode** - режим отображения;
* **map** - карта;
* **visibility** - отображать или скрывать презентацию;
* **sourcesFolder** - пакет с ассетами;
  * **id** - идентификация пакета;
  * **blobId** - название пакета;
  * **fileSize** - размер пакета в байтах;
  * **mimeType** - тип пакета, обычно архив zip;
  * **revision** - ревизия. Используется для синхронизации. При каждом изменении объекта поле увеличивается на единицу;
  * **created** - дата создания пакета;
  * **updated** - дата последней загрузки пакета;
* **mediaFiles** - список медиафайлов. Представляет из себя коллекцию упрощенных объектов описывающих медиафайл;
  * **fileSize** - размер файла в байтах;
  * **id** - уникальный идентификатор медиафайла;
  * **revision** - ревизия. Используется для синхронизации. При каждом изменении объекта поле увеличивается на единицу;
* **slides** - список слайдов. Представляет из себя коллекцию упрощенных объектов описывающих слайд;
  * **id** - идентификатор слайда;
  * **revision** - ревизия. Используется для синхронизации. При каждом изменении объекта поле увеличивается на единицу;
* **presentations** - список презентаций которые необходимы для корректной работы текущей презентации.
* **users** - список пользователей презентации. Представляет из себя коллекцию упрощенных объектов описывающих пользователя;
  * **revision** - ревизия. Используется для синхронизации. При каждом изменении объекта поле увеличивается на единицу;
  * **id** - идентификатор пользователя;
  * **role** - роль пользователя;

### Mediafile

Получает медиафайл по идентификатору.

**Запрос:**

* **Method**: GET
* **Accept**: application/json
* **URL**: https://api.storyclm.com/v1/mediafiles/{mediafileId}
* **URL параметры**:
  * **\{ mediafileId:int }** - идентификатор медиафайла;

**Пример**: https://api.storyclm.com/v1/mediafiles/118

**Пример ответа:**

* **Content Type**: application/json; charset=utf-8
* **Тело ответа**:

```JSON
{
  "id": 118,
  "revision": 0
  "fileName": "mediafile1.pdf",
  "title": "mediafile1.pdf",
  "blobId": "bac2b6191ed0433a878603d5c469da9a68f83753a48f44ec82568ad3bc571d48",
  "fileSize": 721878,
  "mimeType": "application/pdf",
  "created": "2016-12-27T11:06:52.19",
  "updated": "2016-12-27T11:06:54.19",
  "sas": "https://stagingclmsstorage.blob.core.windows.net/mediafiles/bac2b6191ed0433a878603d5c469da9a68f83753a48f44ec82568ad3bc571d48?sv=2016-05-31&sr=b&sig=KZJq7RR7%2BjLot3YhIRTtUlZkRzgalE9IeOMgg3mojko%3D&st=2017-07-20T18%3A33%3A34Z&se=2017-07-21T04%3A38%3A34Z&sp=r",
  "isAvailableForSharing": false,
}
```
**Результат** - объект "Медиафайл". Объект содержит следующие поля:

* **id** - уникальный идентификатор медиафайла в системе;
* **revision** - ревизия. Используется для синхронизации. При каждом изменении объекта поле увеличивается на единицу;
* **fileName** - имя файла в файловой системе;
* **title** - название медиафайла;
* **blobId** - идентификатор медиафайла в хранилище;
* **fileSize** - размер медиафайла в байтах;
* **mimeType** - тип файла;
* **created** - дата создания;
* **updated** - дата обновления;
* **sas** - ссылка на скачивание. Ссылка активна один час.
* **isAvailableForSharing** - дает возможность пользователю пересылать медифайл;

### Slide

Получает слайд по идентификатору.

**Запрос:**

* **Method**: GET
* **Accept**: application/json
* **URL**: https://api.storyclm.com/v1/slides/{slideId}
* **URL параметры**:
  * **\{ slideId:int }** - идентификатор слайда;

**Пример**: https://api.storyclm.com/v1/slides/2140

**Пример ответа:**

* **Content Type**: application/json; charset=utf-8
* **Тело ответа**:

```JSON
{
  "id": 2140,
  "revision": 0
  "name": "10.html",
  "pageSource": "77u/PCFET0NUWVBFIGh0bWw+DQo8aHRtbCBsYW5nPSJydSI+DQo8aGVhZD4NCiAgICA8bWV0YSBjaGFyc2V0PSJ1dGYtOCI+DQogICAgPG1ldGEgbmFtZT0idmlld3BvcnQiIGNvbnRlbnQ9IndpZHRoPWRldmljZS13aWR0aCwgaW5pdGlhbC1zY2FsZT0xLjAsIG1heGltdW0tc2NhbGU9MS4wIj4NCiAgICA8bWV0YSBuYW1lPSJhcHBsZS1tb2JpbGUtd2ViLWFwcC1zdGF0dXMtYmFyLXN0eWxlIiBjb250ZW50PSJibG",
  "linkedSlides": "9.html,11.html",
  "swipeNext": "11.html",
  "swipePrevious": "9.html",
  "created": "2016-12-27T11:09:17.32",
  "updated": "2016-12-27T11:09:18.467",
}
```
**Результат** - объект "Слайд". Объект содержит следующие поля:

* **id** - уникальный идентификатор слайда в системе;
* **revision** - ревизия. Используется для синхронизации. При каждом изменении объекта поле увеличивается на единицу;
* **name** - название слайда в файловой системе;
* **pageSource** - содержимое слайда в формате Base64;
* **linkedSlides** - связные слайды. Используется для построения карты;
* **swipeNext** - следующий салйд. Используется для построения карты;
* **swipePrevious** - предыдущий слайд. Используется для построяния карты;
* **created** - дата создания;
* **updated** - дата обновления;

### Сontentpackage

Получает пакет с ассетами.

**Запрос:**

* **Method**: GET
* **Accept**: application/json
* **URL**: https://api.storyclm.com/v1/contentpackages/{presentationId}
* **URL параметры**:
  * **\{ presentationId:int }** - идентификатор презентации;

**Пример**: https://api.storyclm.com/v1/contentpackages/17

**Пример ответа:**

* **Content Type**: application/json; charset=utf-8
* **Тело ответа**:

```JSON
{
  "id": 16,
  "revision": 1,
  "sas": "https://stagingclmsstorage.blob.core.windows.net/packages/b43e293b66c349309dd9b4fd38c540b39aaba6aba74f488c9538ce8a84864d5d?sv=2016-05-31&sr=b&sig=DMhk3OlGNyBOrqr4hmj%2BqhN85BKeKPP2faXX5r0NZsM%3D&st=2017-07-20T19%3A10%3A55Z&se=2017-07-21T05%3A15%3A55Z&sp=r",
  "blobId": "b43e293b66c349309dd9b4fd38c540b39aaba6aba74f488c9538ce8a84864d5d",
  "fileSize": 9203268,
  "mimeType": "application/zip",
  "created": "2016-12-27T11:06:53.22",
  "updated": "2016-12-27T11:09:25.12"
}
```
**Результат** - объект "Пакет". Объект содержит следующие поля:

* **id** - уникальный идентификатор пакета в системе;
* **revision** - ревизия. Используется для синхронизации. При каждом изменении объекта поле увеличивается на единицу;
* **blobId** - идентификатор пакета в хранилище;
* **fileSize** - размер пакета в байтах;
* **mimeType** - тип файла;
* **created** - дата создания;
* **updated** - дата обновления;
* **sas** - ссылка на скачивание. Ссылка активна один час;
