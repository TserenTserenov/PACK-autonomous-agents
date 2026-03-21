---
id: AS.M.001
name: "Trust Stack Design"
type: method
status: active
source: "WEF 'AI Agents in Action' (февраль 2026), Singapore IMDA (2026), Scout 21 мар 2026"
related: [AS.D.002, AS.D.007, DP.D.033]
summary: "Методология проектирования governance роли автономного агента по 5 компонентам Trust Stack (WEF)"
---

# AS.M.001: Trust Stack Design

## 1. Назначение

Методология проектирования governance **роли** автономного агента в конкретном контексте. Применяется при создании новой роли с `autonomy_level ≥ execute`.

> **Различение (AS.D.007):** Trust Stack проектируется для **роли агента в контексте**, не для агента как системы. Агента проектирует вендор. Мы проектируем роль, границы и governance.

## 2. Контекст применения

| Когда применять | Когда НЕ применять |
|-----------------|-------------------|
| Новая автономная роль (headless, ночной цикл) | Интерактивная сессия с пользователем |
| `autonomy_level: execute` или `publish` | `autonomy_level: draft` (человек решает) |
| Роль работает без присутствия пользователя | Роль работает только под наблюдением |

## 3. Метод: 5 компонентов Trust Stack

При проектировании роли агента в контексте — пройти по каждому компоненту:

### 3.1. Legible Reasoning

> Роль объясняет, **как** пришла к решению.

- Каждое действие роли сопровождается reasoning (на подходящем уровне детализации)
- Формат: секция `### Reasoning` в выходном артефакте

**Реализация в IWE:** Scout выводит reasoning для каждой находки. Верификатор — для каждого пункта чеклиста.

### 3.2. Bounded Agency

> Чёткие границы того, что роль может делать. Никакой скрытой эскалации полномочий.

- `--allowedTools` — явный список разрешённых инструментов
- `--max-budget-usd` — бюджет на вызов
- Lock-механизм — один экземпляр роли в один момент
- Явный запрет на действия вне scope (не «всё кроме X», а «только Y и Z»)

**Реализация в IWE:** `--allowedTools` в overnight-dispatcher.sh, `--max-budget-usd 1.0` для Scout.

### 3.3. Goal Transparency

> Цели роли явные, не скрытые.

- `goal` в agent-card.yaml — одно предложение
- Цели измеримы (accuracy, coverage, relevance score)
- Если роль оптимизирует несколько целей — приоритет явный

**Реализация в IWE:** `goal: "Найти 3-5 релевантных идей из SOTA"` в agent-card Scout.

### 3.4. Contestability & Override

> Человек может оспорить, исправить или отключить.

- Результат роли = черновик, не финальное решение (для `autonomy_level: draft/execute`)
- Человек ревьюит утром (Scout → morning-ideas.md → ревью)
- Kill switch: остановка через lock-файл или launchd unload

**Реализация в IWE:** Результаты в `DS-agent-workspace/`, человек ревьюит, feedback записывается.

### 3.5. Governance by Design

> Логирование, аудит, oversight встроены с нуля, не добавлены потом.

- Логи каждого вызова (`logs/`)
- Trajectory cache для обучения (`trajectory-cache/`)
- Метаданные запуска (`meta.yaml`)
- Audit trail: кто запустил, когда, с каким бюджетом, какой результат

**Реализация в IWE:** `meta.yaml` + `logs/` + `trajectory-cache/` в DS-autonomous-agents.

## 4. Чеклист (для agent-card.yaml)

При создании новой роли — проверить:

- [ ] Legible Reasoning: формат reasoning определён?
- [ ] Bounded Agency: `--allowedTools` + `--max-budget-usd` заданы?
- [ ] Goal Transparency: `goal` в agent-card.yaml — одно предложение?
- [ ] Contestability: результат = черновик? Человек ревьюит?
- [ ] Governance by Design: логи + meta + trajectory cache?

## 5. Связанные документы

- [AS.D.007](../03-distinctions/AS.D.007-design-agent-vs-design-role-in-context.md) — Проектировать агента ≠ Проектировать роль в контексте
- [AS.D.002](../03-distinctions/AS.D.002-agent-is-executor-plus-role.md) — Агент = Исполнитель + Роль
- Источники: WEF «AI Agents in Action» (2026), Singapore IMDA «Model AI Governance Framework for Agentic AI» (2026)
