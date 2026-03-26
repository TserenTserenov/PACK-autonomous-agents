---
id: AS.M.006
type: method
title: Four-Type Memory Architecture for Autonomous Agents
status: active
source: Oracle Developers Blog, 47billion, CoALA framework
date: 2026
---

# AS.M.006: Four-Type Memory Architecture for Autonomous Agents

## Проблема

Большинство агентов имеют ТОЛЬКО working memory (текущее context window). «That's like trying to do your job using nothing but a whiteboard that gets wiped clean every evening.»

Production failures (2026): агенты забывают предпочтения пользователя между сессиями, повторяют ошибки, не могут накапливать domain expertise, неэффективны (re-learn procedures на каждой задаче).

## Решение

4 типа памяти, mapping to human cognition (CoALA framework):

### 1. Working Memory
- **Что:** Текущее context window (most agents have ONLY this)
- **Аналогия:** Оперативная память, whiteboard
- **Характеристики:** Volatile, ограничен token budget, высокая скорость
- **IWE:** Текущая сессия с агентом (ephemeral)

### 2. Episodic Memory
- **Что:** Что произошло (timestamped events, conversation turns, tool calls)
- **Аналогия:** Дневник, timeline
- **Характеристики:** Temporal ordering, конкретные instances
- **IWE:** РП-история, session logs, open-sessions.log

### 3. Semantic Memory
- **Что:** Что я знаю (факты, политики, доменное знание)
- **Аналогия:** Энциклопедия, справочник
- **Характеристики:** Generalized knowledge, no temporal ordering
- **IWE:** Pack entities, ЦД характеристики, CLAUDE.md

### 4. Procedural Memory
- **Что:** Как делать (workflows, playbooks, processes)
- **Аналогия:** Мышечная память, рецепты
- **Характеристики:** Executable patterns, implicit knowledge
- **IWE:** PROCESSES.md, protocol-*.md, skills, trajectory/rules.md

## Production Challenges (2026)

### Storage vs Inference trade-off
Full history = cost explosion. Решение: hierarchical memory + importance scoring + dynamic forgetting.

### Latency
Постоянные retrieve/store decisions замедляют response. Решение: tiered access (hot/warm/cold).

### Forgetting
Самый сложный challenge: когда и что удалять? Решение: importance decay, usage-based eviction, versioned snapshots.

## Database Architecture Patterns

| Storage | Лучше для | Слабость |
|---------|----------|----------|
| Vector DB | Semantic similarity (semantic memory) | Слабый multi-hop reasoning |
| Graph DB | Fast traversal (episodic + procedural) | Сложность schema evolution |
| SQL/Postgres | ACID compliance, auditable (все типы) | Медленный semantic search |

## Связь с Pack

- **AS.FM.014 (Memory Corruption):** integrity каждого типа памяти
- **AS.M.005 (Plan Caching):** procedural memory optimization
- **DP.SOTA.002 (Context Engineering):** memory = component of Context Package
- **DP.AGENT.001 (архитектура агента):** memory architecture blueprint

## Источники

1. Oracle Developers Blog: «Agent Memory: Why Your AI Has Amnesia and How to Fix It» (2026)
2. 47billion: «AI Agent Memory: Types, Implementation, Best Practices 2026»
3. MachineLearningMastery: «Beyond Short-term Memory: The 3 Types of Long-term Memory AI Agents Need»
