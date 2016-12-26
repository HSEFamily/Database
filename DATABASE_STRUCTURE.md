### Структура базы данных

## Таблицы

```sql
CREATE TABLE cast_movies
(
    id INTEGER PRIMARY KEY NOT NULL,
    actor_id INTEGER NOT NULL,
    movie_id INTEGER NOT NULL
);
CREATE TABLE chat_messages
(
    id INTEGER PRIMARY KEY NOT NULL,
    from_id INTEGER NOT NULL,
    to_id INTEGER NOT NULL,
    date TIMESTAMP NOT NULL,
    message TEXT NOT NULL
);
CREATE TABLE clubs
(
    id INTEGER PRIMARY KEY NOT NULL,
    name VARCHAR(50),
    description VARCHAR(255)
);
CREATE TABLE crew_movies
(
    id INTEGER PRIMARY KEY NOT NULL,
    crew_id INTEGER NOT NULL,
    movie_id INTEGER NOT NULL,
    crew_role VARCHAR(20) NOT NULL
);
CREATE TABLE movies
(
    id INTEGER PRIMARY KEY NOT NULL,
    name VARCHAR(50) NOT NULL,
    year DATE NOT NULL,
    description VARCHAR(255),
    tagline VARCHAR(255),
    duration VARCHAR(50),
    genre VARCHAR(50) [],
    country VARCHAR(50) [],
    picture VARCHAR(300)
);
CREATE TABLE persons
(
    id INTEGER PRIMARY KEY NOT NULL,
    name VARCHAR(100)
);
CREATE TABLE users
(
    id INTEGER PRIMARY KEY NOT NULL,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    email VARCHAR(50),
    username VARCHAR(50) NOT NULL,
    password VARCHAR(50) NOT NULL,
    gender VARCHAR(10),
    birthday DATE,
    phone_number VARCHAR(30)
);
CREATE TABLE users_clubs
(
    id INTEGER PRIMARY KEY NOT NULL,
    user_id INTEGER NOT NULL,
    club_id INTEGER NOT NULL,
    user_role VARCHAR(10) NOT NULL
);
CREATE TABLE users_movies
(
    id INTEGER PRIMARY KEY NOT NULL,
    user_id INTEGER NOT NULL,
    movie_id INTEGER NOT NULL,
    status VARCHAR(20) NOT NULL,
    rating INTEGER,
    comment TEXT
);
CREATE TABLE cast_movies_view
(
    id INTEGER,
    name VARCHAR(100),
    movie_id INTEGER
);
CREATE TABLE country_movies_count
(
    country VARCHAR,
    movies_count BIGINT
);
CREATE TABLE crew_movies_view
(
    name VARCHAR(100),
    crew_role VARCHAR(20),
    movie_id INTEGER
);
CREATE TABLE genre_year_popularity
(
    genre VARCHAR,
    movies_year DOUBLE PRECISION,
    popularity BIGINT
);
CREATE TABLE movie_popularity
(
    name VARCHAR(50),
    avg_rating DOUBLE PRECISION
);
CREATE TABLE movie_watch_freq
(
    name VARCHAR(50),
    count BIGINT
);
CREATE TABLE movies_view
(
    id INTEGER,
    name VARCHAR(50),
    year DATE,
    description VARCHAR(255),
    tagline VARCHAR(255),
    duration VARCHAR(50),
    genre VARCHAR(50) [],
    country VARCHAR(50) [],
    picture VARCHAR(300),
    actors VARCHAR(100) [],
    directors VARCHAR(100) [],
    screenwriters VARCHAR(100) [],
    operators VARCHAR(100) [],
    editors VARCHAR(100) [],
    composers VARCHAR(100) [],
    producers VARCHAR(100) []
);
CREATE TABLE movies_year_count
(
    movies_year DOUBLE PRECISION,
    movies_count BIGINT
);
```
