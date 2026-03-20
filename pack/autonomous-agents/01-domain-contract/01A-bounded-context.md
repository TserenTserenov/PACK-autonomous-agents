# Bounded Context: Автономные саморазвивающиеся агенты

## Определение области

**Автономный саморазвивающийся агент** — ИИ-система, способная (1) самостоятельно принимать решения о действиях в рамках заданных границ, (2) улучшаться со временем через петли обратной связи, и (3) работать без присутствия пользователя.

**Ключевое отличие от реактивных агентов (Grade 0-2):** реактивный агент выполняет фиксированный промпт при триггере. Автономный агент **выбирает**, что делать, и **учится** делать лучше.

## Ключевые понятия

| Термин | Определение |
|--------|-------------|
| **Автономия** | Гибкость принятия решений: агент сам выбирает *что* делать (WEF, 2026) |
| **Автоматизация** | Надёжное исполнение запрограммированного: система делает *что ей сказали* |
| **Trajectory** | Полная запись сессии агента: промпт → действия → результат → оценка |
| **Trajectory Cache** | Хранилище успешных траекторий как few-shot примеров для будущих сессий |
| **Reflexion** | Мультипроходная критика с context isolation: создание → критика (другой контекст) → исправление |
| **Self-Challenging** | Агент сам генерирует тест-кейсы для проверки своей работы |
| **Trust Stack** | Многослойная модель доверия: legible reasoning → bounded agency → goal transparency → contestability (WEF) |
| **Graduated Governance** | Принцип: больше автономии → пропорционально больше надзора |
| **Bounded Agency** | Чёткие границы полномочий агента без скрытой эскалации автономии |
| **Agent Card** | Паспорт агента по 7 измерениям: функция, роль, предсказуемость, автономия, авторитет, use case, среда |
| **Improvement Loop** | Замкнутая петля: выполнение → оценка → обратная связь → обновление → лучшее выполнение |
| **Execution Loop** | Петля исполнения одной задачи: plan → act → observe → repeat (без обучения между сессиями) |
| **Agent Maturity (T0–T4)** | Стадии зрелости: T0 (скрипт) → T1 (LLM headless) → T2 (feedback loop) → T3 (self-improvement) → T4 (self-challenging + fine-tuning) |

## Границы области

### Что входит

- Проектирование автономных агентов (архитектура, память, governance)
- Стадии зрелости и переходы между ними
- Петли самоулучшения (improvement loops)
- Типы памяти агента и их реализация
- Trust Stack и Graduated Governance
- Классификация агентов (WEF 7-dimension model)
- Методы: trajectory caching, reflexion, self-challenging
- Failure modes автономных агентов
- Fine-tuning на агентных данных

### Что НЕ входит

- Код конкретных агентов (DS-autonomous-agents — downstream/instrument)
- Архитектура платформы и harness engineering (PACK-digital-platform)
- Верификация результатов (PACK-verification)
- Роли и назначения (DP.ROLE.001)
- Детерминированные системы и scheduler (DS-ai-systems)

## Связь с другими Pack'ами

| Pack | Тип связи |
|------|-----------|
| PACK-digital-platform | Платформа как runtime; различения DP.D.009, DP.D.025, DP.D.033; SOTA DP.SOTA.006 |
| PACK-verification | Верификация результатов агентов (VR.R.001, VR.SOTA.001) |
| PACK-personal | Модель агента как созидателя (PD.FORM.018, PD.FORM.054) |
| SPF | Форма и процесс для Pack-сущностей |

## Источники

- WEF «AI Agents in Action: Foundations for Evaluation and Governance» (2025/2026)
- Reflexion: reflective agents (HuggingFace)
- Memory in the Age of AI Agents (arxiv.org/abs/2512.13564)
- Self-Improving AI through Self-Play (arxiv.org/abs/2512.02731)
