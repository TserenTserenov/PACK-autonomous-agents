---
id: AS.M.005
type: method
title: Agentic Plan Caching
status: active
source: NeurIPS 2025, arXiv:2506.14852
date: 2026-01
---

# AS.M.005: Agentic Plan Caching (APC)

## Проблема

Агенты при каждой похожей задаче переделывают planning с нуля → высокая latency + cost. Среднее решение GitHub issue через агента: 48.4K tokens trajectory, 1.0M accumulated tokens.

## Решение

Test-time memory система: extract, store, adapt, reuse structured plan templates из прошлых executions для семантически похожих задач.

## Ключевое различение: Semantic Caching ≠ Plan Caching

| Аспект | Semantic Caching | Agentic Plan Caching |
|--------|------------------|---------------------|
| **Что кэшируется** | Результаты (outputs) | Планы выполнения (plans) |
| **Когда применимо** | Идентичные запросы | Семантически похожие задачи |
| **Адаптация** | Нет (as-is) | Да (template → specific plan) |
| **Scope** | Single-turn | Multi-step execution |

## Алгоритм

### Phase 1: Plan Extraction
После завершения task execution:
1. Analyze completed trajectory
2. Extract abstract plan structure (steps, dependencies, decision points)
3. Remove task-specific details → template

### Phase 2: Plan Storage
1. Index по keyword embeddings + structural features
2. Store с metadata (success rate, avg execution time)

### Phase 3: Plan Matching
1. Keyword-based retrieval (top-K similar plans)
2. Structural similarity check
3. Select best match

### Phase 4: Plan Adaptation
1. Lightweight LLM reads cached template + new task specifics
2. Fill task-specific parameters, adjust constraints
3. Output: task-specific plan ready for execution

## Performance (Production Benchmarks, 2026)

- **Cost reduction:** 50.31% в среднем
- **Latency reduction:** 27.28%
- **Quality retention:** 96.61% от optimal performance
- **Overhead:** 1.04% от total serving cost (negligible)

## Use Cases в IWE

1. **Scheduler.sh (WP-132):** Daily/weekly rituals — одинаковые паттерны задач → ~2x speedup
2. **Scout (R23):** Reconnaissance pipeline кэшируется, адаптируется под новые sources
3. **Экстрактор (R2):** Plan template per entity type (Distinction, Method, SOTA, FM)

## Failure Modes

| FM | Severity | Mitigation |
|----|----------|-----------|
| Overfitting к cached plan | Средний | Similarity threshold, expiration TTL, performance monitoring |
| Cold start | Низкий | Seed cache с exemplar plans |
| Cache pollution | Низкий | Quality filter (только successful executions), success rate tracking |

## Связь с Pack

- **DP.SOTA.002 (Context Engineering):** APC requires structured context для plan matching
- **AS.M.001 (Trust Stack / GEPA):** GEPA optimizes plans through reflection; APC reuses optimized plans
- **DP.SOTA.006 (Coordination Cost):** APC снижает coordination overhead

## Источники

1. arXiv:2506.14852 (updated Jan 2026): «Agentic Plan Caching: Test-Time Memory for Fast and Cost-Efficient LLM Agents»
2. NeurIPS 2025 Poster
