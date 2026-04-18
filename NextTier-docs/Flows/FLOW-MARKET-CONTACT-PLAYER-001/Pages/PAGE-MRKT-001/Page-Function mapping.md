## 1. Общая информация

| Name       | Description                             |
| ---------- | --------------------------------------- |
| ID         | PFM-MRKT-001                            |
| Страница   | PAGE-MRKT-001                           |
| Назначение | Карта вызовов функций страницы feedback |

---

## 2. Function mapping (только функции)

| Page Event                 | Function ID                      | Назначение вызова                                                | Какие данные передаются                                                                                                                                                                          | Outcomes                                                                                                    | Действие страницы                          |
| -------------------------- | -------------------------------- | ---------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------- | ------------------------------------------ |
| Открытие страницы          | FUNC-MARKET-GET-PLAYER-CARDS-001 | Получить карточки игроков для страницы Market                    | page                                                                                                                                                                                             | `market_player_cards_returned`<br>`market_player_cards_empty`  <br>`internal_error`                         | Отобразить список карточек / empty / error |
| Нажатие "Применить"        | FUNC-MARKET-GET-PLAYER-CARDS-001 | Получить карточки игроков с фильтрацией                          | `faceit_level`  <br>`min_elo`  <br>`max_elo`  <br>`primary_role`  <br>`secondary_role`<br>`min_matches`  <br>`max_matches`  <br>`min_age`  <br>`max_age`  <br>`min_kd`  <br>`max_kd`  <br>`page` | `market_player_cards_returned`<br>`market_player_cards_empty`  <br>`validation_error`  <br>`internal_error` | Обновить список карточек / показать ошибку |
| Изменение сортировки       | FUNC-MARKET-GET-PLAYER-CARDS-001 | Получить карточки игроков с сортировкой                          | `sort_parameter` <br>`sort_order`  <br>`page`                                                                                                                                                    | `market_player_cards_returned`<br>`market_player_cards_empty`  <br>`validation_error`  <br>`internal_error` | Обновить список карточек / показать ошибку |
| Нажатие "Сбросить фильтры" | FUNC-MARKET-GET-PLAYER-CARDS-001 | Получить карточки игроков без параметров фильтрации и сортировки | page                                                                                                                                                                                             | `market_player_cards_returned`<br>`market_player_cards_empty`  <br>`internal_error`                         | Обновить список карточек                   |
| Переключение страницы      | FUNC-MARKET-GET-PLAYER-CARDS-001 | Получить карточки игроков для выбранной страницы                 | `page`  <br>текущие параметры фильтрации и/или сортировки                                                                                                                                        | `market_player_cards_returned`<br>`market_player_cards_empty`  <br>`validation_error`  <br>`internal_error` | Обновить список карточек                   |




---

## 3. Page Navigation mapping (роутинг)

| Navigation Event        | UI Element         | Доступ                      | Тип навигации  | Target Page / Anchor     | Результат                          |
| ----------------------- | ------------------ | --------------------------- | -------------- | ------------------------ | ---------------------------------- |
| Нажатие "Профиль"       | Кнопка в карточке  | Авторизованный пользователь | Internal route | PAGE-PLAYER-PROFILE-001  | Переход на страницу профиля игрока |
| Нажатие "TG"            | Кнопка в карточке  | Авторизованный пользователь | External link  | Telegram                 | Переход во внешнюю систему         |
| Нажатие раздела sidebar | Sidebar Navigation | Авторизованный пользователь | Internal route | Соответствующая страница | Переход в выбранный раздел         |


