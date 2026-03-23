---
id: AS.SOTA.002
name: "Multi-Agent Orchestration Frameworks (2026)"
type: sota
status: active
created: 2026-03-23
source: "Gurusup Multi-Agent Frameworks 2026, DEV Community Orchestration Guide, Scout 22 мар 2026"
related: [AS.M.001, AS.SOTA.001, AS.D.001]
s2r_families: [F8]
---

# AS.SOTA.002: Фреймворки мультиагентной оркестрации (2026)

## Сравнение фреймворков

| Критерий | LangGraph | CrewAI |
|----------|-----------|--------|
| **Парадигма** | Stateful graphs (nodes=functions, edges=control flow) | Role-based collaboration (crew of agents) |
| **Порог входа** | Высокий (теория графов, state management) | Низкий (20 строк до рабочего прототипа) |
| **Production-ready** | Да (durability, точный state, debugging) | Прототипирование (мигрировать на LangGraph для прода) |
| **State management** | Explicit, traceable | Implicit, agent-internal |
| **Лучше для** | Сложные workflows, conditional routing | Быстрое прототипирование, чёткое разделение ролей |
| **Когда использовать** | После PMF, масштабирование в прод | MVP, валидация, ранняя стадия |

## Координационные паттерны (2026)

### 1. Supervisor (наиболее распространён в enterprise)

```
Supervisor получает задачу
    ↓
Делегирует специализированным агентам
    ↓
Workers выполняют независимо
    ↓
Supervisor валидирует результаты
    ↓
Решает: следующая делегация или завершение
```

### 2. Pipeline

```
Agent A → Agent B → Agent C → Output
```
Последовательная обработка, каждый агент добавляет ценность.

### 3. Hierarchical

```
Executive Agent → Manager Agents → Worker Agents
```
Для масштабных систем с организационной структурой.

## Best Practices (2026)

### Model Tiering

- Fast model (Haiku) для triage, routing
- Capable model (Sonnet) для complex reasoning
- Оптимизация затрат: 3-5x дешевле с tiering

### State Management

- LangGraph: explicit state nodes, conditional routing
- CrewAI: agent memory (working, short-term, long-term)
- **Критично:** audit trail для debugging (35% coordination breakdowns)

### Путь миграции

1. **Фаза 1:** Прототип на CrewAI (скорость до валидации)
2. **Фаза 2:** Миграция core workflows на LangGraph (production durability)
3. **Фаза 3:** Гибрид (CrewAI для новых фич, LangGraph для критичных путей)

## Типовые failure modes (2026)

- **35% coordination breakdowns:** агенты не синхронизируются, дублируют работу
- **Неконтролируемые затраты:** нет token caching, избыточные API calls
- **Нет visibility:** невозможно отследить ошибки агентов в проде
- **Compliance gaps:** нет audit trails для регулируемых отраслей

## Источники

- [Gurusup: Best Multi-Agent Frameworks 2026](https://gurusup.com/blog/best-multi-agent-frameworks-2026)
- [DEV Community: LangGraph vs CrewAI Complete Guide](https://dev.to/pockit_tools/langgraph-vs-crewai-vs-autogen-the-complete-multi-agent-ai-orchestration-guide-for-2026-2d63)
