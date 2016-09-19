# Спецификация REST API

### POST /user/new

Тело:
```json
{
  "first_name" : "",
  "last_name" : "",
  "user_name": "",
  "password" : "",
  "email" : "",
  "phone_number" : ""
}
```
Ответ:

```http
HTTP/1.1 200 OK
```

```json
{
  "id" : "",
  "first_name" : "",
  "last_name" : "",
  "user_name": "",
  "password" : "",
  "email" : "",
  "phone_number" : ""
}
```
Назначение - регистрация пользователя в системе

### POST /user/auth

Тело:
```json
{
  "first_name" : "",
  "last_name" : "",
  "user_name": "",
  "password" : "",
  "email" : "",
  "phone_number" : ""
}
```
Ответ:

```http
HTTP/1.1 200 OK
```

```json
{
  "__token__": "",
  "id" : "",
  "first_name" : "",
  "last_name" : "",
  "user_name": "",
  "password" : "",
  "email" : "",
  "phone_number" : ""
}
```
Назначение - аутентификация пользователя

### PUT /user

Тело:
```json
{
  "id" : "",
  "first_name" : "",
  "last_name" : "",
  "user_name": "",
  "password" : "",
  "email" : "",
  "phone_number" : ""
}
```

Ответ:
```http
HTTP/1.1 200 OK
```

```json
{
  "id" : "",
  "first_name" : "",
  "last_name" : "",
  "user_name": "",
  "password" : "",
  "email" : "",
  "phone_number" : ""
}
```
Назначение - обновление персональных данных пользователя

### DELETE /user/{id}

Параметры:
```http
id - уникальный идентификатор пользователя
```

Ответ: 
```http
HTTP/1.1 200 OK
```
Назначение - удаление пользовательского аккаунта

### GET /user/{id}/clubs



### POST /club
