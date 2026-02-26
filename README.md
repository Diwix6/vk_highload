## Проектирования высоконагруженной системы: Онлайн-платформа для совместной работы распределенных команд. Miro
<img width="250" height="108" alt="изображение" src="https://github.com/user-attachments/assets/c881db57-2387-4e17-8d2d-6d9f4b8248d8" />

MVP Miro фокусируется на главных-функциях: бесконечное полотно для досок, обновление в реальном времени (реал-тайм коллаборация), базовые инструменты рисования. Анализ по шаблону highload-архитектуры (как в VK-примере) учитывает нагрузку 1M+ сессий с WebSocket, шардинг досок и кэш для масштаба. [1](https://www.similarweb.com/website/miro.com/)

## Функциональные требования
- Создание/редактирование досок с drag-and-drop (shapes, notes, lines).
- Реал-тайм синхронизация до 50 пользователей/доска, чат, курсоры.
- Интеграции: экспорт PNG/PDF, импорт Figma/Jira (базово).
- Пользователи: регистрация, приглашения, роли (viewer/editor). [2](https://updf.com/knowledge/miro-business-breakdown/)

## Ненфункциональные требования
- Latency < 100ms для обновлений, 99.9% uptime.
- Масштаб: 10k активных досок/мин, 1GB/доска (JSON-структура).
- Безопасность: JWT, доски private/public, rate-limit 100 ops/sec/user.


## Расчёт нагрузки для Miro (по VK highload шаблону)


## Профиль нагрузки
- **Пользователи:** DAU 2M, concurrent 100k (5% активны).
- **Операции/сессия:** 3000 (create object, move, delete, sync).
- **День/мес:** 4.3M сессий/день, 130M/мес. [3](https://www.calculatorultra.com/en/tool/concurrent-users-calculator.html)

## Метрики производительности
**Avg день:** RPS API 5k, WS msg/sec 10k (broadcast /50 users).
**Peak час:** RPS 15k, concurrent WS 50k, QPS DB 1k writes.
**P99 latency:** <200ms API, <100ms WS; throughput 10k RPS/node.
**Точка деградации:** 20k RPS (OOM Redis), timeout 504 >1%.

**Аудитория Miro превышает 90–100 млн пользователей в 250k+ организациях по 180+ странам.** Ежемесячно фиксируется 1 млрд+ коллаборативных действий. Нагрузка оценивается по трафику 30M визитов/мес, с пиковыми онлайном до 100k+ на досках. [2](https://updf.com/knowledge/miro-business-breakdown/)

## Размер аудитории
Общее число пользователей: 90–100 млн (2025–2026), рост с 50 млн в 2023. [4](https://diginomica.com/canvas-25-miro-notches-100-million-users-it-launches-ai-collaboration-tools)
250k+ организаций, включая PayPal, NFL, GitHub; 35 млн пользователей в 130k платящих клиентов. [5](https://sacra.com/c/miro/)
1 млрд коллаборативных действий/мес; MAU ~10–20 млн (оценка по stickiness). [2](https://updf.com/knowledge/miro-business-breakdown/)

## Демография и вовлечённость
Возраст: 25–34 года (основная группа), 52% женщины. [2](https://www.similarweb.com/website/miro.com/)
Профессии: product managers, designers, devs. [5](https://www.northbeam.io/blog/what-is-mau-tracking-monthly-active-users-to-gauge-growth)

## География аудитории

| Страна          | Доля трафика (%) |
|-----------------|------------------|
| США            | 15.1            |
| Россия         | 9.9             |
| Бразилия       | 6.1             |
| Германия       | 6.0             |
| Великобритания | 5.5             | [3](https://canvasbusinessmodel.com/blogs/target-market/miro-target-market)

## Расчёт нагрузки (оценка для MVP)
**Базовые метрики:** MAU 15 млн, DAU 1.5–3 млн (10–20% ratio), сессия 30 мин. [6](https://www.northbeam.io/blog/what-is-mau-tracking-monthly-active-users-to-gauge-growth)
**RPS:** DAU / день * ops/сессию = ~5–10k RPS API + 1–2k WS msg/sec (broadcast). [7](https://www.calculatorultra.com/en/tool/concurrent-users-calculator.html)
**Concurrent users:** RPS * (think time 10s + response 0.5s) = 50–100k пиково; storage 1TB+ JSON states. [8](https://community.miro.com/ask-the-community-45/concurrent-user-limit-to-work-on-a-board-13978)
**Масштаб MVP:** 10k RPS, Redis 100GB, shards x16; пики x3 baseline (meetings). [3](https://canvasbusinessmodel.com/blogs/target-market/miro-target-market)
