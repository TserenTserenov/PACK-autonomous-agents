---
id: AS.FM.019
type: failure-mode
title: Behavioral Drift in Multi-Agent Systems
status: active
source: "CIO (Agentic AI Drift), Machine Learning Mastery (Production Scaling), CSA, arxiv:2601.04170, arxiv:2506.10095, Maxim AI Guide (2026)"
date: 2026-03-28
updated: 2026-03-29
severity: critical
---

# AS.FM.019: Behavioral Drift in Multi-Agent Systems

## Описание

Постепенная деградация поведения агентной системы в production (недели-месяцы), вызванная incremental changes: обновления моделей, изменения промптов, добавление инструментов, обновление зависимостей. Cloud Security Alliance (CSA) классифицирует как **cognitive degradation** — системный риск, возникающий градуально, не внезапно.

## Severity: Критический

Каждое изменение individually safe, но cumulatively — behavior shifts. Невоспроизводим в staging.

## Различение: AS.FM.019 ≠ DP.FM.005 (Model-Reality Drift)

| Аспект | DP.FM.005 (Model-Reality Drift) | AS.FM.019 (Behavioral Drift) |
|--------|--------------------------------|------------------------------|
| Объект | Статичная модель (representation) | Динамичная система агентов (behavior) |
| Причина | Реальность меняется, модель устаревает | Система меняется изнутри (updates, config drift) |
| Временная шкала | Месяцы-годы (медленный external drift) | Недели-месяцы (быстрый internal drift) |
| Детектируется | Метрики качества модели (accuracy drop) | Поведенческие аномалии (execution path changes) |
| Mitigation | Ретренинг модели | Version control, regression testing, observability |

## Сценарий

1. Multi-agent система работает стабильно 3 месяца
2. Постепенно: LLM provider обновляет модель (minor version), разработчик добавляет tool, меняет промпт, обновляет dependency
3. Каждое изменение individually safe, но cumulatively — behavior shifts
4. Результат: agents waiting on agents, race conditions, cascading failures, non-deterministic execution paths
5. Симптомы: latency increase, completion rate drop, "weird behavior" — но нет явной ошибки в логах

## Таксономия дрейфа (arxiv 2601.04170, Jan 2026)

Три типа Agent Drift — progressive degradation через extended interaction:

| Тип | Описание | Пример |
|-----|----------|--------|
| **Semantic drift** | Постепенное отклонение от исходного intent агента | Scheduler приоритизирует urgent над important без явного указания |
| **Coordination drift** | Разрушение consensus mechanisms между агентами | Агенты дублируют задачи, теряя синхронизацию |
| **Behavioral drift** | Появление непредусмотренных стратегий | Агент начинает «обходить» constraints, которые не нарушает формально |

**PBSS Framework (Prompt-Based Semantic Shift):** семантически эквивалентные промпты → разные outputs из-за tokenization/decoding artifacts. Дрейф происходит **без изменений промпта** — versioning текста недостаточен, нужна **behavioral observability**.

### Различение: два механизма дрейфа

| | Config-Driven Drift (§ «Сценарий») | Spontaneous Drift (PBSS) |
|---|---|---|
| **Причина** | Обновления моделей, промптов, tools | Tokenization/decoding artifacts |
| **Триггер** | Explicit change (код, конфиг) | Нет — дрейфует без изменений |
| **Детектируется** | Version control + regression | Behavioral snapshots + continuous eval |
| **Временная шкала** | Недели-месяцы (incremental updates) | Часы-дни (extended interaction) |

## Mitigation

- **Behavioral Snapshots:** зафиксировать эталонное поведение (вход X → ожидаем Y). При каждом изменении — regression suite
- **Prompt/Tool Versioning:** все конфигурации в git. Промпт + инструменты + параметры модели = версионированный контракт
- **Deep Observability:** трассировка execution paths, behavior distribution monitoring, drift detection metrics
- **Staged Rollouts:** canary deployment с behavior monitoring (10% трафика → мониторинг → раскатка)
- **Circuit Breakers:** автоматический rollback если behavior divergence > threshold
- **Continuous Evaluation:** real-time monitoring outputs vs expected patterns (не только при deploys, но и в steady-state)

## Связь с IWE

- **DP.FM.005** (Model-Reality Drift) — смежный drift, но другой объект (external vs internal)
- **AS.FM.013** (Reasoning Loops) — может быть следствием behavioral drift
- **WP-179** (GEPA Test Framework) — drift detection как Phase 2 (Ф7)
- **WP-132** (scheduler.sh) — vulnerable без monitoring; промпты уже в git (mitigation частично)
- **AS.M.001** (Trust Stack) — observability layer

## Связь с AS.SOTA.006 (Three-Layer Framework)

- **Layer 2 failures:** дрейф improvement loop — агент «самосовершенствуется» в неверном направлении
- **Layer 3 failures:** coordination drift — агенты теряют consensus без явных ошибок

## Источники

1. CIO: Agentic AI Systems Don't Fail Suddenly — They Drift Over Time
   URL: https://www.cio.com/article/4134051/agentic-ai-systems-dont-fail-suddenly-they-drift-over-time.html
2. Machine Learning Mastery: 5 Production Scaling Challenges for Agentic AI in 2026
   URL: https://machinelearningmastery.com/5-production-scaling-challenges-for-agentic-ai-in-2026/
3. arxiv:2601.04170 «Agent Drift: Quantifying Behavioral Degradation» (Jan 2026)
4. arxiv:2506.10095 «When Meaning Stays the Same, but Models Drift: Token-Level Behavioral Instability»
5. Maxim AI: «Guide to Preventing AI Agent Drift Over Time» (2026)
   URL: https://www.getmaxim.ai/articles/a-comprehensive-guide-to-preventing-ai-agent-drift-over-time/
