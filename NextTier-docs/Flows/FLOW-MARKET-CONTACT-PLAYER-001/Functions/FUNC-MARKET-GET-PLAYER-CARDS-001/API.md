# API-MARKET-GET-PLAYERS-CARDS-001

## 1. Общая информация об API

| Name                   | Description                                                        |
| ---------------------- | ------------------------------------------------------------------ |
| ID                     | API-MARKET-GET-PLAYERS-CARDS-001                                   |
| Назначение API         | API предназначен для получения карточек игроков на странице market |
| Связь с функцией       | FUNC-MARKET-GET-PLAYERS-CARDS-001                                  |
| Используемый Data Spec | DTO-MARKET-GET-PLAYERS-CARDS-001                                   |

## 2. API Operation — Update Market Visibility

| Параметр              | Значение               |
| --------------------- | ---------------------- |
| Method                | GET                    |
| Path                  | /api/v1/market/players |
| Требуется авторизация | да                     |
| Тип авторизации       | -                      |

## 3. Request Data — Входные данные API

### 3.1 Query Parameters
| parameter      | обязательный | описание                       | правила / ограничения             |
| -------------- | ------------ | ------------------------------ | --------------------------------- |
| min_elo        | нет          | минимальное значение elo       | integer `>= 0`                    |
| max_elo        | нет          | максимальное значение elo      | integer `>= min_elo`              |
| primary_role   | нет          | фильтр по основной роли        | string                            |
| min_matches    | нет          | минимальное количество матчей  | integer `>= 0`                    |
| max_matches    | нет          | максимальное количество матчей | integer `>= min_matches`          |
| prime_time_from    | нет          | игровое время с | time any          |
| prime_time_to    | нет          | игровое время до | 00:00 > time > prime_time_from         |
| min_age        | нет          | минимальный возраст            | integer `>= 0`                    |
| max_age        | нет          | максимальный возраст           | integer `>= min_age`              |
| min_kd         | нет          | минимальное значение k/d       | decimal `>= 0`                    |
| max_kd         | нет          | максимальное значение k/d      | decimal `>= min_kd`               |
| sort_parameter | нет          | параметр сортировки            | `faceit_elo / matches / age / kd` |
| sort_order     | нет          | направление сортировки         | `asc / desc`                      |
| page           | Да           | номер страницы                 | integer `>= 1`                    |



## 4. Коды ответов

| HTTP Status               | Outcome type | Error / Result code          | Что означает                      |
| ------------------------- | ------------ | ---------------------------- | --------------------------------- |
| 200 OK                    | Success      | market_player_cards_returned | карточки игроков успешно получены |
| 200 OK                    | Success      | market_player_cards_empty    | карточки игроков не найдены       |
| 400 Bad Request           | Error        | validation_error             | некорректные параметры запроса    |
| 500 Internal Server Error | Error        | internal_error               | внутренняя ошибка выполнения      |


## 5.1 Success Response Body

200 OK — market_player_cards_returned
```json
{  
"success": true,    
"data": {  
"market_player_cards": [  
{  
"id": "1234",  
"nickname": "s1mple",  
"avatar": "https://...",  
"faceit_elo": 2450,
"faceit_level": 10,
"primary_role": "awper",    
"age": 20,  
"matches": 1442,
"prime_time": 16.30 - 18.00,
"K/D": 1.15,
"prime_time": "18:00-23:00",  
"telegram_link": "https://t.me/...",
"match_percent": "Подходит на 86%"  
}  
],  
"players_count": 1,
"current_page": 1,
"total_pages": 8
}  
}
```
200 OK — market_player_cards_empty
```
{
  "success": true,
  "data": {
    "market_player_cards": [],
    "players_count": 0,
    "message": "По вашим параметрам игроки не найдены"
  }
}
```
## 5.2 Error Response Body

400 — validation_error
```
{  
"success": false,  
"message": "validation error"  
}
```
500 — internal_error
```
{  
"success": false,  
"message": "internal error"  
}
```

## 6. Processing Rules / Notes

- API MUST принимать запрос на получение карточек игроков страницы market.
- API MUST возвращать только игроков с `is_market_visible=true`.
- API MUST применять фильтрацию, если переданы параметры фильтрации.
- API MUST применять сортировку, если переданы параметры сортировки.
- API MUST сначала применять фильтрацию, затем сортировку, если переданы оба типа параметров.
- API MUST возвращать только те ответы, которые определены в рамках функции.
