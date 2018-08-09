# CLM Analytics

This section of analytics relates to the demonstration of presentations and the data which are collected during the demonstration. Work with analytics is carried out within the same client in which user accounts were created.

The sample is made according to the local time of the presentation demonstration and not by the date the data arrived in the storage. If needed to sample by date of adding to the storage, then "Feed" methods are required that allow you to search the storage starting from the first entries to the last.

It is worth noting that most of the time the device works offline and stores data about visits locally. This means that data on visits can appear much later than the actual demonstration -  after the device gets access to the Internet. One should keep this in mind when uploading analytics.


* **Server** - api.storyclm.com
* **Supported clients** -  working on behalf of the user, working on behalf of the service. 
* **Scopes** - CLMAnalitycs-R.

### Sessions

Getting visitor statistics on presentations and users for a period of time for the client.

**Model:**
  * **SessionId** - Session ID.
  * **PresentationId** - Presentation ID.
  * **ClientId** - Client ID.
  * **Complete** - Completed demonstration.
  * **UserId** - user ID.
  * **Latitude** - the latitude of the demonstration venue.
  * **Longtitude** - the longitude of the demonstration venue.
  * **DateTime** - the date of the demonstration. Counting starts from the beginning of the demonstration.
  * **Duration** - the duration of the demonstration in seconds.
  * **Address** - the address where the demonstration was made.
  * **SlidesCount** - the number of slides shown during the demonstration.
  * **TimeZoneOffset** - time zone.

**Request**

* **Method:** GET
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/analitycs/clm/sessions?start={start}&finish={finish}&pids={pIds}&pids={pIds}&uids={uIds}&completeOnly={completeOnly}&skip={skip}&take={take}
* **URL parameters:**
  * **{ pIds:int[] }** - Collection of presentation identifiers. If no presentations are specified, then the sample will be made for all presentations of the client. Optional parameter.
  * **{ uIds:string[] }** - Collection of client user IDs. If users are not specified, then the selection will be made for all users of the client. Optional parameter.
  * **{ start:unixdate }** - The date after which the selection will be made. If the date is not specified, the selection will be made from the beginning of the collection. The date is given in the Unix Date format. Optional parameter.
  * **{ finish:unixdate }** - The date to which the selection will be made. If the date is not specified, the selection will be made until the end of the collection. The date is given in the Unix Date format. Optional parameter.
  * **{ completeOnly:bool }** - Only finished visits. Optional parameter. By default, all will be selected.
  * **{ skip:int }** - the number of entries to skip. The default is 0.
  * **{ take:int }** - the number of entries to be selected. The default is 100. The maximum is 1000.

**Example:** https://api.storyclm.com/v1/analitycs/clm/sessions?skip=0&take=100

**Example:** https://api.storyclm.com/v1/analitycs/clm/sessions?start=1514764800&finish=1522540800&skip=0&take=100

**Example:** https://api.storyclm.com/v1/analitycs/clm/sessions?start=1514764800skip=0&take=100

**Example:** https://api.storyclm.com/v1/analitycs/clm/sessions?uids=b1ae249b-22c4-4b0b-a9ec-66f0521a4715&uids=fe84233b-0f47-

**Example:** https://api.storyclm.com/v1/analitycs/clm/sessions?pids=17&pids=4&uids=b1ae249b-22c4-4b0b-a9ec-66f0521a4715&uids=fe84233b-0f47-4a7e-9ad8-bec78f4b5857&skip=0&take=100

**Request example:**

* **Content Type:** application/json; charset=utf-8
* **Response body:**
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

Getting visitor statistics on presentations and users for a period of time for the client after the specified date.

Data are selected not by the actual date of the demonstration, but by the time data arrived on the server.

**Model:**
  * **SessionId** - Session ID.
  * **PresentationId** - Presentation ID.
  * **ClientId** - Client ID.
  * **Complete** - Completed demonstration.
  * **UserId** - user ID.
  * **Latitude** - the latitude of the demonstration venue.
  * **Longtitude** - the longitude of the demonstration venue.
  * **DateTime** - the date of the demonstration. Counting starts from the beginning of the demonstration.
  * **Duration** - the duration of the demonstration in seconds.
  * **Address** - the address where the demonstration was made.
  * **SlidesCount** - the number of slides shown during the demonstration.
  * **TimeZoneOffset** - time zone.

**Request**

* **Method:** GET
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/analitycs/clm/sessions/feed?date={date}&pids={pIds}&pids={pIds}&uids={uIds}&completeOnly={completeOnly}&skip={skip}&take={take}
* **URL parameters:**
  * **{ pIds:int[] }** - Collection of presentation identifiers. If no presentations are specified, then the sample will be made for all presentations of the client. Optional parameter.
  * **{ uIds:string[] }** - Collection of client user IDs. If users are not specified, then the selection will be made for all users of the client. Optional parameter.
  * **{ date:unixdate }** - The date after which the selection will be made. If the date is not specified, the selection will be made from the beginning of the collection. The date is given in the Unix Date format. Optional parameter.
  * **{ completeOnly:bool }** - Only finished visits. Optional parameter. By default, all will be selected.
  * **{ skip:int }** - the number of entries to skip. The default is 0.
  * **{ take:int }** - the number of entries to be selected. The default is 100. The maximum is 1000.

**Example:** https://api.storyclm.com/v1/analitycs/clm/sessions/feed?skip=0&take=100

**Example:** https://api.storyclm.com/v1/analitycs/clm/sessions/feed?date=1514764800&skip=0&take=100

**Example:** https://api.storyclm.com/v1/analitycs/clm/sessions/feed?uids=b1ae249b-22c4-4b0b-a9ec-66f0521a4715&uids=fe84233b-0f47-

**Example:** https://api.storyclm.com/v1/analitycs/clm/sessions/feed?pids=17&pids=4&uids=b1ae249b-22c4-4b0b-a9ec-66f0521a4715&uids=fe84233b-0f47-4a7e-9ad8-bec78f4b5857&skip=0&take=100

**Request example:**

* **Content Type:** application/json; charset=utf-8
* **Response body:**
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

Obtaining the number of visits for the client on presentations and users over a period of time.

**Request**

* **Method:** GET
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/analitycs/clm/sessions/count?start={start}&finish={finish}&pids={pIds}&pids={pIds}&uids={uIds}&completeOnly={completeOnly}
* **URL parameters:**
  * **{ pIds:int[] }** - Collection of presentation identifiers. If no presentations are specified, then the sample will be made for all presentations of the client. Optional parameter.
  * **{ uIds:string[] }** - Collection of client user IDs. If users are not specified, then the selection will be made for all users of the client. Optional parameter.
  * **{ start:unixdate }** - The date after which the selection will be made. If the date is not specified, the selection will be made from the beginning of the collection. The date is given in the Unix Date format. Optional parameter.
  * **{ finish:unixdate }** - The date to which the selection will be made. If the date is not specified, then the selection will be made until the end of the collection. The date is given in the Unix Date format. Optional parameter.
  * **{ completeOnly:bool }** - Only finished visits. Optional parameter. By default, all will be selected.

**Example:** https://api.storyclm.com/v1/analitycs/clm/sessions/count

**Example:** https://api.storyclm.com/v1/analitycs/clm/sessions/count?start=1514764800&finish=1522540800

**Example:** https://api.storyclm.com/v1/analitycs/clm/sessions/count?start=1514764800

**Example:** https://api.storyclm.com/v1/analitycs/clm/sessions/count?uids=b1ae249b-22c4-4b0b-a9ec-66f0521a4715&uids=fe84233b-0f47

**Example:** https://api.storyclm.com/v1/analitycs/clm/sessions/count?pids=17&pids=4&uids=b1ae249b-22c4-4b0b-a9ec-66f0521a4715&uids=fe84233b-0f47-4a7e-9ad8-bec78f4b5857

**Request example:**

* **Content Type:** application/json; charset=utf-8
* **Response body:**
``` json
{
    "count": 2822
}
```
### Custom Events

Receiving custom presentations events for users for a period of time.

**Model:**
  * **SessionId** - Session ID.
  * **PresentationId** - Presentation ID.
  * **ClientId** - Client ID.
  * **UserId** - user ID.
  * **Key** - Key.
  * **Value** - Value.
  * **Created** - the date of the demonstration. Counting starts from the beginning of the demonstration.
  * **TimeZoneOffset** - time zone.

**Request**

* **Method:** GET
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/analitycs/clm/customevents?start={start}&finish={finish}&pids={pIds}&pids={pIds}&uids={uIds}&completeOnly={completeOnly}&skip={skip}&take={take}
* **URL parameters:**
  * **{ pIds:int[] }** - Collection of presentation identifiers. If no presentations are specified, then the sample will be made for all presentations of the client. Optional parameter.
  * **{ uIds:string[] }** - Collection of client user IDs. If users are not specified, then the selection will be made for all users of the client. Optional parameter.
  * **{ start:unixdate }** - The date after which the selection will be made. If the date is not specified, the selection will be made from the beginning of the collection. The date is given in the Unix Date format. Optional parameter.
  * **{ finish:unixdate }** - The date to which the selection will be made. If the date is not specified, then the selection will be made until the end of the collection. The date is given in the Unix Date format. Optional parameter.
  * **{ completeOnly:bool }** - Only finished visits. Optional parameter. By default, all will be selected.
  * **{ skip:int }** - the number of entries to skip. The default is 0.
  * **{ take:int }** - the number of entries to be selected. The default is 100. The maximum is 1000.

**Example:** https://api.storyclm.com/v1/analitycs/clm/customevents?skip=0&take=100

**Example:** https://api.storyclm.com/v1/analitycs/clm/customevents?start=1514764800&finish=1522540800&skip=0&take=100

**Example:** https://api.storyclm.com/v1/analitycs/clm/customevents?start=1514764800skip=0&take=100

**Example:** https://api.storyclm.com/v1/analitycs/clm/customevents?uids=b1ae249b-22c4-4b0b-a9ec-66f0521a4715&uids=fe84233b-0f47-

**Example:** https://api.storyclm.com/v1/analitycs/clm/customevents?pids=17&pids=4&uids=b1ae249b-22c4-4b0b-a9ec-66f0521a4715&uids=fe84233b-0f47-4a7e-9ad8-bec78f4b5857&skip=0&take=100

**Request example:**

* **Content Type:** application/json; charset=utf-8
* **Response body:**
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

Receiving custom presentations events for users after the specified date. 
The data are selected not by the actual dates of the demonstration, but by the time of data arrival on the server.

**Model:**
  * **SessionId** - Session ID.
  * **PresentationId** - Presentation ID.
  * **ClientId** - Client ID.
  * **UserId** - user ID.
  * **Key** - Key.
  * **Value** - Value.
  * **Created** - the date of the demonstration. Counting starts from the beginning of the demonstration.
  * **TimeZoneOffset** - time zone.

**Request**

* **Method:** GET
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/analitycs/clm/customevents/feed?date={date}&pids={pIds}&pids={pIds}&uids={uIds}&completeOnly={completeOnly}&skip={skip}&take={take}
* **URL parameters:**
  * **{ pIds:int[] }** - Collection of presentation identifiers. If no presentations are specified, then the sample will be made for all presentations of the client. Optional parameter.
  * **{ uIds:string[] }** - Collection of client user IDs. If users are not specified, then the selection will be made for all users of the client. Optional parameter.
  * **{ date:unixdate }** - The date after which the selection will be made. If the date is not specified, the selection will be made from the beginning of the collection. The date is given in the Unix Date format. Optional parameter.
  * **{ completeOnly:bool }** - Only finished visits. Optional parameter. By default, all will be selected.
  * **{ skip:int }** - the number of entries to skip. The default is 0.
  * **{ take:int }** - the number of entries to be selected. The default is 100. The maximum is 1000.

**Example:** https://api.storyclm.com/v1/analitycs/clm/customevents/feed?skip=0&take=100

**Example:** https://api.storyclm.com/v1/analitycs/clm/customevents/feed?date=1514764800&skip=0&take=100

**Example:** https://api.storyclm.com/v1/analitycs/clm/customevents/feed?uids=b1ae249b-22c4-4b0b-a9ec-66f0521a4715&uids=fe84233b-0f47-

**Example:** https://api.storyclm.com/v1/analitycs/clm/customevents/feed?pids=17&pids=4&uids=b1ae249b-22c4-4b0b-a9ec-66f0521a4715&uids=fe84233b-0f47-4a7e-9ad8-bec78f4b5857&skip=0&take=100

**Request example:**

* **Content Type:** application/json; charset=utf-8
* **Response body:**
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

Obtaining the number of visits for the client on presentations and users over a period of time.

**Request**

* **Method:** GET
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/analitycs/clm/customevents/count?start={start}&finish={finish}&pids={pIds}&pids={pIds}&uids={uIds}&completeOnly={completeOnly}
* **URL parameters:**
  * **{ pIds:int[] }** - Collection of presentation identifiers. If no presentations are specified, then the sample will be made for all presentations of the client. Optional parameter.
  * **{ uIds:string[] }** - Collection of client user IDs. If users are not specified, then the selection will be made for all users of the client. Optional parameter.
  * **{ start:unixdate }** - The date after which the selection will be made. If the date is not specified, the selection will be made from the beginning of the collection. The date is given in the Unix Date format. Optional parameter.
  * **{ finish:unixdate }** - The date to which the selection will be made. If the date is not specified, then the selection will be made until the end of the collection. The date is given in the Unix Date format. Optional parameter.
  * **{ completeOnly:bool }** - Only finished visits. Optional parameter. By default, all will be selected.

**Example:** https://api.storyclm.com/v1/analitycs/clm/customevents/count

**Example:** https://api.storyclm.com/v1/analitycs/clm/customevents/count?start=1514764800&finish=1522540800

**Example:** https://api.storyclm.com/v1/analitycs/clm/customevents/count?start=1514764800

**Example:** https://api.storyclm.com/v1/analitycs/clm/customevents/count?uids=b1ae249b-22c4-4b0b-a9ec-66f0521a4715&uids=fe84233b-0f47

**Example:** https://api.storyclm.com/v1/analitycs/clm/customevents/count?pids=17&pids=4&uids=b1ae249b-22c4-4b0b-a9ec-66f0521a4715&uids=fe84233b-0f47-4a7e-9ad8-bec78f4b5857

**Request example:**

* **Content Type:** application/json; charset=utf-8
* **Response body:**
``` json
{
    "count": 91
}
```
### Slides Demonstrations

Obtaining the statistics on slides demonstrations for the client on presentations and users over a period of time.

**Model:**
  * **SessionId** - Session ID.
  * **PresentationId** - Presentation ID.
  * **ClientId** - Client ID.
  * **SlideName** - Slide ID.
  * **UserId** - User ID.
  * **Duration** - Duration in seconds.
  * **Navigation** - Navigation type.
  * **DateTime** - the date of the demonstration. Counting starts from the beginning of the demonstration.

**Request**

* **Method:** GET
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/analitycs/clm/slidesdemonstrations?start={start}&finish={finish}&pids={pIds}&pids={pIds}&uids={uIds}&skip={skip}&take={take}
* **URL parameters:**
  * **{ pIds:int[] }** - Collection of presentation identifiers. If no presentations are specified, then the sample will be made for all presentations of the client. Optional parameter.
  * **{ uIds:string[] }** - Collection of client user IDs. If users are not specified, then the selection will be made for all users of the client. Optional parameter.
  * **{ start:unixdate }** - The date after which the selection will be made. If the date is not specified, the selection will be made from the beginning of the collection. The date is given in the Unix Date format. Optional parameter.
  * **{ finish:unixdate }** - The date to which the selection will be made. If the date is not specified, then the selection will be made until the end of the collection. The date is given in the Unix Date format. Optional parameter.
  * **{ skip:int }** - the number of entries to skip. The default is 0.
  * **{ take:int }** - the number of entries to be selected. The default is 100. The maximum is 1000.

**Example:** https://api.storyclm.com/v1/analitycs/clm/slidesdemonstrations?skip=0&take=100

**Example:** https://api.storyclm.com/v1/analitycs/clm/slidesdemonstrations?start=1514764800&finish=1522540800&skip=0&take=100

**Example:** https://api.storyclm.com/v1/analitycs/clm/slidesdemonstrations?start=1514764800skip=0&take=100

**Example:** https://api.storyclm.com/v1/analitycs/clm/slidesdemonstrations?uids=b1ae249b-22c4-4b0b-a9ec-66f0521a4715&uids=fe84233b-0f47-

**Example:** https://api.storyclm.com/v1/analitycs/clm/slidesdemonstrations?pids=17&pids=4&uids=b1ae249b-22c4-4b0b-a9ec-66f0521a4715&uids=fe84233b-0f47-4a7e-9ad8-bec78f4b5857&skip=0&take=100

**Request example:**

* **Content Type:** application/json; charset=utf-8
* **Response body:**
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

Getting slides demonstration statistics on presentations and users for a period of time for the client after the specified date.

Data are selected not by the actual date of the demonstration, but by the time data arrived on the server.

**Model:**
  * **SessionId** - Session ID.
  * **PresentationId** - Presentation ID.
  * **ClientId** - Client ID.
  * **SlideName** - Название слайда.
  * **UserId** - User ID.
  * **Duration** - Duration in seconds.
  * **Navigation** - Navigation type.
  * **DateTime** - the date of the demonstration. Counting starts from the beginning of the demonstration.

**Request**

* **Method:** GET
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/analitycs/clm/slidesdemonstrations/feed?date={start}&pids={pIds}&pids={pIds}&uids={uIds}&completeOnly={completeOnly}&skip={skip}&take={take}
* **URL parameters:**
  * **{ pIds:int[] }** - Collection of presentation identifiers. If no presentations are specified, then the sample will be made for all presentations of the client. Optional parameter.
  * **{ uIds:string[] }** - Collection of client user IDs. If users are not specified, then the selection will be made for all users of the client. Optional parameter.
  * **{ date:unixdate }** - The date after which the selection will be made. If the date is not specified, the selection will be made from the beginning of the collection. The date is given in the Unix Date format. Optional parameter.
  * **{ skip:int }** - the number of entries to skip. The default is 0.
  * **{ take:int }** - the number of entries to be selected. The default is 100. The maximum is 1000.

**Example:** https://api.storyclm.com/v1/analitycs/clm/slidesdemonstrations/feed?skip=0&take=100

**Example:** https://api.storyclm.com/v1/analitycs/clm/slidesdemonstrations/feed?date=1514764800&skip=0&take=100

**Example:** https://api.storyclm.com/v1/analitycs/clm/slidesdemonstrations/feed?uids=b1ae249b-22c4-4b0b-a9ec-66f0521a4715&uids=fe84233b-0f47-

**Example:** https://api.storyclm.com/v1/analitycs/clm/slidesdemonstrations/feed?pids=17&pids=4&uids=b1ae249b-22c4-4b0b-a9ec-66f0521a4715&uids=fe84233b-0f47-4a7e-9ad8-bec78f4b5857&skip=0&take=100

**Request example:**

* **Content Type:** application/json; charset=utf-8
* **Response body:**
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

Obtaining the number of slides demonstrations for the client on presentations and users over a period of time.

**Request**

* **Method:** GET
* **Accept:** application/json
* **URL**: https://api.storyclm.com/v1/analitycs/clm/slidesdemonstrations/count?start={start}&finish={finish}&pids={pIds}&pids={pIds}&uids={uIds}
* **URL parameters:**
  * **{ pIds:int[] }** - Collection of presentation identifiers. If no presentations are specified, then the sample will be made for all presentations of the client. Optional parameter.
  * **{ uIds:string[] }** - Collection of client user IDs. If users are not specified, then the selection will be made for all users of the client. Optional parameter.
  * **{ start:unixdate }** - The date after which the selection will be made. If the date is not specified, the selection will be made from the beginning of the collection. The date is given in the Unix Date format. Optional parameter.
  * **{ finish:unixdate }** - The date to which the selection will be made. If the date is not specified, then the selection will be made until the end of the collection. The date is given in the Unix Date format. Optional parameter.

**Example:** https://api.storyclm.com/v1/analitycs/clm/slidesdemonstrations/count

**Example:** https://api.storyclm.com/v1/analitycs/clm/slidesdemonstrations/count?start=1514764800&finish=1522540800

**Example:** https://api.storyclm.com/v1/analitycs/clm/slidesdemonstrations/count?start=1514764800

**Example:** https://api.storyclm.com/v1/analitycs/clm/slidesdemonstrations/count?uids=b1ae249b-22c4-4b0b-a9ec-66f0521a4715&uids=fe84233b-0f47

**Example:** https://api.storyclm.com/v1/analitycs/clm/slidesdemonstrations/count?pids=17&pids=4&uids=b1ae249b-22c4-4b0b-a9ec-66f0521a4715&uids=fe84233b-0f47-4a7e-9ad8-bec78f4b5857

**Request example:**

* **Content Type:** application/json; charset=utf-8
* **Response body:**
``` json
{
    "count": 100
}
```