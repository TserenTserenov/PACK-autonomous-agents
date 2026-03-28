---
id: AS.SOTA.005
name: "Cognitive Runtime for Agent Verification (ElephantBroker, 2026)"
type: sota
status: active
created: 2026-03-28
source: "arXiv:2603.25097, Lupascu & Lupascu, March 2026"
related: [AS.M.001, AS.M.004, AS.M.005, AS.M.006, AS.FM.019, AS.FM.018, AS.SOTA.003]
s2r_families: [F5, F8]
---

# AS.SOTA.005: Cognitive Runtime для верификации агентов (2026)

## Суть

**ElephantBroker** — когнитивная среда исполнения (cognitive runtime), объединяющая persistent knowledge graph memory, evidence-driven verification, goal-aware context assembly и safety enforcement в единый runtime. Ключевое отличие от существующих подходов: верификация агента **во время работы** (runtime), а не только pre-deployment.

## Различение: Runtime Verification ≠ Pre-Deployment Testing

| Аспект | Pre-Deployment Testing (GEPA) | Runtime Verification (Cognitive Runtime) |
|--------|-------------------------------|----------------------------------------|
| Когда | До деплоя | Во время выполнения агента |
| Что проверяет | Expected behavior в test environment | Actual behavior в production |
| Реакция на ошибку | Fix & redeploy | Intervention / circuit breaker / require_evidence |
| Coverage | Предусмотренные тест-кейсы | Все edge cases (включая неожиданные) |
| Overhead | Нет production overhead | Runtime cost (latency, compute) |
| Пример | Unit tests, GEPA validation | ElephantBroker cognitive loop |

## Архитектура: 6-фазный когнитивный цикл

**Store → Retrieve → Score → Compose → Protect → Learn**

1. **Store:** факты с типизированным provenance, dual graph-vector индексы (Neo4j + Qdrant)
2. **Retrieve:** 5-source hybrid search (параллельный запрос к нескольким хранилищам)
3. **Score:** 11-мерная конкурентная оценка с budget-constrained selection
4. **Compose:** контекст собирается в 4 блока на 2 промпт-поверхностях (constraints → goals → scored items → evidence)
5. **Protect:** 6-слойный guard pipeline + AI firewall с tool-call interception
6. **Learn:** 9-стадийная консолидация — усиление полезных паттернов, затухание бесполезных

## 4-State Evidence Verification Model

```
Unverified (mᵥ=0.5)
  ↓ [evidence attached]
Self-Supported (mᵥ=0.7)
  ↓ [tool output]
Tool-Supported (mᵥ=0.9)
  ↓ [supervisor sign-off]
Supervisor-Verified (mᵥ=1.0)
```

Состояние верификации напрямую влияет на scoring через confidence multiplier. Структурное предпочтение trustworthy information → инцентив к сбору evidence.

## 11-мерная система скоринга

**Pass 1 (независимые, per candidate):**
1. Turn relevance (cosine similarity)
2. Session goal relevance (direct=1.0, indirect=0.7)
3. Global goal relevance
4. Recency (exponential decay, half-life 12-720h по профилю)
5. Successful use prior (ratio success/total)
6. Confidence (raw × verification multiplier 0.5-1.0)
7. Evidence strength
8. Novelty (0 если compacted)
9. Cost penalty (tokens / budget)

**Pass 2 (interaction-dependent, greedy selection):**
10. Redundancy penalty (cosine > 0.85 к уже выбранным)
11. Contradiction penalty (graph edges: supersession=-1.0, contradiction=-0.9)

Submodular greedy selection: гарантия (1−1/e) ≈ 0.63 оптимальности.

## 6-слойный Guard Pipeline

| Layer | Механизм | Стоимость |
|-------|----------|-----------|
| 0 | Autonomy domain classification (10 доменов × 4 уровня) | Нулевая |
| 1 | Static rules (keyword, regex, tool target) | Нулевая |
| 2 | Semantic matching (BM25 + cosine vs known-bad) | Минимальная |
| 3 | Structural validation (graph queries) | Минимальная |
| 4 | Forced constraint reinjection | Нулевая |
| 5 | LLM escalation (для ambiguous cases) | Высокая |

**Вердикты:** pass, warn, block, require_approval (HITL), require_evidence.
**Auto-tightening:** 3 near-misses за 5 turns → strictness повышается автоматически.

## 9-стадийная консолидация (Learning)

Работает в idle periods. Ключевые стадии:
1. Cluster near-duplicates (cosine ≥ 0.92, zero LLM)
2. Canonicalize (majority voting)
3. Strengthen useful facts: c′ = min(c + s/u × 0.3, 1.0)
4. Decay unused facts (recalled-never-used: ×0.9^t, never-recalled: ×0.95^t)
5. Prune auto-recall (≥5 recalls, 0 uses → blacklist)
6. Promote episodic → semantic (≥3 sessions)
7. Refine procedures (recurring step patterns → new procedures)
8. Identify verification gaps
9. Recompute salience (EMA, ±5% cap per cycle)

## Сравнение с существующими системами

ElephantBroker vs Zep, Mem0, MemGPT, Lossless-Claw — по 19 capability dimensions. Только ElephantBroker реализует: evidence tracking, goal-aware scoring, budget-constrained working sets, guard pipelines, consolidation, enforceable guards, AI safety scanning.

**Ограничение:** нет количественных benchmarks (retrieval latency, accuracy). Фокус на архитектурной полноте.

## Импликации для IWE

| Компонент ElephantBroker | Аналог в IWE | Статус |
|--------------------------|-------------|--------|
| Evidence verification (4-state) | Pack как source-of-truth + Dedup Gate | Зачаток есть |
| Guard pipeline (6-layer) | Pilot-First + pre-push hook | Частично |
| 11-dim scoring | Нет (контексты собираются вручную) | Нет |
| Consolidation (9-stage) | Scout trajectory (rules, accepted, rejected) | Зачаток есть |
| Goal-aware context assembly | WP context files + MEMORY.md | Частично |
| AI firewall + tool interception | Нет | Нет |

**Применение:**
- **Scout (WP-132):** evidence verification model для captures (Unverified → Self-Supported → Tool-Supported при Pack Index check)
- **Бот:** guard pipeline для ответов пользователям (runtime safety)
- **WP-179 Phase 2:** drift detection через consolidation engine (decay unused, strengthen useful)
- **Общая архитектура:** 4-state verification = естественное расширение Trust Stack (AS.M.001)

## Источники

1. Lupascu, C. & Lupascu, A. (2026). ElephantBroker: A Knowledge-Grounded Cognitive Runtime for Trustworthy AI Agents. arXiv:2603.25097.
   URL: https://arxiv.org/abs/2603.25097
