## Структура базы данных

### Таблицы

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

### Ограничения
```sql
ALTER TABLE cast_movies ADD FOREIGN KEY (actor_id) REFERENCES persons (id);
ALTER TABLE cast_movies ADD FOREIGN KEY (movie_id) REFERENCES movies (id);
ALTER TABLE chat_messages ADD FOREIGN KEY (from_id) REFERENCES users (id);
ALTER TABLE chat_messages ADD FOREIGN KEY (to_id) REFERENCES users (id);
ALTER TABLE crew_movies ADD FOREIGN KEY (crew_id) REFERENCES persons (id);
ALTER TABLE crew_movies ADD FOREIGN KEY (movie_id) REFERENCES movies (id);
ALTER TABLE users_clubs ADD FOREIGN KEY (user_id) REFERENCES users (id);
ALTER TABLE users_clubs ADD FOREIGN KEY (club_id) REFERENCES clubs (id);
ALTER TABLE users_movies ADD FOREIGN KEY (user_id) REFERENCES users (id);
ALTER TABLE users_movies ADD FOREIGN KEY (movie_id) REFERENCES movies (id);
```

### Индексы
```sql
CREATE INDEX person_name_idx ON persons (name);
CREATE UNIQUE INDEX username_unique ON users (username);
CREATE INDEX username_idx ON users (username);
```

### Представления
```sql
CREATE VIEW cast_movies_view AS
  SELECT p.*, c.movie_id FROM persons p INNER JOIN cast_movies c ON p.id = c.actor_id;
--
CREATE VIEW crew_movies_view AS
  SELECT p.name, c.crew_role, c.movie_id FROM persons p INNER JOIN crew_movies c ON p.id = c.crew_id;

CREATE VIEW movies_view AS SELECT m.*,
  ARRAY(
      SELECT name FROM cast_movies_view
      WHERE movie_id = m.id
  ) actors,
  ARRAY(
    SELECT name FROM crew_movies_view
    WHERE movie_id = m.id AND crew_role = 'director'
  ) directors,
  ARRAY(
    SELECT name FROM crew_movies_view
    WHERE movie_id = m.id AND crew_role = 'screenwriter'
  ) screenwriters,
  ARRAY(
    SELECT name FROM crew_movies_view
    WHERE movie_id = m.id AND crew_role = 'operator'
  ) operators,
  ARRAY(
    SELECT name FROM crew_movies_view
    WHERE movie_id = m.id AND crew_role = 'editor'
  ) editors,
  ARRAY(
    SELECT name FROM crew_movies_view
    WHERE movie_id = m.id AND crew_role = 'composer'
  ) composers,
  ARRAY(
    SELECT name FROM crew_movies_view
    WHERE movie_id = m.id AND crew_role = 'producer'
  ) producers
FROM movies m;
CREATE VIEW genre_year_popularity AS
  SELECT unnest(genre) genre, EXTRACT(year FROM m.year) movies_year, COUNT(*) popularity FROM movies m GROUP BY m.year, genre;

CREATE VIEW movies_year_count AS
  SELECT EXTRACT(year from m.year) movies_year, COUNT(*) movies_count FROM movies m GROUP BY movies_year;

CREATE VIEW country_movies_count AS
  SELECT unnest(country) country, COUNT(*) movies_count FROM movies m GROUP BY m.country ORDER BY movies_count ASC;

CREATE VIEW movie_watch_freq AS
  SELECT name, COUNT(*) FROM movies INNER JOIN users_movies ON movies.id = users_movies.movie_id
INNER JOIN users ON users_movies.user_id = users.id
GROUP BY movie_id, name;

CREATE VIEW movie_popularity AS
SELECT name, avg(rating)::DOUBLE PRECISION avg_rating FROM movies INNER JOIN users_movies ON movies.id = users_movies.movie_id
INNER JOIN users ON users_movies.user_id = users.id
GROUP BY movie_id, name ORDER BY avg_rating DESC ;
```
