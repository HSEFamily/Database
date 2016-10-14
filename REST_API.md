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
  14. DELETE /user/{userId}/movie/{movieId}
  15. PUT /user/{userId}/movie/{movieId}
  
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

### PUT /club?sectoken={sectoken} 

Тело:

```json
{
  "id" : 1979,
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
    "user_name": "lacrima_umbra",
    "password" : "17seconds",
    "email" : "lacrima_umbra@batcave.com",
    "phone_number" : "8-888-888-88-88",
    "gender" : "female",
    "birthday" : "1982-05-01"
  }
]
```

Назначние - поиск членов клуба

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
