## Проектирования высоконагруженной системы: Онлайн-платформа для совместной работы распределенных команд. Miro
<img width="250" height="108" alt="изображение" src="https://github.com/user-attachments/assets/c881db57-2387-4e17-8d2d-6d9f4b8248d8" />

MVP Miro фокусируется на главных-функциях: бесконечное полотно для досок, обновление в реальном времени (реал-тайм коллаборация), базовые инструменты рисования. Анализ по шаблону highload-архитектуры (как в VK-примере) учитывает нагрузку 1M+ сессий с WebSocket, шардинг досок и кэш для масштаба. [1](https://www.similarweb.com/website/miro.com/)

## Функциональные требования
- Создание/редактирование досок с drag-and-drop (фигуры, заметки, линии).
- Синхронизация в реальном времени до 50 пользователей на доску, чат, курсоры.
- Интеграции: экспорт в PNG/PDF, импорт из Figma/Jira (базовый уровень).
- Пользователи: регистрация, приглашения, роли (viewer/editor). [2](https://updf.com/knowledge/miro-business-breakdown/)

## Нефункциональные требования
- Задержка (Latency) < 100 мс для обновлений, доступность 99.9%.
- Масштабирование: 10k активных досок в минуту, 1 ГБ на доску (JSON-структура).

## Расчёт нагрузки для Miro (по шаблону VK highload)

### Профиль нагрузки
- **Пользователи:** DAU 2M, одновременно 100k (5% активны).
- **Операций за сессию:** 3000 (создание объекта, перемещение, удаление, синхронизация).
- **В день/месяц:** 4.3M сессий/день, 130M/мес. [3](https://www.calculatorultra.com/en/tool/concurrent-users-calculator.html)

## Метрики производительности
**Средний день:** RPS API 5k, сообщений WS/сек 10k (broadcast на 50 пользователей).
**Пиковый час:** RPS 15k, одновременных WS 50k, QPS БД 1k записей.
**P99 задержка:** <200 мс API, <100 мс WS; пропускная способность 10k RPS/node.
**Точка деградации:** 20k RPS (OOM Redis), таймаут 504 >1%.

**Аудитория Miro превышает 90–100 млн пользователей в 250k+ организациях из 180+ стран.** Ежемесячно фиксируется 1 млрд+ коллаборативных действий. Нагрузка оценивается по трафику 30M визитов/мес, с пиковым онлайном до 100k+ на досках. [2](https://updf.com/knowledge/miro-business-breakdown/)

## Размер аудитории
Общее число пользователей: 90–100 млн (2025–2026), рост с 50 млн в 2023. [4](https://diginomica.com/canvas-25-miro-notches-100-million-users-it-launches-ai-collaboration-tools)
250k+ организаций, включая PayPal, NFL, GitHub; 35 млн пользователей из 130k платящих клиентов. [5](https://sacra.com/c/miro/)
1 млрд коллаборативных действий/мес; MAU ~10–20 млн (оценка по вовлечённости). [2](https://updf.com/knowledge/miro-business-breakdown/)

## Демография и вовлечённость
Возраст: 25–34 года (основная группа), 52% женщины. [2](https://www.similarweb.com/website/miro.com/)
Профессии: менеджеры продуктов, дизайнеры, разработчики.. [5](https://www.northbeam.io/blog/what-is-mau-tracking-monthly-active-users-to-gauge-growth)

## Распределение по возрасту
<img width="712" height="386" alt="изображение" src="https://github.com/user-attachments/assets/ba71755e-edee-4a37-b77d-54552ece445c" />


## География аудитории

| Страна          | Доля трафика (%) |
|-----------------|------------------|
| США            | 15.1            |
| Россия         | 9.9             |
| Бразилия       | 6.1             |
| Германия       | 6.0             |
| Великобритания | 5.5             | [3](https://canvasbusinessmodel.com/blogs/target-market/miro-target-market)

<img width="1078" height="505" alt="изображение" src="https://github.com/user-attachments/assets/42c306bc-ee2a-461d-88c5-6104fc4b26a2" />


## Расчёт нагрузки (оценка для MVP)
**Базовые метрики:** MAU 15 млн, DAU 1.5–3 млн (10–20% ratio), сессия 30 мин. [6](https://www.northbeam.io/blog/what-is-mau-tracking-monthly-active-users-to-gauge-growth) <br>
**RPS:** DAU / день * ops/сессию = ~5–10k RPS API + 1–2k WS msg/sec. [7](https://www.calculatorultra.com/en/tool/concurrent-users-calculator.html) <br>
**Concurrent users:** RPS * (10s + ответ 0.5s) = 50–100k пиково. [8](https://community.miro.com/ask-the-community-45/concurrent-user-limit-to-work-on-a-board-13978) <br>
