# API-AUTH-RESOLVE-USER-ACCESS-001

## 1. Общая информация об API

| Name                   | Description                                                                                  |
| ---------------------- | -------------------------------------------------------------------------------------------- |
| ID                     | API-AUTH-RESOLVE-USER-ACCESS-001                                                             |
| Назначение API         | API предназначен для обработки авторизованного пользователя и определения маршрута редиректа |
| Связь с функцией       | FUNC-AUTH-RESOLVE-USER-ACCESS-001                                                            |
| Используемый Data Spec | DTO-AUTH-RESOLVE-USER-ACCESS-001                                                             |


## 2. API Operation 

| Параметр              | Значение                         |
| --------------------- | -------------------------------- |
| Method                | POST                             |
| Path                  | /api/v1/auth/resolve-user-access |
| Требуется авторизация | да                               |
| Тип авторизации       | Bearer Token                     |

## 3. Request Data — Входные данные API

### 3.1 Query Parameters
| parameter | обязательный | описание                           | правила / ограничения |
| --------- | ------------ | ---------------------------------- | --------------------- |
| faceit_id | да           | внешний идентификатор пользователя | string                |

#### 3.2 Request Body Example
```json
{
  "faceit_id": "abcd-1234"
}
```

## 4. Коды ответов

| HTTP Status               | Outcome type | Error / Result code | Что означает                                      |
| ------------------------- | ------------ | ------------------- | ------------------------------------------------- |
| 200 OK                    | Success      | user_processed      | пользователь успешно обработан, маршрут определён |
| 400 Bad Request           | Error        | validation_error    | `faceit_id` отсутствует или некорректен           |
| 500 Internal Server Error | Error        | internal_error      | внутренняя ошибка выполнения                      |


## 5.1 Success Response Body

200 OK — user_processed
```json
{
  "success": true,
  "next_route": "onboarding"
}
```
```json
{
  "success": true,
  "next_route": "market"
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

- API MUST принимать запрос на обработку пользователя.
- API MUST принимать `faceit_id`.
- API MUST выполнять поиск пользователя в системе по `faceit_id`.
- Если пользователь не найден, API MUST создать нового пользователя.
- Если пользователь не найден, API MUST сохранить `faceit_id` в профиле пользователя.
- Если пользователь не найден, API MUST получить и сохранить базовые данные профиля пользователя.
- Если пользователь не найден, API MUST установить `is_onboarding_completed = N`.
- Если пользователь не найден, API MUST установить `status = Draft`.
- Если пользователь не найден, API MUST вернуть `next_route = onboarding`.
- Если пользователь найден и `is_onboarding_completed = N`, API MUST вернуть `next_route = onboarding`.
- Если пользователь найден и `is_onboarding_completed = Y`, API MUST вернуть `next_route = market`.


## 7. External Dependencies / Data Sources
 
#### API для общей статистики 
GET https://open.faceit.com/data/v4/players/ **faceit_id**

#### API для подробной статистики профиля
GET https://open.faceit.com/data/v4/ **faceit_id** /stats/cs2

#### API для статистики по последним матчам
GET  https://open.faceit.com/data/v4/ **faceit_id** games/cs2/stats?limit=10

!Запросы происходят после выполнения логики функции!