
# [REST API](https://ru.wikipedia.org/wiki/REST)

## Аутентификация и авторизация

API StoryCLM представляет из себя совокупность ресурсов связанных между собой по средствам шины сообщений. Каждый ресурс - это отдельный, независимый от других сервис, который имеет свою логику, структуру данных и решает определенную бизнес задачу. В рамках своей бизнес задачи ресурс полностью самодостаточен. Ресурсы обмениваются данными между собой и воркерами по средствам шины сообщений.

Потребителем ресурсов явлются клиенты. Клиент - это приложение, сайт или другая система которая взаимодействует со StoryCLM через API от своего имени или от имени пользователя StoryCLM. В зависимости от задач, клиент самостоятельно выбирает необходимые ему ресурсы обращаясь к ним, и, тем самым, решая свои задачи интеграции. Для того что бы клиент не авторизовывался на каждом ресурсе в StoryCLM используется Single Sign-On или "Технология единого входа". Эта технология позволяет клиенту обращаться к разным ресурсам без повторной аутентификации на каждом из них. 

В StoryCLM SSO (Single Sign-On) реализуется средствами OpenID Connect. OpenID Connect - открытый стандарт децентрализованной системы аутентификации, предоставляющей пользователю возможность создать единую учётную запись для аутентификации на множестве не связанных друг с другом ресурсов, используя услуги сервера авторизации (более подробная информация). Доступ к ресурсам StoryCLM предоставляется по JWT токенам. При каждом обращении к ресурсу или установлении realtime соединения, токен нужно передавать в заголовке запроса. Токен выдает сервер аутентификации - auth.storyclm.com. Правила выдачи и обновления токена, а так же другие моменты касающиеся правил аутентификации в StoryCLM описаны в конфигурации OpenId Connect. Конфигурация OpenId Connect для StoryCLM находится по адресу https://auth.storyclm.com/.well-known/openid-configuration.  

Принципиальная схема взаимодействия клиентов и ресурсов, а так же ресурсов между собой и вокерами через шину обмена сообщениями:

![s](images/rest/1.png)

## Настройка 

Для того что бы получить доступ к ресурсам StoryCLM, на панели администрирования нужно зарегистрировать приложение, настроить тип клиента и доступ у нужным ресурсам. Приложение - это совокупность учетных данных и набор ресурсов, к которым приложение может получить доступ.

Консоль управления приложениями находится во вкладке "Приложения" раздела "Интеграция" клиента.

![s](images/rest/2.png)

В таблице отображается список уже созданных приложений.

![s](images/rest/3.png)

Для того что бы создать новое приложение, нужно нажать на кнопку "Новое приложение". Появится форма создания нового приложения.

![s](images/rest/4.png)

Форма состоит из следующих полей:

 1. Название - обычно совпадает с названием приложения, которое будет использовать эти учетные данные.
 2. Enabled - включает или отключает доступ. Это означает что по этим учетным данным сервер аутентификации перестанет выдавать новые токены доступа. Токены, которые уже были выданы продолжат функцианировать до истечения их срока действия.
 3. Type - тип приложения, описывает способ аутентификации на сервере.
 4. Scopes - ресурсы, которые будут доступны приложению по ключу доступа. Разные ресурсы работают с разными типами приложений по-разному. Одни могут давать возможность взаимодействовать с ним от имени пользователя, другие только от имени сервиса. Некоторые ресурсы позволяют взаимодействовать с ними всем типам приложений, но например, если клиент взаимодействует от имени пользователя, то он получит один набор данных а клиент работающий от имени сервиса получит другой. Узнать как именно ресурсы работают с разными типами клиентов можно узнать в документации к самому ресурсу.


После создания приложения оно появится в списке. Приложение можно удалить или отредактировать, а так же, получить ключи доступа в виде пары client ID и secret.

![s](images/rest/5.png)

Что бы получить доступ к ресурсам StoryCLM, нужно авторизоваться и получить токен доступа. В противном случае, без токена ресурс будет отвечать сообщением с кодом 401 (Unauthorized). Существуют разные типы аутентификации. Тип аутентификации зависит от типа приложения. 

### Типы приложений и аутентификация

В StoryCLM в роли клиента может быть веб приложение, сервис, мобильное или настольное приложение. В зависимости от этого клиент может совершать операции от своего имени или от имени пользователя StoryCLM. 

**Service**. В роли клиента выступает другой сервис. Используется для интеграции StoryCLM с другой системой. Клиент получает доступ к ресурсам только в рамках клиента StoryCLM. Для получения токена доступа потребуется только ClientId и Secret. Это самый простой и небезопасный способ из всех. Для того что бы получить токен нужно выполнить запрос:

Пример запроса:

```
POST /connect/token HTTP/1.1
Host: auth.storyclm.com/connect/token
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials
&client_id=client_1_1
&client_secret=e3f8314c34073e4509b16f1125ed5d7b47fcb8fac2291b495eb01bad4a0fb5f9e543
```

Пример ответа:

```
{
  "access_token": "eyJhbGciOiJSUzI1NiIsImtpZCI6IjZjZTc1ZGMxMTFmMWY3YTNkODkwZTU0MTgzMjViNGZlIiwidHlwIjoiSldUIn0.eyJuYmYiOjE1MDAzMzQ5MjgsImV4cCI6MTUwMDMzODUyOCwiaXNzIjoiaHR0cHM6Ly9sb2NhbGhvc3Q6NDQzMzEiLCJhdWQiOlsiaHR0cHM6Ly9sb2NhbGhvc3Q6NDQzMzEvcmVzb3VyY2VzIiwiY29udGVudCIsIm15byIsInRhYmxlcyJdLCJjbGllbnRfaWQiOiJjbGllbnRfMV8xIiwic2NvcGUiOlsiY29udGVudCIsIm15byIsInRhYmxlcyJdfQ.Cm9mQe458lXuxzV5lAE6wMlXVE7u3aZRwEnpK6g9gnp9B9mwKnml24QgusKqKUCkFZ8_rboFqYz7lguluBTiO75EZO0J7Npm9s41Mnv9AEuSAcfaJuqqdi9vIxTSddxJFZ2QDJvAmQMrp_A5SfPeqNzsxZ2gcry3YbJTxwxu5R_2J4yCIHRI0930Qu_lM57YNcxgYOGOQ4WNJT4OAru1IlO2MYbaCYp7a5OqH93tzV_LlYFTvNL_ppceuZrxkENHzmV_Jo-Rryx4ICjgmEpXYOfLXufGZqZUPe98hGl4zMkPaIppso5Qh6usi1UNrfzVEC6Qd3RlE6rQ0dQ5lDSv1A",
  "expires_in": 3600,
  "token_type": "Bearer"
}
```

**Application**. В роли клиента выступает мобильное или настольное приложение. Клиент взаимодействует с ресурсами StoryCLM от имени пользователя StoryCLM. Для получения токена доступа потребуется ClientId, Secret, Username и Password. Для того что бы получить токен нужно выполнить запрос:

Пример запроса:

```
POST /connect/token HTTP/1.1
Host: auth.storyclm.com/connect/token
Content-Type: application/x-www-form-urlencoded

grant_type=password
&username=rsk-k1361%40test.ru
&password=password%23
&client_id=client_1_4
&client_secret=ce200179f3dd344ca3896a144550996b82092c0e5ab976d0d495cafbd0a84b2fa3bc6
```

Пример ответа:

```
{
  "access_token": "eyJhbGciOiJSUzI1NiIsImtpZCI6Ijc35YWVkYThmZWM4M2I1NDhmNzU4ZTBjYWM5NzMxZTQ1IiwidHlwIjoiSldUIn0.eyJuYmYiOjE1MDAzNzc2MjksImV4cCI6MTUwMDM4MTIyOSwiaXNzIjoiaHR0cHM6Ly9sb2NhbGhvc3Q6NDQzMzEiLCJhdWQiOlsiaHR0cHM6Ly9sb2NhbGhvc3Q6NDQzMzEvcmVzb3VyY2VzIiwiY29udGVudCIsIm15byIsInRhYmxlcyJdLCJjbGllbnRfaWQiOiJjbGllbnRfMV80Iiwic3ViIjoiYjFhZTI0OWItMjJjNC00YjBiLWE53ZWMtNjZmMDUyMWE0NzE1IiwiYXV0aF90aW1lIjoxNTAwMzc3NjI5LCJpZHAiOiJsb2NhbCIsIm5hbWUiOiJyc2stazE2MUB5YS5ydSIsImZ1bGxuYW1lIjoi0J_RgNC-0YLQvtC9INCf0YDQvtGC0L7QvdC-0LIiLCJyb2xlIjoidXNlciIsInJvbGVfY2xpZW50XzEiOiJ1c2VyIiwicm9sZV9jbGllbnRfMiI6InVzZXIiLCJzY29wZSI6WyJjb250ZW50IiwibXlvIiwidGFibGVzIiwib2ZmbGluZV9hY2Nlc3MiXSwiYW1yIjpbIiJdfQ.KjLIYZ4Jd33e6uXw1zuNylvB5KJCNcQRvgltBV56GcEzaKmxE9MgImF0ainj7eVfZJU9REipLw1Ni2l4aG7C2buEORhNYXX79-ZC4liJFFOCUsWv0pBA0jSonKxtT4FQGdXXkBQb2obqVYyinzsx-EX8Avs-V56Sh4iV4-3Se-rePVQ_1ZzEpFnw66e0cvX6PUYvjU-0GwaVlayEZBNizzQ7X6suKBOvk17-SaDTx0rtdIFEkkh_J0L9yPpICHacE2zgtxI6UHHKpC2BIrOGCMcNDGrh20O2otjygvQ0MATOm7T1Cb5gH4CdfN7AyIHh288uvX2L9moy_UaUm_Xo3w",
  "expires_in": 3600,
  "token_type": "Bearer",
  "refresh_token": "2f88f0cd342b9e0adca37c78cc27bf3e803b5544241acee5c7b14258110b584a7cfa"
}
```

**Website**. В роли клиента выступает веб сайт или веб приложение. Клиент взаимодействует с ресурсами StoryCLM от имени пользователя StoryCLM. Grant Type - code. Это самый безопасный и надежный способ аутентификации, но так же и самый сложный. Для разных языков программирования и фреймворков созданы свои провайдеры аутентификации для OpenID Connect. Следует использовать их для того что бы авторизоваться через StoryCLM. 


### Использование токена

Ответ от сервера приходит в формате Json.  Полученный объект может содержать следующие поля:

* access_token - токен доступа.
* expires_in - время жизни токена доступа в секундах.
* token_type - тип токена.
* refresh_token -  токен по которому можно получить новый токен доступа, выдается только в для типов приложения Web site и Application.

Теперь в каждый запрос к ресурсу, в заголовок, нужно добавлять access_token в формате:

```
Authorization: Bearer eyJhbGciOiJSUzI1NiIsImtpZCI6ImJlMjcxZjEwYmVlZWQ5OTEyMDQ...
```

Следует отметить, что токен доступа живет час. После чего от ресурса будет приходить код 401 (Unauthorized). Что бы избежать этого нужно получать новый токен до истечения срока действия текущего, в случае если тип приложения Service. В остальных случаях для получения нового токена доступа нужно использовать refresh_token. Дело в том, что токен обновления (refresh_token), в отличии от токена доступа, живет год и если токен доступа стал просроченный то можно не заставлять пользователя получить новый токен доступа, вводя пароль. Можно в фоновом режиме по токену обновления получить новый токен доступа.  Для того что бы получить новый токен доступа по refresh_token нужно выполнить запрос:

Пример запроса:

```
POST /connect/token HTTP/1.1
Host: auth.storyclm.com/connect/token
Content-Type: application/x-www-form-urlencoded

grant_type=refresh_token
&refresh_token=2f88f0cd42b9e0adca74c78cc27bf3e80b5544241ace4e5c7b1258110b584a7cfa
&client_id=client_1_4&
client_secret=ce200179f3dd4ca3896a15504996b82092c50eab976d0d495cafbd0a84b2fa3bc6
```

Пример ответа:

```
{
  "access_token": "eyJhbGciOiJSUzI1NiIsImtpZCI6Ijc5YWVkYThmZWM4M2I1NDhmNzU4ZTBjYWM5NzMxZTQ1IiwidHlwIjoiSldUIn0.eyJuYmYiOjE1MDAzNzc2MzgsImV4cCI6MTUwMDM4MTIzOCwiaXNzIjoiaHR0cHM6Ly9sb2NhbGhvc3Q6NDQzMzEiLCJhdWQiOlsiaHR0cHM6Ly9sb2NhbGhvc3Q6NDQzMzEvcmVzb3VyY2VzIi4wiY29udGVudCIsInRhYmxlcyIsIm15byJdLCJjbGllbnRfaWQiOiJjbGllbnRfMV80Iiwic3ViIjoiYjFhZTI0OWItMjJjNC00YjBiLWE5ZWMtNjZmMDUyMWE0NzE1IiwiYXV0aF90aW1lIjoxNTAwMzc3NjI5LCJpZHAiOiJsb2NhbCIsIm5hbWUiOiJyc2stazE2MUB5YS5ydSIsImZ1bGxuY3W1lIjoi0J_RgNC-0YLQvtC9INCf0YDQvtGC0L7QvdC-0LIiLCJyb2xlIjoidXNlciIsInJvbGVfY2xpZW50XzEiOiJ1c2VyIiwicm9sZV9jbGllbnRfMiI6InVzZXIiLCJzY29wZSI6WyJjb250ZW50IiwidGFibGVzIiwibXlvIiwib2ZmbGluZV9hY2Nlc3Mi4XSwiYW1yIjpbIiJdfQ.jGsZo2s16pQ-dVMq1krVZjUITIMoDdOMEHAb7cgy4XLzsc5lMYuJEYjAZlAUjQbnqChgT5QYBThcv-Mt8HRCFW3lxPZWgXxgVskZQDpRS8o75yISeq8kHpbDk1IugugmwLJLwvCh5NGMGT4hKLNtQA79NY-iJZwLXktACvt0Q7TbsvWPwK_C7dGcjAyXxgI_e1OhNu3e-iIjkb-Bfc_bX6OzTZfzGFDVBZwkPPyUr87i3k9m6ibhflKbdSYUlulOxM6-TMXvGs46oTJ5NraLo-gPsaZOEKeiYz_xuCERhpN9_tWyn-Hra-inSzo61g84G53einr7xOnbR1rszsOobg",
  "expires_in": 3600,
  "token_type": "Bearer",
  "refresh_token": "a0d139e1acb497f8640640f9d3c119b6d8cb3d2638912a6975193ba4e457f77ed89"
}
```

## Ресурсы

* [Таблицы](RESTAPI_TABLES.md)





