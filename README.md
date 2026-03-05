## Проектирования высоконагруженной системы: Онлайн-платформа для совместной работы распределенных команд. Miro
<img width="250" height="108" alt="изображение" src="https://github.com/user-attachments/assets/c881db57-2387-4e17-8d2d-6d9f4b8248d8" />

Miro — это онлайн-платформа для визуального сотрудничества, аналогичная реальным сервисам вроде Figma или MURAL, с функционалом MVP, ориентированным на совместную работу в реальном времени: drag-and-drop доски, редактирование объектов, экспорт в PNG/PDF, интеграции с Figma и Jira, режимы viewer/editor.
 [[similarweb.com]](https://www.similarweb.com/website/miro.com/)

## Функциональные требования
- Создание/редактирование досок с drag-and-drop (фигуры, заметки, линии). <br>
- Синхронизация в реальном времени до 50 пользователей на доску, чат, курсоры. <br>
- Интеграции: экспорт в PNG/PDF, импорт из Figma/Jira (базовый уровень). <br>
- Пользователи: регистрация, приглашения, роли (viewer/editor). [[updf]](https://updf.com/knowledge/miro-business-breakdown/) <br>
<br>
Инструменты MVP: рисование от руки, выделение, ластик (удаление объектов и нарисованных линий), перетаскивание, фигуры, стрелки, текстовые блоки, фреймы (рамки), комментарии, совместная работа в реальном времени.

<br>

| Метрика         | Значение |
| --------------- | --------------------------|
| MAU             | 90M |
| DAU             | 9-13.5M |
| DAU/MAU         | 10-15% |
| Демография      | 25-34 года, 52% женщины |
| Платящие клиенты | 130k |

[[fueler.io]](https://fueler.io/blog/miro-usage-revenue-valuation-growth-statistics) 
[[similarweb.com]](https://www.similarweb.com/website/miro.com/)


## Демография и вовлечённость
Возраст: 25–34 года (основная группа), 52% женщины. <br>
Профессии: менеджеры продуктов, дизайнеры, разработчики.. [[similarweb.com]](https://www.similarweb.com/website/miro.com/)<br>

## Распределение по возрасту <br>
<img width="712" height="386" alt="изображение" src="https://github.com/user-attachments/assets/ba71755e-edee-4a37-b77d-54552ece445c" />

<br>

## География аудитории<br>

| Страна          | Доля трафика (%) |
|-----------------|------------------|
| США            | 15.1            |
| Россия         | 9.9             |
| Бразилия       | 6.1             |
| Германия       | 6.0             |
| Великобритания | 5.5             | [[similarweb.com]](https://www.similarweb.com/website/miro.com/)<br>

<br>
<img width="1078" height="505" alt="изображение" src="https://github.com/user-attachments/assets/42c306bc-ee2a-461d-88c5-6104fc4b26a2" />
<br>

## Расчёт нагрузки

### Профиль нагрузки
- **Пользователи:** DAU 10M, одновременно 100k (5% активны). <br>
- **Сессия:** ~45 минут. 
- **Операций за сессию:** 3000 (создание объекта, перемещение, удаление, синхронизация). <br>
- **В день/месяц:** 4.3M сессий/день, 130M/мес. <br>
[[similarweb.com]](https://www.similarweb.com/website/miro.com/)
[[fueler.io]](https://fueler.io/blog/miro-usage-revenue-valuation-growth-statistics)

## Метрики производительности

| Метрика          | Средний                | Пиковый (×2) | Примечание                                 |
| ---------------- | ---------------------- | ------------ | ------------------------------------------ |
| MAU             | 90M | - | - |
| DAU             | 13.5M | - | - |
| DAU/MAU         | 15% | - | - |
| Concurrent users | 90k | 180k   | <300/доска × тысячи досок |
| RPS API          | 10-20k  | 40k          | 5-10 ops/sec/1000 users   |
| WS msg/sec       | 20-50k  | 100k         | -     |
| P99 latency      | 100-200мс | -            |  - |
| Трафик пик       | 10-20 Гбит/сек           | -            | - |


| Метрика | Значение | Источник |
|---|---|---|
| **Monthly Active Users (MAU)** | 90 млн | Официальное заявление Miro на Canvas 25 (2025): "100 million users"  [[diginomica]](https://diginomica.com/canvas-25-miro-notches-100-million-users-it-launches-ai-collaboration-tools) |
| **Daily Active Users (DAU)** | 13.5 млн | **Допущение** ( ≈15% от MAU ) |
| **Среднее количество сессий/досок в день** | ≈1.0/день | **Допущение** на основе типичного использования (1 сессия/день для DAU)  [[fueler]](https://fueler.io/blog/miro-usage-revenue-valuation-growth-statistics) |
| **Среднее количество созданных досок** | 0.1/день | **Оценка** (учитывая по бесплатному плану - 3 доски) [[fueler]](https://fueler.io/blog/miro-usage-revenue-valuation-growth-statistics)) |
| **Среднее количество коллаборативных действий** | ≈5/сессию | **Оценка** ( [[fueler]](https://salessoftwareofficer.com/miro-board-review-2025-key-insights-and-features/)) |
| **Время сессии (средняя длительность)** | 45 минут | Fueler: "session average durations around 45 minutes"  [[fueler]](https://fueler.io/blog/miro-usage-revenue-valuation-growth-statistics) |
| **Количество досок на пользователя** | ≈2-5 активных | **Оценка** (по бесплатному плану 3; макс 5 тыс. objects  [[salessoftwareofficer]](https://salessoftwareofficer.com/miro-board-review-2025-key-insights-and-features/)) |
| **Размер одной доски** | 1-200 МБ | Miro Help: backup up to 200 MB  [[community.miro]](https://community.miro.com/ask-the-community-45/finding-out-miro-board-file-size-4834) |
| **Средний размер доски** | 10-50 МБ | **Оценка** ([[salessoftwareofficer]](https://salessoftwareofficer.com/miro-board-review-2025-key-insights-and-features/)) |
| **Размер ответа доски (load)** | 500 КБ - 5 МБ | **Оценка** |
| **Интервал авто-сейва** | 1-5 сек | **Допущение** |
| **Число обновлений за сессию** | 540 | 45 мин / 5 сек |

## 2.2 Технические метрики

### Расчёт объёма хранения
Расчёт производится для хранения данных, генерируемых за **1 год** использования сервиса.

| Тип данных | Формула расчёта для 1 пользователя | Общий объём данных |
| :--- | :--- | :--- |
| **Доски (boards)** | 0.1 доска × 365 д. × 30 МБ ≈ 1.1 ГБ | **≈110 ПБ** |
| **Коллаборативные действия** | 5 действий × 365 × 1 КБ ≈ 1.8 МБ | **≈180 ТБ** |
| **Сессии/логи** | 1 сессия × 365 × 10 КБ ≈ 3.65 МБ | **≈365 ТБ** |
| **Шаблоны/экспорты** | 0.3 × 365 × 5 КБ ≈ 0.55 МБ | **≈55 ТБ** |
| **Итого** | **≈1.1 ГБ на пользователя** | **≈110 ПБ**  [[miro]](https://miro.com/product-development/product-metrics/)
