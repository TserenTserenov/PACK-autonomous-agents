---
id: AS.SOTA.003
name: "Global Agentic AI Governance (WEF/Singapore 2026)"
type: sota
status: active
created: 2026-03-23
source: "WEF AI Agents in Action (2026), Singapore IMDA Agentic AI Framework (2026), Scout 22 мар 2026"
related: [AS.M.001, AS.M.004, AS.D.001, AS.SOTA.001]
s2r_families: [F8]
---

# AS.SOTA.003: Глобальное governance для агентного AI (WEF/Singapore 2026)

## Контекст

22 января 2026, World Economic Forum, Singapore IMDA представил **Model AI Governance Framework for Agentic AI** — первый в мире специализированный фреймворк governance для автономных AI-систем.

## Ключевые принципы

### 1. Progressive Governance

Safeguards расширяются вместе с операционным scope агента. Не one-size-fits-all, а graduated по зрелости.

### 2. Bounded Autonomy

Автономия должна быть **заработана** через продемонстрированную надёжность:
- Старт с чётких операционных лимитов
- Escalation paths для high-stakes решений
- Comprehensive audit trails

### 3. Agentic Trust Framework (ATF)

Zero Trust принципы, применённые к AI-агентам. 4 уровня зрелости с прогрессивным расширением автономии и governance.

## 4 уровня зрелости (ATF)

| Уровень | Автономия | Governance | Пример |
|---------|-----------|-----------|--------|
| **L1: Reactive** | Минимальная (human-triggered) | Базовый logging | ChatGPT, Claude chat |
| **L2: Proactive** | Средняя (agent предлагает, human одобряет) | Approval gates, audit logs | Email drafts, code suggestions |
| **L3: Autonomous** | Высокая (agent выполняет, human мониторит) | Real-time monitoring, rollback, escalation | Scheduling, data processing |
| **L4: Fully Autonomous** | Полная (agent владеет outcomes) | Comprehensive: continuous monitoring, automated guardrails, compliance, insurance/liability | Medical diagnosis, financial trading |

## Компоненты governance

### Operational Limits
Определить границы: что агент МОЖЕТ делать vs ОБЯЗАН НЕ делать.
Пример: Scout может read/search, не может писать в Pack.

### Escalation Paths
High-impact решения → human approval.
Пример: агент нашёл критичный баг → эскалация до human перед деплоем фикса.

### Audit Trails
Каждое решение залоговано: input → reasoning → action → outcome.
Регуляторное требование для L3-L4 агентов.

### Monitoring & Rollback
Real-time monitoring для detecting drift (изменение поведения агента).
1-click rollback для failed actions.

## Маппинг на IWE

| IWE-агент | ATF Level | Governance |
|-----------|-----------|-----------|
| scheduler.sh | L1 (Reactive) | Базовый logging |
| Scout (Idea Scout) | L2-L3 | Trajectory cache, human review |
| Strategist | L2 | Human approval на dayplan |
| Будущий Fixer | L3 | Approval gates, audit, rollback |

## Production Adoption Data (2026)

> Обогащение: Scout 26 мар 2026 (LangGraph, Iterathon, IBM Research)

**Multi-agent orchestration в production:**
- 40% of enterprise apps will feature task-specific agents (up from <5% in 2025)
- **BUT:** only 10-15% of pilots reach production
- 86% of copilot spending ($7.2B) → agent-based systems
- **75% of multi-agent systems become unmanageable beyond 5 agents**

**Production-grade patterns:**
- State management: SQLite-based persistence, checkpoint recovery
- Monitoring: Human-in-the-loop checks, observability (LangSmith)
- Architecture: Structured message bus, ACP logging

**Coordination cost (IBM Research):**
- Process hand-offs: **-45%** с intelligent routing
- Decision speed: **3x improvement**
- Mitigation: team size limits (3-7 agents per workflow), hierarchical beyond that

## Источники

- [WEF: AI Agents in Action](https://www.weforum.org/publications/ai-agents-in-action-foundations-for-evaluation-and-governance/)
- [Singapore IMDA: Model AI Governance Framework for Agentic AI](https://www.imda.gov.sg/-/media/imda/files/about/emerging-tech-and-research/artificial-intelligence/mgf-for-agentic-ai.pdf)
- Iterathon: «Agent Orchestration 2026: LangGraph, CrewAI & AutoGen Guide» (2026)
- IBM Research: Multi-agent coordination metrics (2026)
