# Спецификация REST API

### Краткое описание запросов
  
  1. POST /user/new
  2. POST /user/auth
  3. PUT /user
  4. DELETE /user/{id}
  5. POST /user/{id}/club
  6. PUT /club/{id}
  7. DELETE /club/{id}
  6. GET /user/{id}/clubs
  7. GET /club/{id}/members
  8. POST /user/{id}/movie
  9. GET /user/{id}/movies
  10. DELETE /user/{id}/movie
  11. GET /movie/{id}/info
  
### POST /user/new

Тело:
```json
{
  "first_name" : "Лакрима",
  "last_name" : "Умбрасон",
  "user_name": "lacrima_umbra",
  "password" : "17seconds",
  "email" : "lacrima_umbra@batcave.com",
  "phone_number" : "8-888-888-88-88",
  "gender" : "female",
  "birthday" : "1982-05-01"
}
```
Ответ:

```http
HTTP/1.1 200 OK
```

```json
{
  "id" : "888",
  "first_name" : "Лакрима",
  "last_name" : "Умбрасон",
  "user_name": "lacrima_umbra",
  "password" : "17seconds",
  "email" : "lacrima_umbra@batcave.com",
  "phone_number" : "8-888-888-88-88",
  "gender" : "female",
  "birthday" : "1982-05-01"
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
  "id" : "888",
  "first_name" : "Лакрима",
  "last_name" : "Умбрасон",
  "user_name": "lacrima_umbra",
  "password" : "17seconds",
  "email" : "lacrima_umbra@batcave.com",
  "phone_number" : "8-888-888-88-88",
  "gender" : "female",
  "birthday" : "1982-05-01"
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
  "id" : "888",
  "first_name" : "Лакрима",
  "last_name" : "Умбрасон",
  "user_name": "lacrima_umbra",
  "password" : "17seconds",
  "email" : "lacrima_umbra@batcave.com",
  "phone_number" : "8-888-888-88-88",
  "gender" : "female",
  "birthday" : "1982-05-01"
}
```

Ответ:
```http
HTTP/1.1 200 OK
```

```json
{
  "id" : "888",
  "first_name" : "Лакрима",
  "last_name" : "Умбрасон",
  "user_name": "lacrima_umbra",
  "password" : "17seconds",
  "email" : "lacrima_umbra@batcave.com",
  "phone_number" : "8-888-888-88-88",
  "gender" : "female",
  "birthday" : "1982-05-01"
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
