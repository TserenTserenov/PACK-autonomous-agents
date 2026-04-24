---
id: AS.SOTA.007
name: "Automated Research Agents — Closed-Loop Scientific Research (2026)"
type: sota
status: active
created: 2026-04-24
source: "Anthropic Alignment Blog: 'Automated Weak-to-Strong Supervision Researcher' (April 2026); Scout 23 апр 2026 (rt-005)"
related: [AS.D.006, AS.D.009, AS.M.006, AS.SOTA.002, AS.SOTA.006]
s2r_families: [F8]
summary: "Параллельные агенты Claude в минимально прескриптивной среде (shared forum + shared code, без workflow scaffolding) обогнали команду людей в open-ended research task. Ключ: verifiable goal + shared knowledge pool."
---

# AS.SOTA.007: Automated Research Agents — Closed-Loop Scientific Research (2026)

## 1. Контекст

Anthropic, апрель 2026. Задача — автоматизация исследования **weak-to-strong supervision** (подхода, при котором более слабая модель надзирает за более сильной). Эксперимент: может ли команда автономных агентов провести open-ended research task, традиционно требующий человеческого исследователя?

## 2. Архитектура

| Компонент | Описание |
|-----------|----------|
| **Executors** | N параллельных Claude Opus 4.6 агентов в независимых sandbox-окружениях |
| **Shared forum** | Общее хранилище находок: каждый агент пишет свои результаты и читает результаты остальных |
| **Shared code** | Общее хранилище кода: snapshots, которые любой агент может поднять и развивать |
| **Scaffolding** | Минимальный. Нет детализации workflow, нет фиксированных ролей |
| **Goal definition** | Цель + метрика верификации (verifiable outcome) |

## 3. Результат

**Агенты обогнали команду человеческих исследователей** по скорости и качеству решения проблемы W2S supervision.

Anthropic цитирует ключевой вывод:
> "Human-prescribed workflows unnecessarily constrain the agents' flexibility and degrade performance."

## 4. Дизайн-принципы (для проектировщиков агентных систем)

1. **Минимальный scaffolding для open-ended задач.** Детальные workflow-прескрипции снижают производительность — агент лучше справляется сам, если цель чётко верифицируема.
2. **Verifiable goal обязателен.** Без объективной метрики успеха improvement loop не работает (см. AS.D.009).
3. **Shared knowledge pool вместо изолированных агентов.** Форум + общий код = коллективная семантическая память (см. AS.M.006), эмерджентная координация без supervisor'а.
4. **Параллелизм > последовательность.** Несколько агентов в независимых sandbox расширяют пространство поиска.

## 5. Противопоставление 2025→2026

| 2025 (AS.SOTA.002 baseline) | 2026 (этот кейс) |
|------------------------------|------------------|
| Explicit orchestration (supervisor/pipeline/hierarchical) | Emergent coordination через shared forum |
| Human-prescribed workflows | Minimal scaffolding, верифицируемая цель |
| Single-agent improvement | Collective improvement через общее знание |

Этот кейс подтверждает shift в сторону **collective multi-agent reasoning** (AS.SOTA.006 Layer 3) для задач с verifiable outcome, но одновременно соседствует с обратным трендом для production-workflows (см. AS.SOTA.002 Controllable Orchestration).

## 6. Условия применимости

Кейс работает, когда:
- Задача **верифицируема** (W2S имел формальную метрику качества надзора) → AS.D.009
- Пространство решений **широкое** (нет единственного правильного пути)
- Параллельная работа **не создаёт конфликтов** (agent sandboxes изолированы)

Когда **не работает**:
- Non-verifiable domains (стратегия, стиль, ценности) — см. AS.D.009
- Production workflows с требованием debuggability / human-in-the-loop (контркейс: AS.SOTA.002 controllable orchestration 2026)
- Задачи с единой правильной последовательностью шагов (там scaffolding даёт выигрыш)

## 7. Импликации для IWE

- **Для R23 Scout и R2 Экстрактор:** подтверждена гипотеза «роль + верифицируемая цель + общее знание → лучше, чем прописанный workflow». Scout уже работает в этой парадигме (цель: «что нового в мире», верификация через accepted/rejected).
- **Для будущих агентов:** если появляется задача с проверяемым выходом (например, автоматический Verifier или Extractor pool) — закладывать shared forum + minimal scaffolding, а не жёсткий pipeline.
- **Граница применимости:** для Диагноста/Портного/Навигатора (non-verifiable outputs) этот паттерн неуместен — там нужен human gate.

## 8. Связи

| Сущность | Связь |
|----------|-------|
| AS.D.006 (Execution Loop ≠ Improvement Loop) | Кейс = успешный improvement loop на verifiable задаче |
| AS.D.009 (Verifiable ≠ Non-Verifiable) | Верифицируемость цели = ключевое условие успеха |
| AS.M.006 (Four-Type Memory) | Shared forum = коллективная семантическая память |
| AS.SOTA.002 (Multi-Agent Orchestration) | Контркейс для production: controllable orchestration vs emergent для research |
| AS.SOTA.006 (Three-Layer Framework) | Кейс демонстрирует Layer 3 (Collective) на verifiable task |

## 9. Источники

- [Anthropic Alignment: Automated W2S Researcher (April 2026)](https://alignment.anthropic.com/2026/automated-w2s-researcher/)
