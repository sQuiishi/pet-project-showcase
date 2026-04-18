# API-ONBOARDING-COMPLETE-001

## 1. Общая информация об API

| Name                   | Description                                             |
| ---------------------- | ------------------------------------------------------- |
| ID                     | API-ONBOARDING-COMPLETE-001                             |
| Назначение API         | API предназначен для завершения onboarding пользователя |
| Связь с функцией       | FUNC-ONBOARDING-COMPLETE-001                            |
| Используемый Data Spec | DTO-ONBOARDING-COMPLETE-001                             |

## 2. API Operation 

| Параметр              | Значение                    |
| --------------------- | --------------------------- |
| Method                | POST                        |
| Path                  | /api/v1/onboarding/complete |
| Требуется авторизация | да                          |
| Тип авторизации       | Bearer Token                |

## 3. Request Data — Входные данные API

### 3.1 Query Parameters
| parameter             | обязательный | описание                     | правила / ограничения                                                          |
| --------------------- | ------------ | ---------------------------- | ------------------------------------------------------------------------------ |
| telegram              | да           | контакт пользователя         | string; допускается `nickname` или `@nickname`                                 |
| birth_date            | да           | дата рождения пользователя   | date                                                                           |
| primary_role          | да           | основная роль пользователя   | enum (`IGL`, `AWPer`, `Riffler`, `Support`, `Entry fragger`, `Lurker`, `Flex`) |
| search_goal           | да           | цель поиска                  | enum (`looking_for_players`, `looking_for_team`, `not_searching`)              |
| prime_time            | нет          | игровое время                | time                                                                           |

#### 3.2 Request Body Example
```json
{  
"telegram": "@bro",  
"birth_date": "2004-06-15",  
"primary_role": "AWPer",  
"search_goal": "looking_for_team",  
"prime_time": "17:30-18:30" 
}
```

## 4. Коды ответов

| HTTP Status               | Outcome type | Error / Result code  | Что означает                                                                         |
| ------------------------- | ------------ | -------------------- | ------------------------------------------------------------------------------------ |
| 200 OK                    | Success      | onboarding_completed | onboarding успешно завершён                                                          |
| 400 Bad Request           | Error        | validation_error     | обязательные поля отсутствуют, или переданы некорректно |
| 500 Internal Server Error | Error        | internal_error       | внутренняя ошибка выполнения                                                         |


## 5.1 Success Response Body

200 OK — user_processed
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

- API MUST принимать запрос на завершение onboarding.
- API MUST принимать данные формы onboarding.
- API MUST проверять наличие обязательных полей:
    - `telegram`
    - `birth_date`
    - `primary_role`
    - `search_goal`
    - `personal_data_consent`
- API MUST проверять, что `personal_data_consent = Y`.
- API MUST проверять корректность значений переданных полей.
- API MUST принимать `telegram` в формате `nickname` или `@nickname`.
- API MUST нормализовать `telegram` в формат `t.me/...`.
- API MUST сохранять `telegram`, `birth_date`, `primary_role`, `search_goal` в профиле пользователя.
- Если передано `prime_time`, API MUST сохранять `prime_time` в профиле пользователя.
- Если `prime_time` не передано, API MUST устанавливать значение `prime_time` "не указано".
- API MUST устанавливать `is_onboarding_completed = Y`.
- API MUST устанавливать `status = Active`.
- API MUST устанавливать `is_market_visible`:
    - `Y`, если `search_goal = looking_for_team`
    - `N`, если `search_goal = looking_for_players`
    - `N`, если `search_goal = not_searching`
- API MUST возвращать `next_route = market` при успешном выполнении.
