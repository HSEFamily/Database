# Спецификация REST API

### Краткое описание запросов
  
  1. POST /user/new
  2. POST /user/auth
  3. GET /user/{id}
  4. PUT /user/{id}
  5. DELETE /user/{id}
  6. POST /user/{id}/club
  7. PUT /club/{id}
  8. DELETE /club/{id}
  9. GET /user/{id}/clubs
  10. GET /club/{id}/members
  11. PUT /club/{clubId}/member/{memberId}
  12. DELETE /club/{clubId}/member/{memberId}
  13. GET /clubs
  14. GET /movies
  15. POST /user/{id}/movie
  16. GET /user/{id}/movies
  17. DELETE /user/{userId}/movie/{movieId}
  18. PUT /user/{userId}/movie/{movieId}
  
### POST /user/new

Тело:

```json
{
  "first_name" : "Лакрима",
  "last_name" : "Умбрасон",
  "username": "lacrima_umbra",
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
  "username": "lacrima_umbra",
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
  "username": "lacrima_umbra",
  "password" : "17seconds"
}
```
Ответ:

```json
{
  "user": {
    "gender": "female",
    "password": "17seconds",
    "id": 25687,
    "last_name": "Умбрасон",
    "birthday": "Sat, 01 May 1982 00:00:00 GMT",
    "email": "lacrima_umbra@batcave.com",
    "username": "lacrima_batcave",
    "phone_number": "8-888-888-88-88",
    "first_name": "Лакрима"
  },
  "sectoken": "21fed01e3084ea42dd1a984e03589c7079a152df419fd7b15672b57118825d50"
}
```
Назначение - аутентификация пользователя (получение секретного токена)

### GET /user/{id}?sectoken={sectoken} 

Параметры:

```http
sectoken - секретный ключ (128-битный GUID)
```

Ответ:

```json
{
  "id" : 1919,
  "first_name" : "Лакрима",
  "last_name" : "Умбрасон",
  "username": "lacrima_umbra",
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
  "first_name" : "Лакрима",
  "last_name" : "Умбрасон",
  "username": "lacrima_umbra",
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
 "username": "lacrima_umbra",
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

### POST /user/{ownerId}/club?sectoken={sectoken} 

Тело:

```json
{
  "name" : "Batcave",
  "description" : "Movies inspired by gothic subculture, per se"
}
```

Ответ:

```json
{
  "id" : 1979,
  "name" : "Batcave",
  "description" : "Movies inspired by gothic subculture, per se"
}
```

Назначение - создание клуба (пользователь, по чей инициативе был создан клуб, становится его владельцем и админом)

### PUT /club/{id}?sectoken={sectoken} 

Тело:

```json
{
  "name" : "Batcave",
  "description" : "Movies inspired by gothic subculture, per se"
}
```

Назначение - обновление данных о клубе

### DELETE /club/{id}?sectoken={sectoken} 

Параметры:

```http
id - идентификатор клуба
```

Назначение - удаление клуба

### GET /user/{id}/clubs?sectoken={sectoken} 

Параметры:

```http
id - идентификатор пользователя
```

Тело:

```json
[
  {
    "id" : 1979,
    "name" : "Batcave",
    "description" : "Movies inspired by gothic subculture, per se"
  }
]
```

Назначение - поиск клубов, в которых пользователь состоит

### GET /club/{id}/members?sectoken={sectoken} 

Параметры:

```http
id - идентификатор клуба
```

Ответ:

```json
[
  {
    "id" : 1919,
    "first_name" : "Лакрима",
    "last_name" : "Умбрасон",
    "username": "lacrima_umbra",
    "password" : "17seconds",
    "email" : "lacrima_umbra@batcave.com",
    "phone_number" : "8-888-888-88-88",
    "gender" : "female",
    "birthday" : "1982-05-01"
  }
]
```

Назначние - поиск членов клуба

### PUT /club/{clubId}/member/{memberId}?sectoken={sectoken}

Параметры:

```http
clubId - идентификатор клуба,
memberId - идентификатор члена клуба
```

Назначение - добавление пользователя в клуб

### DELETE /club/{clubId}/member/{memberId}?sectoken={sectoken}

Параметры:

```http
clubId - идентификатор клуба,
memberId - идентификатор члена клуба
```
Назначение - удаление члена клуба

### GET /clubs?sq={sq}&sectoken={sectoken}

Параметры:

```http
sq - название клуба или клубов
```

Назначение - поиск клуба или клубов по названию

### GET /movies?sq={sq}&sectoken={sectoken} 

Параметры:

```http
sq - название фильма или фильмов
```

Ответ:

```json
[
  {
    "id" : 2389,
    "name" : "Битлджус",
    "year" : "1988",
    "description" : "Битлджус Битлджус Битлджус",
    "tagline" : "Проделки Факира из загробной жизни",
    "duration" : "92 мин. / 01:32",
    "genre" : ["готика", "черная комедия"],
    "country" : ["США"],
    "picture" : "https://st.kp.yandex.net/images/film_iphone/iphone360_2389.jpg",
    "director" : "Тим Бертон",
    "composer" : "Дэнни Элфман",
    "screenwriters" : [
      "Майкл Макдауэлл", 
      "Уоррен Скаарен", 
      "Ларри Уилсон"
    ],
    "operator" : "Томас Э. Экермен",
    "editor" : "Джейн Карсон",
    "actors" : [
      "Алек Болдуин",
      "Джина Дэвис",
      "Майкл Китон",
      "Вайнона Райдер",
      "Джеффри Джонс",
      "Кэтрин О’Хара"
    ]
  }
]
```

Назначение - поиск фильма или фильмов по названию

### POST /user/{userId}/movie/{movieId}?sectoken={sectoken} 

Параметры:

```http
userId - идентификатор пользователя,
movieId - идентификатор фильма
```

Ответ:

```json
{
    "id" : 2389,
    "name" : "Битлджус",
    "year" : "1988",
    "description" : "Битлджус Битлджус Битлджус",
    "tagline" : "Проделки Факира из загробной жизни",
    "duration" : "92 мин. / 01:32",
    "genre" : ["готика", "черная комедия"],
    "country" : ["США"],
    "picture" : "https://st.kp.yandex.net/images/film_iphone/iphone360_2389.jpg",
    "director" : "Тим Бертон",
    "composer" : "Дэнни Элфман",
    "screenwriters" : [
      "Майкл Макдауэлл", 
      "Уоррен Скаарен", 
      "Ларри Уилсон"
    ],
    "operator" : "Томас Э. Экермен",
    "editor" : "Джейн Карсон",
    "actors" : [
      "Алек Болдуин",
      "Джина Дэвис",
      "Майкл Китон",
      "Вайнона Райдер",
      "Джеффри Джонс",
      "Кэтрин О’Хара"
    ]
}
```

Назначение - сохранение фильма в личной коллекции пользователя

### GET /user/{id}/movies?sectoken={sectoken} 

Параметры:

```http
id - идентификатор пользователя
```

Отве:
```json
[
  {
    "id" : 2389,
    "name" : "Битлджус",
    "year" : "1988",
    "description" : "Битлджус Битлджус Битлджус",
    "tagline" : "Проделки Факира из загробной жизни",
    "duration" : "92 мин. / 01:32",
    "genre" : ["готика", "черная комедия"],
    "country" : ["США"],
    "picture" : "https://st.kp.yandex.net/images/film_iphone/iphone360_2389.jpg",
    "director" : "Тим Бертон",
    "composer" : "Дэнни Элфман",
    "screenwriters" : [
      "Майкл Макдауэлл", 
      "Уоррен Скаарен", 
      "Ларри Уилсон"
    ],
    "operator" : "Томас Э. Экермен",
    "editor" : "Джейн Карсон",
    "actors" : [
      "Алек Болдуин",
      "Джина Дэвис",
      "Майкл Китон",
      "Вайнона Райдер",
      "Джеффри Джонс",
      "Кэтрин О’Хара"
    ]
  }
]
```

Назначение - поиск фильмов в личной коллекции пользователя

### DELETE /user/{userId}/movie/{movieId}?sectoken={sectoken} 

Параметры:

```http
userId - идентификатор пользователя
movieId - идентификатор фильма
```

Назначение - удаление фильма из личной коллекции

### PUT /user/{userId}/movie/{movieId}?sectoken={sectoken} 

Параметры:

```http
userId - идентификатор пользователя,
movieId - идентификатор фильма
```

Тело:
```json
{
  "status" : "watched",
  "rating" : 10,
  "comment" : "Классный! Нет слов!"
}
```
