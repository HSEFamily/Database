# Проект для курса "Databases"
  Основная спецификация лежит по [ссылке] (https://docs.google.com/document/d/1p1ihGia8fvkueMhqMkVNX4MV4BssVhzVDqP_4lNqBxI/edit)

### Краткое описание проекта
Мы хотим создать приложение, в котором пользователь мог бы сохранять фильмы, которые он хочет посмотреть или уже посмотрел. Для каждого фильма будет создана страница, на которой будет определенная информация (год выхода, жанр, режиссер, список актеров и описание фильме). Впоследствии, когда список фильмов будет пополняться, мы сможем предложить пользователю похожие фильмы по жанру. На основе зрительских предпочтений приложение посоветует фильмы, которые снимает их любимый режиссер или в которых снимется определенный актерский состав. 
Пользователь после просмотра фильма сможет поставить свою оценку и оставить комментарий о нем. Так же предусмотрена возможность организовать клуб по интересам(чат).

### Что сервис позволяет делать пользователям:
  - искать фильмы, режиссеров, актеров и прочее прочее прочее;
  - ставить рейтинги;
  - писать комментарии;
  - организовывать клубы по интересам.
  
### Что мы должны сделать сейчас:
  - написать требования к проекту;
  - разработать предметную область и модель базы данных;
  - определиться с технологиями;
  - распределить роли;
  - распределить задачи.

### Модель базы данных:
![Database scheme] (komorebi_erd.png)

Пользователи (users):

| Колонка | Тип | Назначение |
| ------- | --- | ---------- |
| id      | primary key | уникальный идентификатор |
| first_name | string | имя пользователя |
| last_name | string | фамилия пользователя |
| email | string | электронная почта |
| user_name | string | логин |
| password | string | пароль |

```sql
CREATE TABLE `users` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `first_name` varchar(50) NOT NULL,
  `last_name` varchar(50) NOT NULL,
  `email` varchar(50) NOT NULL,
  `user_name` varchar(50) NOT NULL,
  `password` varchar(50) NOT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

Фильмы (movies):

| Колонка | Тип | Назначение |
| ------- | --- | ---------- |
| id      | primary key | уникальный идентификатор |
| name | string | название фильма |
| description | string | описание |
| genre | enum string | жанр |
| year | string | год выпуска |

```sql
CREATE TABLE `movies` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `name` varchar(50) NOT NULL,
  `description` varchar(255) NOT NULL,
  `genre` varchar(50) NOT NULL,
  `year` date NOT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

Киноклубы (cinema_clubs):

| Колонка | Тип | Назначение |
| ------- | --- | ---------- |
| id      | primary key | уникальный идентификатор |
| name | string | название клуба |
| description | string | описание |
| club_type | enum string | тип сообщества (приватное, публичное, профессиональное) 

```sql
CREATE TABLE `cinema_clubs` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `name` varchar(50) DEFAULT NULL,
  `description` varchar(255) DEFAULT NULL,
  `club_type` varchar(255) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

Член съемочной группы (film_crew):

| Колонка | Тип | Назначение |
| ------- | --- | ---------- |
| id      | primary key | уникальный идентификатор |
| first_name | string | имя члена съемочной площадки |
| last_name | string | фамилия члена съемочной площадки |
| job_role | string | профессия |

```sql
CREATE TABLE `film_crew` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `first_name` varchar(50) NOT NULL,
  `last_name` varchar(50) NOT NULL,
  `job_role` varchar(50) NOT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

Актерский состав (actors):

| Колонка | Тип | Назначение |
| ------- | --- | ---------- |
| id      | primary key | уникальный идентификатор |
| first_name | string | имя актера |
| last_name | string | фамилия актера |

```sql
CREATE TABLE `actors` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `first_name` varchar(50) NOT NULL,
  `last_name` varchar(50) NOT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```
### Спецификация REST API

Чтобы посмотреть REST API, нужно перейти по [ссылке] (REST_API.md)

### Технологии, которые будут использованы:
  1. серверная часть:
    - postgresql
    - unittest;
    - digitalocean
    - ssh
    - python 3
    - flask
    - psycopg 2
    - git
    - pip 3
  2. клиентская часть:
    - c#;
    - wpf;
    - restsharp;
    - nuget.

### Алгоритмы, используемые в разработке
  1. [Анализ предпочтений пользователей] (https://habrahabr.ru/company/yandex/blog/241455/)
  2. [Метод главных компонент] (https://ru.wikipedia.org/wiki/%D0%9C%D0%B5%D1%82%D0%BE%D0%B4_%D0%B3%D0%BB%D0%B0%D0%B2%D0%BD%D1%8B%D1%85_%D0%BA%D0%BE%D0%BC%D0%BF%D0%BE%D0%BD%D0%B5%D0%BD%D1%82#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80.D1.8B_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F)
