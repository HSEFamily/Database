# Спецификация REST API

### POST /user

Тело:
```json
{
  'first_name' : '',
  'last_name' : '',
  'user_name': '',
  'password' : '',
  'email' : '',
  'phone_number' : ''
}
```
Ответ:
```json
{
  'id' : '',
  'first_name' : '',
  'last_name' : '',
  'user_name': '',
  'password' : '',
  'email' : '',
  'phone_number' : ''
}
```
Назначение - регистрация пользователя в системе

### PUT /user

### DELETE /user

### GET /user/{id}/clubs

### POST /club
