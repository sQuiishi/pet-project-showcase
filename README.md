# NextTier — Product Requirements Documentation

> **Статус:** MVP v1.0.0 — в активной разработке  
> **Моя роль:** System Analyst / UI/UX Designer

## О проекте

**NextTier** — платформа для игроков в CS2, которая упрощает поиск партнёров по команде, 
благодаря маркету игроков, организовывает тренировочные матчи и помогает в формировании киберспортивных команд.

В будущем планируется добавление dota 2, valorant и других игр.

Проект разрабатывается командой из 7 человек: я отвечаю за аналитику требований и 
проектирование продукта, 1 backend разработчик, 1 frontend разработчик, 1 дизайнер, 3 системных аналитика (2 из которых на смежных ролях), 1 api разработчик.

---

## Моя роль в проекте

| Что делал | Артефакты |
|---|---|
| Сбор и формализация требований | User Stories, бизнес-правила (MUST/MAY) |
| Проектирование пользовательских сценариев | User Flows с Happy Path и альтернативными сценариями |
| Составление критериев приёмки | Acceptance Criteria в формате Given / When / Then |
| Описание структур данных API | DTO (Input / System / Output Data) |
| Проектирование страниц и компонентов | Page Specifications, Page-Function Mapping |
| Визуализация логики | Activity-диаграммы |

---

## Артефакты в этом репозитории

### 📋 Scope & Vision
Таблица всех пользовательских флоу продукта с описанием назначения каждого сценария.  
→ [Scope & Vision.md](NextTier-docs/Scope%20%26%20Vision.md)

---

### 🔐 FLOW-AUTH-ACCESS-001 — Авторизация через Faceit
Флоу авторизации через внешний OAuth-провайдер (Faceit) с определением маршрута доступа 
(онбординг или маркет).

**Содержит:**
- Happy Path + 2 альтернативных сценария (существующий пользователь: с/без онбординга)
- Бизнес-правила в MUST/MAY нотации
- Activity-диаграмму

→ [FLOW-AUTH-ACCESS-001](NextTier-docs/Flows/FLOW-AUTH-ACCESS-001/)

---

### 🛒 FLOW-MARKET-CONTACT-PLAYER-001 — Маркет игроков
Ключевой флоу: просмотр маркета, фильтрация/сортировка карточек, переход к профилю игрока 
и контакт через Telegram.

**Содержит:**
- Happy Path + 2 альтернативных сценария
- **DTO-MARKET-GET-PLAYERS-CARDS-001** — спецификация входных, системных и выходных данных API
- **AC-MARKET-GET-PLAYERS-CARDS-001** — 9 acceptance criteria в формате Given/When/Then
- **PAGE-MRKT-001** — спецификация страницы: блоки, поведение, состояния, маппинг на функции
- Activity-диаграмму

→ [FLOW-MARKET-CONTACT-PLAYER-001](NextTier-docs/Flows/FLOW-MARKET-CONTACT-PLAYER-001/)

---

### 👤 FLOW-PLAYER-PROFILE-MANAGE-001 — Управление профилем игрока
Флоу просмотра и редактирования профиля: валидация данных, сохранение изменений.

→ [FLOW-PLAYER-PROFILE-MANAGE-001](NextTier-docs/Flows/FLOW-PLAYER-PROFILE-MANAGE-001/)

---

### 🎮 Practice Matches — Структура данных
Описание классов и сущностей для раздела тренировочных матчей: форматы (Bo1/Bo3/Bo5), 
регионы серверов, карты, хосты, статусы удаления.

→ [Data Structure.md](NextTier-docs/Flows/PRACTICE-MATCHES/Data%20Structure.md)

---

## Figma

Прототипы ключевых экранов платформы: Welcome-page, login-page, profile-page, FAQ-page (Предложения и баги).

→ [Открыть в Figma](https://www.figma.com/design/mLoxZLhWO5jLbjHmUhqhzn/Untitled?node-id=0-1&t=j1cCXd9bZPU61FDW-1)

---

## Стек и инструменты

| Инструмент | Зачем |
|---|---|
| Figma | Прототипирование интерфейсов (макеты, навигация, логика экранов) |
| Markdown / GitHub | Документирование требований |
| Draw.io | Activity-диаграммы |

---
