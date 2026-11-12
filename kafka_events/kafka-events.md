### Событие: Создание задачи (Task Created)

**Название топика:** `dev.organizer.fact.tasks.1`
**Описание очереди:** Очередь, в которую отправляется информация о создании новой задачи пользователем. Служит для планирования напоминаний и подбора рекомендаций.

**Параметры сообщений:**

| Название параметра | Тип | Обязательность | Описание |
| :--- | :--- | :--- | :--- |
| `eventId` | UUID | true | Уникальный идентификатор события (для идемпотентности) |
| `eventType` | string | true | Тип события (всегда `task.created`) |
| `occurredAt` | string | true | Дата и время возникновения события (ISO 8601) |
| `payload.taskId` | UUID | true | Идентификатор задачи |
| `payload.userId` | UUID | true | ID пользователя |
| `payload.title` | string | true | Название задачи |
| `payload.dueAt` | string | true | Дата и время выполнения (ISO 8601) |
| `payload.categoryId` | int | true | Идентификатор категории задачи |
| `payload.recurrence` | string | true | Периодичность задачи (NEVER, DAILY, WEEKLY и т.д.) |

**Пример сообщения:**

```json
{
  "eventId": "e8b2c3d4-0000-1111-2222-333344445555",
  "eventType": "task.created",
  "occurredAt": "2026-08-30T14:00:00Z",
  "payload": {
    "taskId": "d171daeb-891c-4c03-a5bf-f88bc2b1ca8a",
    "userId": "aa19f67d-1d46-4e5d-9ff2-ed9b8c8c9548",
    "title": "Купить витамины",
    "dueAt": "2026-08-30T14:05:00+03:00",
    "categoryId": 3,
    "recurrence": "DAILY"
  }
}

### Событие: Обновление задачи (Task Updated)

**Название топика:** `dev.organizer.fact.tasks-updated.1`
**Описание очереди:** Очередь, в которую отправляется информация об изменении полей задачи пользователем.

**Параметры сообщений:**

| Название параметра | Тип | Обязательность | Описание |
| :--- | :--- | :--- | :--- |
| `eventId` | UUID | true | Уникальный идентификатор события |
| `eventType` | string | true | Тип события (всегда `task.updated`) |
| `occurredAt` | string | true | Дата и время возникновения события (ISO 8601) |
| `payload.taskId` | UUID | true | Идентификатор задачи |
| `payload.userId` | UUID | true | ID пользователя |
| `payload.oldTitle` | string | false | Предыдущее название задачи |
| `payload.newTitle` | string | false | Новое название задачи |
| `payload.oldDueAt` | string | false | Предыдущая дата выполнения (ISO 8601) |
| `payload.newDueAt` | string | false | Новая дата выполнения (ISO 8601) |
| `payload.oldStatus` | string | false | Предыдущий статус (NEW, IN_PROGRESS, POSTPONED, CANCELLED) |
| `payload.newStatus` | string | false | Новый статус (NEW, IN_PROGRESS, POSTPONED, CANCELLED) |

**Пример сообщения (Отмена задачи):**

```json
{
  "eventId": "f9c4d5e6-1111-2222-3333-444455556666",
  "eventType": "task.updated",
  "occurredAt": "2026-08-30T15:00:00Z",
  "payload": {
    "taskId": "d171daeb-891c-4c03-a5bf-f88bc2b1ca8a",
    "userId": "aa19f67d-1d46-4e5d-9ff2-ed9b8c8c9548",
    "oldStatus": "NEW",
    "newStatus": "CANCELLED"
  }
}

### Событие: Выполнение задачи (Task Completed)

**Название топика:** `dev.organizer.fact.tasks-completed.1`
**Описание очереди:** Очередь, в которую отправляется факт завершения задачи. Используется для отмены запланированных пуш-уведомлений.

**Параметры сообщений:**

| Название параметра | Тип | Обязательность | Описание |
| :--- | :--- | :--- | :--- |
| `eventId` | UUID | true | Уникальный идентификатор события (для идемпотентности) |
| `eventType` | string | true | Тип события (всегда `task.completed`) |
| `occurredAt` | string | true | Дата и время возникновения события (ISO 8601) |
| `payload.taskId` | UUID | true | Идентификатор задачи |
| `payload.userId` | UUID | true | ID пользователя |
| `payload.completedAt` | string | true | Дата и время фактического выполнения задачи пользователем (ISO 8601) |

**Пример сообщения:**

```json
{
  "eventId": "a1b2c3d4-7777-8888-9999-000011112222",
  "eventType": "task.completed",
  "occurredAt": "2026-08-30T18:00:05Z",
  "payload": {
    "taskId": "d171daeb-891c-4c03-a5bf-f88bc2b1ca8a",
    "userId": "aa19f67d-1d46-4e5d-9ff2-ed9b8c8c9548",
    "completedAt": "2026-08-30T18:00:00Z"
  }
}
