---
id: AS.D.006
name: "Execution Loop ≠ Improvement Loop"
status: active
source: "Andrej Karpathy, 'Loopy Era', март 2026 (Scout 21 мар 2026)"
related: [AS.D.002, AS.D.004]
---

# AS.D.006: Execution Loop ≠ Improvement Loop

## Различение

| Аспект | Execution Loop | Improvement Loop |
|--------|---------------|------------------|
| Суть | Агент решает задачу | Агент улучшает способность решать задачи |
| Вход | Задание от пользователя / триггер | Результаты Execution Loop + метрики |
| Артефакт | Рабочий продукт | Обновлённый промпт, процедура, конфигурация |
| Частота | Каждый запрос | По триггеру (после N итераций, по расписанию, при деградации) |
| Аналогия | Матч | Тренировка |

## Почему важно

Без Improvement Loop агент застревает на plateau: повторяет одни и те же ошибки, не адаптируется к изменениям контекста, не интегрирует обратную связь.

## Связь с ОРЗ-фракталом

В контексте IWE:
- **Execution Loop** = стадия «Работа» (сессия) — выполняется РП
- **Improvement Loop** = стадия «Закрытие» (Quick Close / Day Close) — KE, captures, обновление протоколов

Без Close (Improvement Loop) агент работает, но не развивается.

## Триггеры для Improvement Loop

1. Ошибка повторилась >1 раза
2. Плановое ревью (Day Close, Week Close)
3. Метрика деградировала (качество, скорость)
4. Новое знание получено (Scout, чтение, обратная связь)

## Связанные документы

- [AS.D.002](./AS.D.002-agent-is-executor-plus-role.md) — агент = исполнитель + роль
- [AS.D.004](./AS.D.004-core-vs-context.md) — core vs context (Improvement Loop меняет context, не core)
- Источник: Andrej Karpathy, «Loopy Era», март 2026
