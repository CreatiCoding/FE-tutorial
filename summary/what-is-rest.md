---
description: '원문: https://www.codecademy.com/articles/what-is-rest'
---

# \[번역중\]What is REST?

코드아카데미의 번역본입니다. \(미완성\)

REST 패러다임을 이용하여 웹 서비스를 디자인하는 방법을 배워봅시다!

### 대표적인 상태 전송\(**RE**presentational **S**tate **T**ransfer\)

REST, 혹은 **RE**presentational **S**tate **T**ransfer 는  웹상에서 컴퓨터 시스템간에 표준을 제공하기 위한 구조적 양식이 시스템이 각각의 다른 것들과 더 쉽게 통신하기 위해 만들어졌습니다.  RESTful 시스템이라고도 하는 REST-준수 시스템은 상태 정보를 저장하지 않는 방식으로 클라이언트와 서버의 문제를 구분합니다. 우리는 이 용어가 의미하는 것과 그들이 왜 웹 상의 서비스에 유익한 특징인지 살펴볼 것 입니다.

### 서버와 클라이언트의 분리

REST 구조에서는 서버와 클라이언트가 서로의 존재를 알지 못한채 독립적으로 구현될 수 있습니다. 즉, 서버의 작동에 영향을 주지 않고 클라이언트 측 코드를 언제든지 변경할 수 있으며 클라이언트 작동에 영향을 주지 않고 서버 측 코드를 변경할 수 있습니다.

As long as each side knows what format of messages to send to the other, they can be kept modular and separate. Separating the user interface concerns from the data storage concerns, we improve the flexibility of the interface across platforms and improve scalability by simplifying the server components. Additionally, the separation allows each component the ability to evolve independently.

By using a REST interface, different clients hit the same REST endpoints, perform the same actions, and receive the same responses.

### 상태 없는 것\(statelessness, 좀 더 매끄러운 표현 없을까?\)

REST 패러다임을 따르는 시스템은 모두 상태가 없으며 이는 서버 혹은 클라이언트가 서로 어떤 상태인지 알 필요가 없다는 것을 의미합니다. In this way, both the server and the client can understand any message received, even without seeing previous messages. This constraint of statelessness is enforced through the use of _resources_, rather than _commands_. Resources are the nouns of the Web - they describe any object, document, or _thing_ that you may need to store or send to other services.

Because REST systems interact through standard operations on resources, they do not rely on the implementation of interfaces.

These constraints help RESTful applications achieve reliability, quick performance, and scalability, as components that can be managed, updated, and reused without affecting the system as a whole, even during operation of the system.

Now, we’ll explore how the communication between the client and server actually happens when we are implementing a RESTful interface.

### 서버와 클라이언트간의 통신

In the REST architecture, clients send requests to retrieve or modify resources, and servers send responses to these requests. Let’s take a look at the standard ways to make requests and send responses.

#### 요청 만들기

REST requires that a client make a request to the server in order to retrieve or modify data on the server. A request generally consists of:

* an HTTP verb, which defines what kind of operation to perform
* a _header_, which allows the client to pass along information about the request
* a path to a resource
* an optional message body containing data

**HTTP 행동**

REST 체계에는 리소스와 상호작용하기 위해서 4가지 HTTP 행동을 취할 수 있습니다.

* GET — \(아이디를 통해\) 특정 리소스나 리소스의 모음을 검색 \(retrieve\)
* POST — 새로운 리소스를 생성
* PUT — \(아이디를 통해\) 특정 리소스를 수정
* DELETE — 아이를 통해 특정 리소스를 삭제

You can learn more about these HTTP verbs in the following Codecademy article:

* [What is CRUD?](https://www.codecademy.com/articles/what-is-crud)

**헤더와 파라미터 ACCEPT**

In the header of the request, the client sends the type of content that it is able to receive from the server. This is called the `Accept` field, and it ensures that the server does not send data that cannot be understood or processed by the client. The options for types of content are MIME Types \(or Multipurpose Internet Mail Extensions, which you can read more about in the [MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_types).

MIME Types, used to specify the content types in the `Accept` field, consist of a `type` and a `subtype`. They are separated by a slash \(/\).

For example, a text file containing HTML would be specified with the type `text/html`. If this text file contained CSS instead, it would be specified as `text/css`. A generic text file would be denoted as `text/plain`. This default value, `text/plain`, is not a catch-all, however. If a client is expecting `text/css` and receives `text/plain`, it will not be able to recognize the content.

Other types and commonly used subtypes:

* `image` — `image/png`, `image/jpeg`, `image/gif`
* `audio` — `audio/wav`, `image/mpeg`
* `video` — `video/mp4`, `video/ogg`
* `application` — `application/json`, `application/pdf`, `application/xml`, `application/octet-stream`

For example, a client accessing a resource with `id` 23 in an `articles`resource on a server might send a GET request like this:

```text
GET /articles/23
Accept: text/html, application/xhtml
```

The `Accept` header field in this case is saying that the client will accept the content in `text/html` or `application/xhtml`.

**경로**

Requests must contain a path to a resource that the operation should be performed on. In RESTful APIs, paths should be designed to help the client know what is going on.

Conventionally, the first part of the path should be the plural form of the resource. This keeps nested paths simple to read and easy to understand.

A path like `fashionboutique.com/customers/223/orders/12` is clear in what it points to, even if you’ve never seen this specific path before, because it is hierarchical and descriptive. We can see that we are accessing the order with `id` 12 for the customer with `id` 223.

Paths should contain the information necessary to locate a resource with the degree of specificity needed. When referring to a list or collection of resources, it is unnecessary to add an `id` to a POST request to a `fashionboutique.com/customers` path would not need an extra identifier, as the server will generate an `id` for the new object.

If we are trying to access a single resource, we would need to append an `id` to the path. For example: `GET fashionboutique.com/customers/:id` — retrieves the item in the `customers` resource with the `id` specified.`DELETE fashionboutique.com/customers/:id` — deletes the item in the `customers` resource with the `id` specified.

#### SENDING RESPONSES

**CONTENT TYPES**

In cases where the server is sending a data payload to the client, the server must include a `content-type` in the header of the response. This `content-type` header field alerts the client to the type of data it is sending in the response body. These content types are MIME Types, just as they are in the `accept` field of the request header. The `content-type` that the server sends back in the response should be one of the options that the client specified in the `accept` field of the request.

For example, when a client is accessing a resource with `id` 23 in an `articles` resource with this GET Request:

```text
GET /articles/23 HTTP/1.1
Accept: text/html, application/xhtml
```

The server might send back the content with the response header:

```text
HTTP/1.1 200 (OK)
Content-Type: text/html
```

This would signify that the content requested is being returning in the response body with a `content-type` of `text/html`, which the client said it would be able to accept.

**RESPONSE CODES**

Responses from the server contain status codes to alert the client to information about the success of the operation. As a developer, you do not need to know every status code \(there are [many](http://www.restapitutorial.com/httpstatuscodes.html) of them\), but you should know the most common ones and how they are used:

| Status code | Meaning |
| :--- | :--- |
| 200 \(OK\) | This is the standard response for successful HTTP requests. |
| 201 \(CREATED\) | This is the standard response for an HTTP request that resulted in an item being successfully created. |
| 204 \(NO CONTENT\) | This is the standard response for successful HTTP requests, where nothing is being returned in the response body. |
| 400 \(BAD REQUEST\) | The request cannot be processed because of bad request syntax, excessive size, or another client error. |
| 403 \(FORBIDDEN\) | The client does not have permission to access this resource. |
| 404 \(NOT FOUND\) | The resource could not be found at this time. It is possible it was deleted, or does not exist yet. |
| 500 \(INTERNAL SERVER ERROR\) | The generic answer for an unexpected failure if there is no more specific information available. |

For each HTTP verb, there are expected status codes a server should return upon success:

* GET — return 200 \(OK\)
* POST — return 201 \(CREATED\)
* PUT — return 200 \(OK\)
* DELETE — return 204 \(NO CONTENT\) If the operation fails, return the most specific status code possible corresponding to the problem that was encountered.

**EXAMPLES OF REQUESTS AND RESPONSES**

Let's say we have an application that allows you to view, create, edit, and delete customers and orders for a small clothing store hosted at `fashionboutique.com`. We could create an HTTP API that allows a client to perform these functions:

If we wanted to view all customers, the request would look like this:

```text
GET http://fashionboutique.com/customers
Accept: application/json
```

A possible response header would look like:

```text
Status Code: 200 (OK)
Content-type: application/json
```

followed by the `customers` data requested in `application/json` format.

Create a new customer by posting the data:

```text
POST http://fashionboutique.com/customers
Body:
{
  “customer”: {
    “name” = “Scylla Buss”
    “email” = “scylla.buss@codecademy.org”
  }
}
```

The server then generates an `id` for that object and returns it back to the client, with a header like:

```text
201 (CREATED)
Content-type: application/json
```

To view a single customer we _GET_ it by specifying that customer’s id:

```text
GET http://fashionboutique.com/customers/123
Accept: application/json
```

A possible response header would look like:

```text
Status Code: 200 (OK)
Content-type: application/json
```

followed by the data for the `customer` resource with `id` 23 in `application/json` format.

We can update that customer by \_PUT\_ting the new data:

```text
PUT http://fashionboutique.com/customers/123
Body:
{
  “customer”: {
    “name” = “Scylla Buss”
    “email” = “scyllabuss1@codecademy.com”
  }
}
```

A possible response header would have `Status Code: 200 (OK)`, to notify the client that the item with `id` 123 has been modified.

We can also _DELETE_ that customer by specifying its `id`:

```text
DELETE http://fashionboutique.com/customers/123
```

The response would have a header containing `Status Code: 204 (NO CONTENT)`, notifying the client that the item with `id` 123 has been deleted, and nothing in the body.

### PRACTICE WITH REST

Let’s imagine we are building a photo-collection site for a different want to make an API to keep track of users, venues, and photos of those venues. This site has an `index.html` and a `style.css`. Each user has a username and a password. Each photo has a venue and an owner \(i.e. the user who took the picture\). Each venue has a name and street address. Can you design a REST system that would accommodate:

* storing users, photos, and venues
* accessing venues and accessing certain photos of a certain venue

Start by writing out:

* what kinds of requests we would want to make
* what responses the server should return
* what the `content-type` of each response should be

### POSSIBLE SOLUTION - MODELS

```text
{
  “user”: {
    "id": <Integer>,
    “username”: <String>,
    “password”:  <String>
  }
}
{
  “photo”: {
    "id": <Integer>,
    “venue_id”: <Integer>,
    “author_id”: <Integer>
  }
}
{
  “venue”: {
    "id": <Integer>,
    “name”: <String>,
    “address”: <String>
  }
}
```

### POSSIBLE SOLUTION - REQUESTS/RESPONSES

**GET REQUESTS**

Request- `GET /index.html` Accept: `text/html` Response- 200 \(OK\) Content-type: `text/html`

Request- `GET /style.css` Accept: `text/css` Response- 200 \(OK\) Content-type: `text/css`

Request- `GET /venues` Accept:`application/json` Response- 200 \(OK\) Content-type: `application/json`

Request- `GET /venues/:id` Accept: `application/json` Response- 200 \(OK\) Content-type: `application/json`

Request- `GET /venues/:id/photos/:id` Accept: `application/json`Response- 200 \(OK\) Content-type: `image/png`

**POST REQUESTS**

Request- `POST /users` Response- 201 \(CREATED\) Content-type: `application/json`

Request- `POST /venues` Response- 201 \(CREATED\) Content-type: `application/json`

Request- `POST /venues/:id/photos` Response- 201 \(CREATED\) Content-type: `application/json`

**PUT REQUESTS**

Request- `PUT /users/:id` Response- 200 \(OK\)

Request- `PUT /venues/:id` Response- 200 \(OK\)

Request- `PUT /venues/:id/photos/:id` Response- 200 \(OK\)

**DELETE REQUESTS**

Request- `DELETE /venues/:id` Response- 204 \(NO CONTENT\)

Request- `DELETE /venues/:id/photos/:id` Response- 204 \(NO CONTENT\)

