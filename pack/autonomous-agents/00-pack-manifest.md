# Pack Manifest: Автономные саморазвивающиеся агенты

## Идентификатор

- **Pack ID**: `AS`
- **Версия**: 0.1.0
- **Статус**: Draft

## Область

**Название**: Автономные саморазвивающиеся агенты

**Описание**: Предметная область проектирования, развития и эксплуатации автономных саморазвивающихся ИИ-агентов: стадии зрелости (T0→T4), петли самоулучшения, типы памяти агента, governance автономности (Trust Stack, Graduated Governance), trajectory caching, reflexion, self-challenging, метакогнитивные способности.

## Scope

### В scope

- Архитектура автономного агента (отличие от реактивного и полуавтономного)
- Стадии зрелости агента (T0–T4)
- Петли самоулучшения (improvement loop vs execution loop)
- Типы памяти агента (эпизодическая, семантическая, процедурная)
- Governance автономности (Trust Stack, Graduated Governance, Bounded Agency)
- Классификация агентов (7-dimension model: функция, роль, предсказуемость, автономия, авторитет, use case, среда)
- Методы: trajectory caching, reflexion, self-challenging
- Failure modes автономных агентов
- SOTA в области агентного ИИ (self-improvement, world models)
- Fine-tuning на агентных данных (за границей DP)

### Вне scope

- Код конкретных агентов (это DS-autonomous-agents — downstream/instrument)
- Архитектура платформы IWE (это PACK-digital-platform)
- Верификация результатов агентов (это PACK-verification)
- Детерминированные системы и MCP (это DP)

## Расширенные виды (SPF.SPEC.001)

| Код | Вид | Описание | Папка |
|-----|-----|----------|-------|
| `LIFECYCLE` | Lifecycle | Стадии жизненного цикла агента | `02-domain-entities/` |
| `ARCH` | Architecture | Архитектурное описание автономного агента | `02-domain-entities/` |
| `CYCLE` | Cycle | Петли и циклы самоулучшения | `02-domain-entities/` |

## Содержимое Pack'а

| Категория | Файлов | Ключевые сущности |
|-----------|--------|-------------------|
| Доменный контракт | 2 | Bounded context, онтология |
| Различения | 4 | AS.D.001–D.004 |
| Доменные сущности | 0 | (будут по мере реализации) |
| Методы | 0 | (будут по мере реализации) |
| Failure modes | 0 | (будут по мере реализации) |
| SOTA | 0 | (будут по мере реализации) |

## Entity Index

| ID | Name | Kind | Summary | Status |
|----|------|------|---------|--------|
| AS.D.001 | Автономия ≠ Автоматизация | D | Автоматизация = надёжное исполнение запрограммированного. Автономия = гибкость принятия решений. Принципиально разные классы систем с разными требованиями к governance | draft |
| AS.D.002 | Агент = Исполнитель + Роль | D | Агент — не отдельная программа, а Claude Code в определённой роли. Именовать по роли: «Верификатор», не «agent-verifier» | draft |
| AS.D.003 | Роль ≠ Режим вызова | D | Роль определяет *что* делать (эталон, чеклист). Режим — *как* запускать (sub-agent / headless). «Reviewer» = Верификатор в ночном режиме, не отдельная роль | draft |
| AS.D.004 | Ядро роли ≠ Контекст вызова | D | Ядро (Pack: роль, метод, принципы) фиксировано. Контекст (эталон, файлы, чеклист) подставляется при вызове. Один промпт — разные задачи | draft |

## Upstream dependencies

- [PACK-digital-platform](../../../PACK-digital-platform/) — платформа как runtime
- [PACK-verification](../../../PACK-verification/) — верификация результатов
- [SPF](https://github.com/TserenTserenov/SPF) — Second Principles Framework

## Downstream outputs

- [DS-autonomous-agents](../../../DS-IT-systems/DS-autonomous-agents/) — реализация агентов (instrument)

## Maintainers

- @TserenTserenov

## Changelog

- 0.1.0 — Initial structure: BC, первое различение (AS.D.001)
