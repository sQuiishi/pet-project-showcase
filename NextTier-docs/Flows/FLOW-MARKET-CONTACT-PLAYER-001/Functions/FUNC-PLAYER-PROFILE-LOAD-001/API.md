# API-PLAYER-PROFILE-LOAD-001

## 1. Общая информация об API

| Name                   | Description                                             |
| ---------------------- | ------------------------------------------------------- |
| ID                     | API-PLAYER-PROFILE-LOAD-001                             |
| Назначение API         | API предназначен для загрузки профиля выбранного игрока |
| Связь с функцией       | FUNC-PLAYER-PROFILE-LOAD-001                            |
| Используемый Data Spec | DTO-PLAYER-PROFILE-LOAD-001                             |

## 2. API Operation — Update Market Visibility

| Параметр              | Значение             |
| --------------------- | -------------------- |
| Method                | GET                  |
| Path                  | /api/v1/players/{id} |
| Требуется авторизация | да                   |
| Тип авторизации       | Bearer Token         |
## 3. Request Data — Входные данные API

### 3.1 Path Parameters

| Parameter | Обязательное | Описание             | Тип    | Пример |
| --------- | ------------ | -------------------- | ------ | ------ |
| id        | Да           | Идентификатор игрока | string | `1002` |

## 4. Коды ответов

| HTTP Status               | Outcome type | Error / Result code      | Что означает                    |
| ------------------------- | ------------ | ------------------------ | ------------------------------- |
| 200 OK                    | Success      | player_profile_loaded    | Профиль игрока успешно загружен |
| 404 Not Found             | Success      | player_profile_not_found | Профиль игрока не найден        |
| 400 Bad Request           | Error        | validation_error         | Некорректный `id`               |
| 500 Internal Server Error | Error        | internal_error           | Внутренняя ошибка системы       |

## 5.1 Success Response Body

200 OK — market_visibility_updated
```json
{
  "success": true,
  "player_profile": {
    "id": "1002",
    "nickname": "s1mple",
    "avatar": "https://cdn.example.com/avatar.jpg",
    "telegram_link": "https://t.me/player_contact",
    "faceit_profile_url": "https://www.faceit.com/en/players/s1mple",
    "age": 18,
    "primary_role": "awper",
    "secondary_role": "rifler",
    "looking_for_team": true,
    "prime_time": "18:30-20:30",
    "recent_matches": [
      {
        "match_finished_at": 1774627147000,
        "score": "13 / 5",
        "kills": 14,
        "deaths": 12,
        "assists": 9,
        "adr": 84.8,
        "kd_ratio": 1.17,
        "kr_ratio": 0.78,
        "headshots_percent": 43,
        "mvps": 3,
        "map": "de_mirage",
        "map_avatar": "https://cdn.example.com/maps/de_mirage.png"
      }
      {
        "match_finished_at": 1774627147000,
        "score": "13 / 5",
        "kills": 14,
        "deaths": 12,
        "assists": 9,
        "adr": 84.8,
        "kd_ratio": 1.17,
        "kr_ratio": 0.78,
        "headshots_percent": 43,
        "mvps": 3,
        "map": "de_mirage",
        "map_avatar": "https://cdn.example.com/maps/de_mirage.png"
      }
      {
        "match_finished_at": 1774627147000,
        "score": "13 / 5",
        "kills": 14,
        "deaths": 12,
        "assists": 9,
        "adr": 84.8,
        "kd_ratio": 1.17,
        "kr_ratio": 0.78,
        "headshots_percent": 43,
        "mvps": 3,
        "map": "de_mirage",
        "map_avatar": "https://cdn.example.com/maps/de_mirage.png"
      }
    ]
  }
}
```

Profile Not Found — 404
```
{
  "success": false,
  "error": "player_profile_not_found"
}
```
## 5.2 Error Response Body

Validation Error — 400
```
{
  "success": false,
  "error": "validation_error"
}
```
Internal Error — 500
```
{  
"success": false,  
"error": "internal_error"  
}
```
## 6. Processing Rules / Notes

- API MUST принимать `id` игрока из path параметра
- API MUST валидировать `id` перед выполнением
- API MUST выполнять поиск профиля игрока по `id`
- API MUST формировать объект `player_profile` согласно DTO
- API MUST возвращать только данные одного игрока
- API MUST возвращать `player_profile_loaded`, если профиль найден
- API MUST возвращать `player_profile_not_found`, если профиль не найден
- API MUST возвращать `validation_error`, если `id` некорректен
- API MUST возвращать `internal_error`, если выполнение невозможно