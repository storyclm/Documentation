# Content

The notion of "content" in StoryCLM is based on an interactive presentation (application). Applications for StoryCLM are web-applications created with the use of such web technologies as HTML, CSS and JavaScript. Applications consist of slides, media files and assets packages. Each application is located in the StoryCLM client. To gain access to the content via API ones has to have the necessary rights in the client to which the application belongs. Apart from having the rights, both the client and the application must be active

* **Server** - api.storyclm.com
* **Supported clients** -  working on behalf of the user, working on behalf of the service. 


### Clients

List of available clients.

**Request:**

* **Method**: GET
* **Accept**: application/json
* **URL**: https://api.storyclm.com/v1/clients

**Example**: https://api.storyclm.com/v1/clients

**Example of response:**

* **Content Type**: application/json; charset=utf-8
* **The body of response:**

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
The result is the "Client"collection of objects. Every object of the collection contains the following fields:

* **id** - the unique client ID;
* **name** - the name of the client;
* **lockoutEnabled** - blocking;
* **shortDescription** - short description;
* **longDescription** - description;
* **thumbImgId** - URL of the background image; 
* **imgId** - URL of the logo; 
* **url** - the company's website;
* **email** - email of the contact person;
* **created** - date of creation;
* **updated** - date of the last update;
* **deviceLogTable** - the identifier of the table in which the system log is written;
* **baseStatisticsTable** - the identifier of the table in which application statistics are written;
* **geolocationTable** - the identifier of the table in which geodata are written;
* **presentations** - the list of presentations. It is a collection of simplified objects describing the presentation;
  * **debug** - presentation in the development mode;
  * **skip** - do no sync the presentation;
  * **lockout** - the presentation has been blocked; 
  * **id** - unique identifier;
  * **revision** - revision. Used for synchronization. With each change of object the field is increased by one;
* **users** - the list of users. It is a collection of simplified objects describing the user;
  * **id** - the identifier of the user;
  * **role** - the role of the user in the client;
* **groups** -  list of groups. It is a collection of simplified objects that describe a group of users;
  * **users** - a list of user IDs in the group;
  * **id** - the identifier of the group;
  * **name** - the name of the group;
* **tables** - list of tables. It is a collection of simplified objects that describe the table;
  * **id** - the identifier of the table;
  * **name** - the name of the table; 


### Client

Received by the client through ID. 

**Request:**

* **Method**: GET
* **Accept**: application/json
* **URL**: https://api.storyclm.com/v1/clients/{clientid}
* **URL параметры**:
  * **\{ clientid:int }** - client ID;

**Example**: https://api.storyclm.com/v1/clients/1

**Example of response:**

* **Content Type**: application/json; charset=utf-8
* **The body of response:**

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

Receives the presentation through ID. 

**Request:**

* **Method**: GET
* **Accept**: application/json
* **URL**: https://api.storyclm.com/v1/presentations/{presentationId}
* **URL параметры**:
  * **\{ presentationId:int }** - presentation ID;

**Example**: https://api.storyclm.com/v1/presentations/17

**Example of response:**

* **Content Type**: application/json; charset=utf-8
* **The body of response:**

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
**The resulting** - object "Presentation" contains the following fields:

* **id** - the unique ID of presentation;
* **name** -  the name of the presentation;
* **shortDescription** - short description;
* **longDescription** - description;
* **thumbImgId** - icon;
* **imgId** - logo;
* **order** -  "weight", used to organise the list;
* **revision** -  revision. Used when synchronysing. With each change of object the field is increased by one;
* **created** - date of creation;
* **updated** -  date edited;
* **clientId** - the ID of the client whose presentation it is;
* **debugModeEnabled** - development mode;
* **skip** - skip sync;
* **mapEnabled** - map enabled. It means the presentation is using the map;
* **mapType** - map type;
* **needConfirmation** - ask for confirmation when exiting the presentation;
* **previewMode** - preview mode;
* **map** - map;
* **visibility** - show or hide the presentation;
* **sourcesFolder** - the assets package;
  * **id** - the package ID;
  * **blobId** - the name of the package;
  * **fileSize** - the package size in bytes;
  * **mimeType** - package tupe, usually a zip archive;
  * **revision** - revision. Used when synchronysing. With each change of object the field is increased by one;
  * **created** - the date package was created;
  * **updated** - the date package was last uploaded;
* **mediaFiles** -  the list of media files. It is a collection of simplified objects describing the media file; 
  * **fileSize** - file size in bytes;
  * **id** - the unique ID of the media file;
  * **revision** - revision. Used when synchronysing. With each change of object the field is increased by one;
* **slides** -  list of slides. It is a collection of simplified objects describing a slide;
  * **id** - slide ID;
  * **revision** - revision. Used when synchronysing. With each change of object the field is increased by one;
* **presentations** - the list of presentations required for the correct work of the current presentation.
* **users** - the list of presentation users. It is a collection of simplified objects describing the user;
  * **id** - user ID;
  * **role** - user's role;

### Get Presentation Users

Gets the list of users who have access to the presentation. The presentation must be active.

*To access the resource the scope "users" must be enabled.*

*The presentation has to be in the same client in which the account was created.*

**Request:**

* **Method**: GET
* **Accept**: application/json
* **URL**: https://api.storyclm.com/v1/presentations/{presentationId}/users
* **URL параметры**:
  * **\{ presentationId:int }** - presentation ID;

**Example**: https://api.storyclm.com/v1/presentations/17/users

**Example of response:**

* **Content Type**: application/json; charset=utf-8
* **The body of response:**

```JSON
[
  {
    "id": "77b638b2-9eac-413a-8715-5401ef811fbf",
    "role": 0,
    "revision": 0
  },
  {
    "id": "3d320152-2b38-4b51-9939-0b2f96d23759",
    "role": 0,
    "revision": 0
  }
]
```

### Add Users To Presentation

It gives a group of users access to the presentation. The presentation must be active. Rights can not be given to users "Project Manager", "Account Manager" or users who do not belong to the client to which the presentation belongs. Also, access can not be given to users who already have access rights. When being added as a group, only the users meeting those criteria will be added. As a result, a list of all users who have access to the presentation will be displayed. The list allows to check which users have been added.

*To access the resource the scope "users" must be enabled.*

*The presentation has to be in the same client in which the account was created.*

**Request:**

* **Method**: POST
* **Accept**: application/json
* **URL**: https://api.storyclm.com/v1/presentations/{presentationId}/users
* **URL параметры**:
  * **\{ presentationId:int }** - presentation ID;

**Тело запроса:**
``` json
[
	"3975f964-e93e-4df3-814b-ae8df9bf741f",
	"77b638b2-9eac-413a-8715-5401ef811fbf",
	"3d320152-2b38-4b51-9939-0b2f96d23759"
]
```

**Example**: https://api.storyclm.com/v1/presentations/17/users

**Example of response:**

* **Content Type**: application/json; charset=utf-8
* **The body of response:**

```JSON
[
  {
    "id": "77b638b2-9eac-413a-8715-5401ef811fbf",
    "role": 0,
    "revision": 0
  },
  {
    "id": "3d320152-2b38-4b51-9939-0b2f96d23759",
    "role": 0,
    "revision": 0
  }
]
```
### Remove Users From Presentation

Denies access to the presentation to a group of users. The presentation must be active. Only those users who already have access to the presentation can have the access limited. As a result, a list of all users who have access to the presentation will be displayed. The list allows to check which users have been denied access.

*To access the resource the scope "users" must be enabled.*

*The presentation has to be in the same client in which the account was created.*

**Request:**

* **Method**: DELETE
* **Accept**: application/json
* **URL**: https://api.storyclm.com/v1/presentations/{presentationId}/users?users={userId}&users={userId}
* **URL параметры**:
  * **\{ presentationId:int }** - идентификатор презентации;
  * **\{ userId:string }** - идентификатор пользователя;

**Example**: https://api.storyclm.com/v1/presentations/17/users?users=3975f964-e93e-4df3-814b-ae8df9bf741f&users=3d320152-2b38-4b51-9939-0b2f96d23759

**Example of response:**

* **Content Type**: application/json; charset=utf-8
* **The body of response:**

```JSON
[
  {
    "id": "77b638b2-9eac-413a-8715-5401ef811fbf",
    "role": 0,
    "revision": 0
  }
]
```
### Synchronize Presentation Users

It gives a group of users access to the presentation according to the given list. Only the listed users will be granted access. Users who are not on the list but who have the necessary rights will be denied the right to access. If there are users without access rights on the list, they will be given the rights. No change of rights will be applied to users who are on the list and who already have access. The presentation must be active. 

Access rights can not be changed for users "Project Manager", "Account Manager" or users who do not belong to the client to which the presentation belongs. As a result a list of all users who have access to the presentation will be displayed. The list allows to check which users have been added.

*To access the resource the scope "users" must be enabled.*

*The presentation has to be in the same client in which the account was created.*

**Request:**

* **Method**: PUT
* **Accept**: application/json
* **URL**: https://api.storyclm.com/v1/presentations/{presentationId}/users
* **URL параметры**:
  * **\{ presentationId:int }** - идентификатор презентации;

**Тело запроса:**
``` json
[
	"77b638b2-9eac-413a-8715-5401ef811fbf",
	"3d320152-2b38-4b51-9939-0b2f96d23759"
]
```
**Example**: https://api.storyclm.com/v1/presentations/17/users

**Example of response:**

* **Content Type**: application/json; charset=utf-8
* **The body of response:**

```JSON
[
  {
    "id": "77b638b2-9eac-413a-8715-5401ef811fbf",
    "role": 0,
    "revision": 0
  },
  {
    "id": "3d320152-2b38-4b51-9939-0b2f96d23759",
    "role": 0,
    "revision": 0
  }
]
```
### Mediafile

Receives a media file through ID. 

**Request:**

* **Method**: GET
* **Accept**: application/json
* **URL**: https://api.storyclm.com/v1/mediafiles/{mediafileId}
* **URL параметры**:
  * **\{ mediafileId:int }** - medifile ID;

**Example**: https://api.storyclm.com/v1/mediafiles/118

**Example of response:**

* **Content Type**: application/json; charset=utf-8
* **The body of response:**

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
**Result** - the resulting object "Mediafile" has the following fields:

* **id** - the unique ID of the media file in the system; 
* **revision** - revision. Used when synchronysing. With each change of object the field is increased by one;
* **fileName** - name of the file in the file system; 
* **title** - the title of the media file;
* **blobId** - the file identifier in storage; 
* **fileSize** - the package size in bytes;
* **mimeType** - type of the file;
* **created** - date of creation;
* **updated** - date updated;
* **sas** - link to download. Remains active for one hour;
* **isAvailableForSharing** - gives the user a possibility to send the media file on;

### Slide

Receives a slide through ID. 

**Request:**

* **Method**: GET
* **Accept**: application/json
* **URL**: https://api.storyclm.com/v1/slides/{slideId}
* **URL параметры**:
  * **\{ slideId:int }** - slide ID;

**Example**: https://api.storyclm.com/v1/slides/2140

**Example of response:**

* **Content Type**: application/json; charset=utf-8
* **The body of response:**
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
**Result** - The resulting object is "Slide". The object contains the following fields:

* **id** - unique identifier of the slide in the system; 
* **revision** - revision. Used for synchronization. With every change of the object the field is increased by one;
* **name** - the name of the slide in the file system;
* **pageSource** - the contents of the slide in the Base64 format;
* **linkedSlides** - connected slides. Used to build a map;
* **swipeNext** - the next slide. Used to build a map;
* **swipePrevious** - the previous slide. Used to build a map;
* **created** - date of creation;
* **updated** - date updated;

### Сontentpackage

Gets the assets package.

**Request:**

* **Method**: GET
* **Accept**: application/json
* **URL**: https://api.storyclm.com/v1/contentpackages/{presentationId}
* **URL параметры**:
  * **\{ presentationId:int }** - presentation ID;

**Example**: https://api.storyclm.com/v1/contentpackages/17

**Example of response:**

* **Content Type**: application/json; charset=utf-8
* **The body of response:**

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
**Result** - the resulting object is "Package". The object contains the following fields:

* **id** - unique identifier of the package in the system; 
* **revision** - - revision. Used for synchronization. With every change of the object the field is increased by one;
* **blobId** -  the identifier of the package in thestorage;
* **fileSize** - the size of the packet in bytes;
* **mimeType** - the type of the file;
* **created** - creation date;
* **updated** - update date;
* **sas** - download link. The link remains active for one hour;
