# Спецификация REST API

### Краткое описание запросов
  
  1. POST /user/new
  2. POST /user/auth
  3. GET /user/{id}
  4. PUT /user
  5. DELETE /user/{id}
  6. POST /user/{id}/club
  7. PUT /club/{id}
  8. DELETE /club/{id}
  9. GET /user/{id}/clubs
  10. GET /club/{id}/members
  11. GET /movies
  12. POST /user/{id}/movie
  13. GET /user/{id}/movies
  14. DELETE /user/{id}/movie/{id}
  15. PUT /user/{id}/movie/{id}
  
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

```json
{
  "user_name": "lacrima_umbra",
  "password" : "17seconds"
}
```
Ответ:

```json
{
  "sectoken" : "6F9619FF-8B86-D011-B42D-00CF4FC964FF",
  "user_id" : 1919
}
```
Назначение - аутентификация пользователя (получение секретного токена)

### GET /user/{id} 

Тело:
```json
{
  "sectoken" : "6F9619FF-8B86-D011-B42D-00CF4FC964FF"
}
```
Ответ:

```json
{
  "id" : 1919,
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

### PUT /user?sectoken={sectoken}

Параметры:

```http
sectoken - секретный токен
```

Тело:

```json
{
  "id" : 1919,
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

```json
{
  "id" : 1919,
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

### DELETE /user/{id}?sectoken={sectoken}

Параметры:
```http
sectoken - секретный токен
```

Параметры:
```http
id - уникальный идентификатор пользователя
```

Назначение - удаление пользовательского аккаунта

### POST /user/{ownerId}/club

### PUT /club/{id}

### DELETE /club/{id}

### GET /user/{id}/clubs

### GET /club/{id}/members

### GET /movies

### POST /user/{id}/movie/{id}

### GET /user/{id}/movies

### DELETE /user/{id}/movie/{id}

### PUT /user/{id}/movie/{id}
