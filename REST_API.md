# Спецификация REST API

### POST /user

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

### GET /user/{id}/clubs

### POST /club
