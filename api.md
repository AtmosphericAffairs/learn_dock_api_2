---
title: Api для библиотеки v1.0.0
language_tabs: []
language_clients: []
toc_footers: []
includes: []
search: true
highlight_theme: darkula
headingLevel: 2

---

<!-- Generator: Widdershins v4.0.1 -->

<h1 id="api-">Api для библиотеки v1.0.0</h1>

> Scroll down for example requests and responses.

<b> Api для работы с базой данных библиотеки.</b> <br>
API позволяет получать: <ul>
<li> Список всех книг с их авторами, </li>
<li> Информацию о конкретной книге, </li>
<li> список авторов,</li>
<li> список книг одного автора. </li> </ul>
Также книги можно добавлять, удалять и редактировать о них сведения.

Base URLs:

* <a href="https://api.library.com/v1">https://api.library.com/v1</a>

* <a href="https://staging-api.library.com/v1">https://staging-api.library.com/v1</a>

# Authentication

* API Key (ApiKeyAuth)
    - Parameter Name: **X-API-KEY**, in: header. 

<h1 id="api--default">Default</h1>

## get__books

> Code samples

`GET /books`

*Получить список книг с авторами.*

Возвращает массив книг. Каждая книга содержит: id, название, данные об авторе.

> Example responses

> 200 Response

```json
[
  {
    "id": 1,
    "name_book": "Война и Мир",
    "author": {
      "id": 1,
      "name_author": "Лёва Толстый"
    }
  }
]
```

<h3 id="get__books-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Успешно. Возвращает список книг.|Inline|

<h3 id="get__books-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[allOf]|false|none|none|

*allOf*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|[BookMin](#schemabookmin)|false|none|none|
|»» id|integer(int64)|true|none|none|
|»» name_book|string|true|none|none|

*and*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|object|false|none|none|
|»» author|[Author](#schemaauthor)|true|none|none|
|»»» id|integer(int64)|true|none|none|
|»»» name_author|string|true|none|none|

<aside class="success">
This operation does not require authentication
</aside>

## post__books

> Code samples

`POST /books`

*Добавить новую книгу.*

Добавляет книгу в базу. Для добавления требуется ключ.

> Body parameter

```json
{
  "name_book": "Шекспир",
  "name_author": "Рома и Джуля",
  "annotation": "Книга о любви..."
}
```

<h3 id="post__books-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[BookCreate](#schemabookcreate)|true|none|

<h3 id="post__books-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Успешно. Книга добавлена в базу.|None|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
ApiKeyAuth
</aside>

## get__books_{id}

> Code samples

`GET /books/{id}`

*Получить информацию о книге по id.*

Возвращает объект с данными о книге по id. Объект содержит: id, название, данные об авторе, аннотацию.

<h3 id="get__books_{id}-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|id|path|integer|true|id книги.|

> Example responses

> 200 Response

```json
{
  "id": 1,
  "name_book": "Война и Мир",
  "author": {
    "id": 1,
    "name_author": "Лёва Толстый"
  },
  "annotation": "События в книге происходят во время наполеоновских войн..."
}
```

<h3 id="get__books_{id}-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Успешно. Возвращает данные о книге.|[BookFull](#schemabookfull)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Книга с указанным id не найдена.|None|

<aside class="success">
This operation does not require authentication
</aside>

## put__books_{id}

> Code samples

`PUT /books/{id}`

*Изменить данные о книге.*

Изменяет данные о книге по id. Для изменения требуется ключ.

> Body parameter

```json
{
  "name_book": "Шекспир",
  "name_author": "Рома и Джуля",
  "annotation": "Книга о любви..."
}
```

<h3 id="put__books_{id}-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|id|path|integer|true|id книги.|
|body|body|[BookCreate](#schemabookcreate)|true|none|

<h3 id="put__books_{id}-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Успешно. Данные о книге изменены.|None|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Неверный или отсутствующий API-ключ.|None|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Книга с указанным id не найдена.|None|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
ApiKeyAuth
</aside>

## delete__books_{id}

> Code samples

`DELETE /books/{id}`

*Удалить книгу по id.*

Удаляет книгу. Для удаления требуется ключ.

<h3 id="delete__books_{id}-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|id|path|integer|true|id книги.|

<h3 id="delete__books_{id}-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Успешно. Книга удалена из базы.|None|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Книги с таким id нет в базе.|None|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
ApiKeyAuth
</aside>

## get__author

> Code samples

`GET /author`

*Получить список авторов.*

Возвращает список авторов. Каждый автор содержит: id, имя.

> Example responses

> 200 Response

```json
[
  {
    "id": 1,
    "name_author": "Лёва Толстый"
  }
]
```

<h3 id="get__author-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Успешно. Возвращает список авторов.|Inline|

<h3 id="get__author-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[[Author](#schemaauthor)]|false|none|none|
|» id|integer(int64)|true|none|none|
|» name_author|string|true|none|none|

<aside class="success">
This operation does not require authentication
</aside>

## get__author_{id}_books

> Code samples

`GET /author/{id}/books`

*Получить список книг автора по его id.*

Возвращает список книг. Книга содержит: id, название.

<h3 id="get__author_{id}_books-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|id|path|integer|true|id автора.|

> Example responses

> 200 Response

```json
[
  {
    "id": 1,
    "name_book": "Война и Мир"
  }
]
```

<h3 id="get__author_{id}_books-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Успешно. Возвращает список книг.|Inline|

<h3 id="get__author_{id}_books-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[[BookMin](#schemabookmin)]|false|none|none|
|» id|integer(int64)|true|none|none|
|» name_book|string|true|none|none|

<aside class="success">
This operation does not require authentication
</aside>

# Schemas

<h2 id="tocS_BookMin">BookMin</h2>
<!-- backwards compatibility -->
<a id="schemabookmin"></a>
<a id="schema_BookMin"></a>
<a id="tocSbookmin"></a>
<a id="tocsbookmin"></a>

```json
{
  "id": 1,
  "name_book": "Война и Мир"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|id|integer(int64)|true|none|none|
|name_book|string|true|none|none|

<h2 id="tocS_BookBase">BookBase</h2>
<!-- backwards compatibility -->
<a id="schemabookbase"></a>
<a id="schema_BookBase"></a>
<a id="tocSbookbase"></a>
<a id="tocsbookbase"></a>

```json
{
  "id": 1,
  "name_book": "Война и Мир",
  "author": {
    "id": 1,
    "name_author": "Лёва Толстый"
  }
}

```

### Properties

allOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[BookMin](#schemabookmin)|false|none|none|

and

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|object|false|none|none|
|» author|[Author](#schemaauthor)|true|none|none|

<h2 id="tocS_BookFull">BookFull</h2>
<!-- backwards compatibility -->
<a id="schemabookfull"></a>
<a id="schema_BookFull"></a>
<a id="tocSbookfull"></a>
<a id="tocsbookfull"></a>

```json
{
  "id": 1,
  "name_book": "Война и Мир",
  "author": {
    "id": 1,
    "name_author": "Лёва Толстый"
  },
  "annotation": "События в книге происходят во время наполеоновских войн..."
}

```

### Properties

allOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[BookBase](#schemabookbase)|false|none|none|

and

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|object|false|none|none|
|» annotation|string|true|none|none|

<h2 id="tocS_Author">Author</h2>
<!-- backwards compatibility -->
<a id="schemaauthor"></a>
<a id="schema_Author"></a>
<a id="tocSauthor"></a>
<a id="tocsauthor"></a>

```json
{
  "id": 1,
  "name_author": "Лёва Толстый"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|id|integer(int64)|true|none|none|
|name_author|string|true|none|none|

<h2 id="tocS_BookCreate">BookCreate</h2>
<!-- backwards compatibility -->
<a id="schemabookcreate"></a>
<a id="schema_BookCreate"></a>
<a id="tocSbookcreate"></a>
<a id="tocsbookcreate"></a>

```json
{
  "name_book": "Шекспир",
  "name_author": "Рома и Джуля",
  "annotation": "Книга о любви..."
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|name_book|string|true|none|none|
|name_author|string|true|none|none|
|annotation|string|true|none|none|

