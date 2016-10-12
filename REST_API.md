# Спецификация REST API



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
