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
```http
username - имя пользователя (логин),
password - пароль
```
Ответ:

```http
HTTP/1.1 200 OK
```

```http
sectoken - секретный токен
```
Назначение - аутентификация пользователя (получение секретного токена)

### GET /user/info 

Параметры:
```http
sectoken - секретный токен
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

Назначение - получения информации о пользователе

### PUT /user

Параметры:
```http
sectoken - секретный токен
```

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
sectoken - секретный токен
```

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
