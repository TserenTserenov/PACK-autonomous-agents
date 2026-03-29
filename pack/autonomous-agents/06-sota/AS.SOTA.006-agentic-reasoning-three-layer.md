---
id: AS.SOTA.006
name: "Agentic Reasoning — Three-Layer Framework (2026)"
type: sota
status: active
created: 2026-03-29
source: "arxiv:2601.12538 'Agentic Reasoning for Large Language Models' (Jan 2026), Scout 29 мар 2026"
related: [AS.D.006, AS.M.005, AS.M.006, AS.SOTA.002, AS.M.001, AS.M.004]
s2r_families: [F8]
summary: "Архитектурный паттерн: три слоя способностей агента (foundational → self-evolving → collective). Agent = actor in environment, не text predictor"
---

# AS.SOTA.006: Agentic Reasoning — Three-Layer Framework (2026)

## 1. Определение

**Agentic reasoning** — парадигмальный сдвиг от реактивных LLM (генерация текста) к автономным агентам (планирование, действие, обучение через непрерывное взаимодействие со средой). LLM переосмысляются как actors, не generators.

**Ключевое различение:** Agent = actor in environment (state → action → new state loop). LLM = text predictor (prompt → completion).

## 2. Three-Layer Framework

### Layer 1: Foundational Agentic Reasoning

Базовые способности одиночного агента:

- **Planning** — декомпозиция задач, секвенирование шагов
- **Tool use** — function calling, API interaction
- **Reasoning** — chain-of-thought, reflection
- **Memory** — episodic, semantic, procedural, working (см. AS.M.006)

### Layer 2: Self-Evolving Agentic Reasoning

Агент совершенствует собственные способности через обратную связь:

- **Improvement loop** (AS.D.006: Execution Loop ≠ Improvement Loop)
- **Reflexion** — self-critique + retry
- **Self-challenging** — генерация более сложных тестов
- **Trajectory caching** (AS.M.005: переиспользование планов)

### Layer 3: Collective Multi-Agent Reasoning

Коллективный интеллект:

- **Координация** — consensus, negotiation между агентами
- **Распределённое решение** — разные агенты решают разные подзадачи
- **Обмен знаниями** — cross-agent memory synchronization
- **Эмерджентные способности** — целое > сумма частей

## 3. Связь с существующими сущностями

| Сущность | Связь |
|----------|-------|
| AS.D.006 (Execution ≠ Improvement Loop) | Layer 2 = формализация improvement loop |
| AS.M.006 (Four-Type Memory) | Layer 1 foundational capability |
| AS.M.005 (Agentic Plan Caching) | Layer 2 self-evolution mechanism |
| AS.SOTA.002 (Multi-Agent Orchestration) | Layer 3 collective reasoning (frameworks как реализация) |
| AS.M.001 (Trust Stack Design) | Governance применяется ко всем 3 layers |
| AS.M.004 (Graduated Governance) | Graduated по layers (см. §5) |

## 4. Failure Modes по layers

| Layer | Типичные FM |
|-------|-------------|
| Layer 1 | AS.FM.012 (specification), AS.FM.016 (tool misuse) |
| Layer 2 | AS.FM.019 (behavioral drift — improvement loop не детектирует degradation) |
| Layer 3 | AS.FM.015 (multi-agent communication), AS.FM.019 (coordination drift) |

## 5. Graduated Governance по layers

| Layer | Tier governance | Описание |
|-------|----------------|----------|
| Foundational (L1) | Tier 1 | Full human oversight |
| Self-evolving (L2) | Tier 2 | Approval required для self-modifications |
| Collective (L3) | Tier 3 | Consensus mechanisms + audit trail |

## 6. Различение: AS.SOTA.006 ≠ DP.SOTA.006

| | AS.SOTA.006 | DP.SOTA.006 |
|---|-------------|-------------|
| **Фокус** | Agents как autonomous reasoners | Agents помогают разработке |
| **Scope** | Domain-agnostic framework | Platform engineering |
| **Объект** | Архитектура способностей агента | Workflow разработки |

## 7. Статус SOTA (январь 2026)

**SOTA, формализация.** Research community сходится на three-layer taxonomy. Production-реализации:

- **AutoGen** — conversations (Layer 3, maintenance mode)
- **CrewAI** — role-based teams (Layer 3 prototyping)
- **LangGraph** — graph-based stateful (все layers, production leader)

## 8. Источники

- arxiv:2601.12538 «Agentic Reasoning for Large Language Models» (Jan 2026)
