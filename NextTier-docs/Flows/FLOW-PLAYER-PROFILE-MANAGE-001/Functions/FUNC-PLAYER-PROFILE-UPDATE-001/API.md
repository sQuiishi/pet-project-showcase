# 1. Общая информация

| Параметр              | Значение                             |
| --------------------- | ------------------------------------ |
| Method                | PATCH                                |
| Path                  | /api/v1/profile/                     |
| Требуется авторизация | Да                                   |
| Тип авторизации       | Bearer Token                         |

# 2. Входные данные

## 2.1 Request Body

Content Type: form-data

```
"telegram": "@nickname"
"prime_time": "17:30-18:30"
"primary_role": "AWPer"
"avatar": file
```

## 2.2 Path params

-

## 2.3 Query params

-

# 3. Коды ответов

| HTTP Status     | Outcome type         | Error / Result code  | Что означает                 | Response Body               |
| --------------- | -------------------- | -------------------- | ---------------------------- | --------------------------- |
| 200             | Success              | -                    | Профиль обновлен             | См. Success Response        |
| 400             | Error                | validation_error     | Некорректные параметры       | См. 400 Error Response Body |
| 403             | Forbidden            | forbidden            | Нельзя изменить эту запись   | См. 403 Error Response Body |

# 4.1 Success Response Body

```json
{  
    "success": true,
    "message": "Successfuly updated",
    "item": {
        "id" : 2412,
        "avatar_url": "path/to/avatar",
        "nickname": "faceit nickname",
        "telegram_link": "https://t.me/nickname",
        "birth_date": "2004-06-15",
        "primary_role": "AWPer",
        "search_goal": "looking_for_team",
        "prime_time": "17:30-18:30"
    }
}
```

# 4.2 400 Error Response Body

```json
{  
    "success": false,  
    "message": "Validation error",
    "details": {
        // Здесь конкретные ошибки
    }
}
```

# 4.3 403 Error Response Body

```json
{  
    "success": false,  
    "message": "You are not authorized to do this action",
}
```


# 5. Processing Rules / Notes

- Система должна принимать `telegram` в формате `nickname` или `@nickname` или `t.me/...`.
- Система должна нормализовать `telegram` в формат `t.me/...`.
- Чтобы пользователь удалил `prime_time`, он должен передать в запросе `"prime_time": NULL`.
- В API описаны только те ответы, которые формируются системой в рамках логики функции.
- Клиентские ошибки, автоматические ошибки сервера и внутренние технические сбои в API не описываются.
