
# [REST API](https://en.wikipedia.org/wiki/REST)

## Table of contents

* [Tables](RESTAPI_TABLES.md)
* [Content](RESTAPI_CONTENT.md)
* [Users](RESTAPI_USERS.md)
* [CLM Analytics](RESTAPI_CLMANALITYCS.md)

## Authentication and Authorisation

The StoryCLM API is a set of resources interconnected by message bus. Each resource serves a specific business task and represents a separate independent service with its own logic and data structure. While preforming its business task, the resource is completely self-sufficient. Resources exchange data with each other and web workers by the means of the service bus. 

The resources are consumed by clients. A client is an application, website or another system which interacts with StoryCLM through the API on its own behalf or on behalf of a StoryCLM user. Depending on the task, the client chooses necessary resources to access thus solving its integration tasks. For the client not to sign in for every StoryCLM resource, Single Sign-On technology is used. This technology makes it possible for the client to access different resources without reauthentication on each of them.

SSO (Single Sign-On) in StoryCLM is implemented by means of OpenID Connect. OpenID Connect is an open standard of a decentralized authentication protocol that gives the user a possibility to create a single account to sign in on a number of unrelated resources using the services of an authorization server (more detailed information). StoryCLM resources are accessible by JWT tokens. Each every time a resource is accessed or a realtime connection established, a token has to be sent in the request header. The token gives the authentication server - auth.storyclm.com. The rules for generating and refreshing tokens as well as other information concerning the authentication rules in StoryCLM is described in the OpenId Connect configuration. The OpenId Connect configuration for StoryCLM is located at https://auth.storyclm.com/.well-known/openid-configuration. 

The functional diagram of client-resource interaction as well as inter-resource interaction and interactions with web workers through a message bus: 

![s](images/rest/1.png)

## Configuration 

To gain access to StoryCLM resources, one needs to register the application on the control panel, select the client type and access to necessary resources. An application is a collection of user account details and a set of resources the application can access. 

The control panel for applications is located in the "Applications" tab of the "Integration" section of a client.

![s](images/rest/2.png)

The table contains a list of already created applications.

![s](images/rest/3.png)

In order to create a new application, you need to click on the "New Application" button. It will bring up a form for creating a new application.

![s](images/rest/4.png)

The form consists of the following fields:

 1. Name - usually is the same as the name of the application that will use the account.
 2. Enabled - enables or disables access, meaning that the authentication server will stop generating new access tokens for this account. Tokens that have already been given will remain valid until they expire.
 3. Type - the type of application. It refers to the authentication method on the server.
 4. Scopes - resources that will be available to the application by an access key. Different resources have a different way of working with various types of applications. Some of them allow to interact with it on behalf of the end user, others – only on behalf of the service. Some resources allow interaction with all types of applications, but if, for instance, the client interacts on behalf of the end user, it will be given one data array, while the client working on behalf of the service will receive a different one. Information on how resources work with different types of clients can be found in the documentation for the resource. 

After an application has been created, it appears on the list. The application can be deleted or edited, as well as get access keys as in the form of client ID and secret.

![s](images/rest/5.png)

To gain access to StoryCLM resources, one needs to log in and receive an access token. In case there is no token, the resource responds with error 401 (Unauthorized). There are different types of authentication depending on the type of application.

### Types of applications and authentication

In StoryCLM, the client can be represented by a web-based application, a service, a mobile or desktop application. Depending on this, the client can carry out operations on its own behalf or on behalf of the StoryCLM user.

**Service**. The client is another service. It is used to integrate StoryCLM with another system. The client gets access to resources only within the StoryCLM client. Only ClientId and Secret are required to receive the access token,. This is the simplest and most insecure method of all. For a token to be generated, a request has to be sent: 

Example of a request:

```
POST /connect/token HTTP/1.1
Host: auth.storyclm.com/connect/token
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials
&client_id=client_1_1
&client_secret=e3f8314c34073e4509b16f1125ed5d7b47fcb8fac2291b495eb01bad4a0fb5f9e543
```

Example of a response:

```
{
  "access_token": "eyJhbGciOiJSUzI1NiIsImtpZCI6IjZjZTc1ZGMxMTFmMWY3YTNkODkwZTU0MTgzMjViNGZlIiwidHlwIjoiSldUIn0.eyJuYmYiOjE1MDAzMzQ5MjgsImV4cCI6MTUwMDMzODUyOCwiaXNzIjoiaHR0cHM6Ly9sb2NhbGhvc3Q6NDQzMzEiLCJhdWQiOlsiaHR0cHM6Ly9sb2NhbGhvc3Q6NDQzMzEvcmVzb3VyY2VzIiwiY29udGVudCIsIm15byIsInRhYmxlcyJdLCJjbGllbnRfaWQiOiJjbGllbnRfMV8xIiwic2NvcGUiOlsiY29udGVudCIsIm15byIsInRhYmxlcyJdfQ.Cm9mQe458lXuxzV5lAE6wMlXVE7u3aZRwEnpK6g9gnp9B9mwKnml24QgusKqKUCkFZ8_rboFqYz7lguluBTiO75EZO0J7Npm9s41Mnv9AEuSAcfaJuqqdi9vIxTSddxJFZ2QDJvAmQMrp_A5SfPeqNzsxZ2gcry3YbJTxwxu5R_2J4yCIHRI0930Qu_lM57YNcxgYOGOQ4WNJT4OAru1IlO2MYbaCYp7a5OqH93tzV_LlYFTvNL_ppceuZrxkENHzmV_Jo-Rryx4ICjgmEpXYOfLXufGZqZUPe98hGl4zMkPaIppso5Qh6usi1UNrfzVEC6Qd3RlE6rQ0dQ5lDSv1A",
  "expires_in": 3600,
  "token_type": "Bearer"
}
```

**Application**. The client is a mobile or desktop application. The client interacts with StoryCLM resources on behalf of a StoryCLM end user. To obtain the access token ClientId, Secret, Username, and Password are required. In order to receive a token, you need to execute the query:

Example of a request:
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

Example of a response:
```
{
  "access_token": "eyJhbGciOiJSUzI1NiIsImtpZCI6Ijc35YWVkYThmZWM4M2I1NDhmNzU4ZTBjYWM5NzMxZTQ1IiwidHlwIjoiSldUIn0.eyJuYmYiOjE1MDAzNzc2MjksImV4cCI6MTUwMDM4MTIyOSwiaXNzIjoiaHR0cHM6Ly9sb2NhbGhvc3Q6NDQzMzEiLCJhdWQiOlsiaHR0cHM6Ly9sb2NhbGhvc3Q6NDQzMzEvcmVzb3VyY2VzIiwiY29udGVudCIsIm15byIsInRhYmxlcyJdLCJjbGllbnRfaWQiOiJjbGllbnRfMV80Iiwic3ViIjoiYjFhZTI0OWItMjJjNC00YjBiLWE53ZWMtNjZmMDUyMWE0NzE1IiwiYXV0aF90aW1lIjoxNTAwMzc3NjI5LCJpZHAiOiJsb2NhbCIsIm5hbWUiOiJyc2stazE2MUB5YS5ydSIsImZ1bGxuYW1lIjoi0J_RgNC-0YLQvtC9INCf0YDQvtGC0L7QvdC-0LIiLCJyb2xlIjoidXNlciIsInJvbGVfY2xpZW50XzEiOiJ1c2VyIiwicm9sZV9jbGllbnRfMiI6InVzZXIiLCJzY29wZSI6WyJjb250ZW50IiwibXlvIiwidGFibGVzIiwib2ZmbGluZV9hY2Nlc3MiXSwiYW1yIjpbIiJdfQ.KjLIYZ4Jd33e6uXw1zuNylvB5KJCNcQRvgltBV56GcEzaKmxE9MgImF0ainj7eVfZJU9REipLw1Ni2l4aG7C2buEORhNYXX79-ZC4liJFFOCUsWv0pBA0jSonKxtT4FQGdXXkBQb2obqVYyinzsx-EX8Avs-V56Sh4iV4-3Se-rePVQ_1ZzEpFnw66e0cvX6PUYvjU-0GwaVlayEZBNizzQ7X6suKBOvk17-SaDTx0rtdIFEkkh_J0L9yPpICHacE2zgtxI6UHHKpC2BIrOGCMcNDGrh20O2otjygvQ0MATOm7T1Cb5gH4CdfN7AyIHh288uvX2L9moy_UaUm_Xo3w",
  "expires_in": 3600,
  "token_type": "Bearer",
  "refresh_token": "2f88f0cd342b9e0adca37c78cc27bf3e803b5544241acee5c7b14258110b584a7cfa"
}
```

**Website**. The client is a web site or a web application. The client interacts with StoryCLM resources on behalf of the StoryCLM end user. Grant Type - code. This is the most secure and reliable authentication method, but at the same time the most complicated. For different programming languages ​​and frameworks there are different authentication providers for OpenID Connect. They are to be used for authorisation through StoryCLM.

### Using the token

The response from the server is in JSON format. The resulting object can contain the following fields:

* access_token - access token
* expires_in - lifetime of the token in seconds
* token_type - token type
* refresh_token - a token using which a new access token can be obtained. It is generated only for the Web site and Application application types

Now the header for every request to the resource has to contain access_token in the following format:

```
Authorization: Bearer eyJhbGciOiJSUzI1NiIsImtpZCI6ImJlMjcxZjEwYmVlZWQ5OTEyMDQ...
```
It has to be said that an access token is valid for one hour. After that the resource will response with code 401 (Unauthorized). To avoid this a new token has to be obtained before the current one expires, in case of Service application type. In other cases to obtain an access token you need to use refresh_token. The thing is that the refresh token (refresh_token), unlike the access token, is valid for a year and if the access token expires, there is no need to make the user receive a new access token by entering a password. A new access token can be obtained in the background with the update token. To get a new access token by refresh_token, you need to execute the query:

Example of a request:

```
POST /connect/token HTTP/1.1
Host: auth.storyclm.com/connect/token
Content-Type: application/x-www-form-urlencoded

grant_type=refresh_token
&refresh_token=2f88f0cd42b9e0adca74c78cc27bf3e80b5544241ace4e5c7b1258110b584a7cfa
&client_id=client_1_4&
client_secret=ce200179f3dd4ca3896a15504996b82092c50eab976d0d495cafbd0a84b2fa3bc6
```
Example of a response:
```
{
  "access_token": "eyJhbGciOiJSUzI1NiIsImtpZCI6Ijc5YWVkYThmZWM4M2I1NDhmNzU4ZTBjYWM5NzMxZTQ1IiwidHlwIjoiSldUIn0.eyJuYmYiOjE1MDAzNzc2MzgsImV4cCI6MTUwMDM4MTIzOCwiaXNzIjoiaHR0cHM6Ly9sb2NhbGhvc3Q6NDQzMzEiLCJhdWQiOlsiaHR0cHM6Ly9sb2NhbGhvc3Q6NDQzMzEvcmVzb3VyY2VzIi4wiY29udGVudCIsInRhYmxlcyIsIm15byJdLCJjbGllbnRfaWQiOiJjbGllbnRfMV80Iiwic3ViIjoiYjFhZTI0OWItMjJjNC00YjBiLWE5ZWMtNjZmMDUyMWE0NzE1IiwiYXV0aF90aW1lIjoxNTAwMzc3NjI5LCJpZHAiOiJsb2NhbCIsIm5hbWUiOiJyc2stazE2MUB5YS5ydSIsImZ1bGxuY3W1lIjoi0J_RgNC-0YLQvtC9INCf0YDQvtGC0L7QvdC-0LIiLCJyb2xlIjoidXNlciIsInJvbGVfY2xpZW50XzEiOiJ1c2VyIiwicm9sZV9jbGllbnRfMiI6InVzZXIiLCJzY29wZSI6WyJjb250ZW50IiwidGFibGVzIiwibXlvIiwib2ZmbGluZV9hY2Nlc3Mi4XSwiYW1yIjpbIiJdfQ.jGsZo2s16pQ-dVMq1krVZjUITIMoDdOMEHAb7cgy4XLzsc5lMYuJEYjAZlAUjQbnqChgT5QYBThcv-Mt8HRCFW3lxPZWgXxgVskZQDpRS8o75yISeq8kHpbDk1IugugmwLJLwvCh5NGMGT4hKLNtQA79NY-iJZwLXktACvt0Q7TbsvWPwK_C7dGcjAyXxgI_e1OhNu3e-iIjkb-Bfc_bX6OzTZfzGFDVBZwkPPyUr87i3k9m6ibhflKbdSYUlulOxM6-TMXvGs46oTJ5NraLo-gPsaZOEKeiYz_xuCERhpN9_tWyn-Hra-inSzo61g84G53einr7xOnbR1rszsOobg",
  "expires_in": 3600,
  "token_type": "Bearer",
  "refresh_token": "a0d139e1acb497f8640640f9d3c119b6d8cb3d2638912a6975193ba4e457f77ed89"
}
```