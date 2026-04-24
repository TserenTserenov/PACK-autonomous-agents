---
id: AS.D.009
name: Verifiable ≠ Non-Verifiable Domains
type: distinction
created: 2026-04-24
source: "Synthesis: OpenAI Self-Evolving Cookbook + o-mega.ai 2026 + Anthropic W2S Researcher (April 2026); Scout 23 апр 2026"
related:
  extends: [AS.D.006]
  uses: [AS.SOTA.007]
---

# AS.D.009: Verifiable ≠ Non-Verifiable Domains

## Суть различения

**Verifiable task domain** и **non-verifiable task domain** — две категории задач, различающиеся наличием объективной метрики успеха. Различение критично при проектировании **improvement loop** для автономного агента: на verifiable задачах петля замыкается сама, на non-verifiable — только через human-in-the-loop или переопределение метрики.

## Таблица сравнения

| Параметр | Verifiable | Non-Verifiable |
|----------|------------|----------------|
| **Суть** | Исход можно проверить объективно (ground truth существует) | Исход требует человеческого суждения (ground truth — субъективная оценка) |
| **Примеры** | Код (компилируется? тесты проходят?), математика (доказательство валидно?), алгоритм (метрика быстрее baseline?) | Стратегический совет, стиль письма, ценностные суждения, качество Pack-сущности |
| **Improvement loop** | Надёжен: generate → evaluate → keep/discard | Ненадёжен: нет объективной метрики, самосогласованность вместо близости к реальности |
| **Failure risk** | Низкий (petля сама отсекает плохие итерации) | Высокий: агент оптимизирует по субъективному прокси и деградирует (см. DP.FM.005) |
| **В IWE** | Тест ДЗ (pass/fail), code lint, schema validation | Качество Pack-сущности, стратегический совет Навигатора, формулировка цели |
| **Оптимальный дизайн** | Minimal scaffolding + shared knowledge pool (см. AS.SOTA.007) | Human gate на каждой итерации ИЛИ переопределение задачи в verifiable прокси |

## Критерий разграничения

**Тест:** «Можно ли написать `assert result == expected` или `metric(result) > threshold` без участия человека?»

- Да → verifiable
- Нет → non-verifiable

**Второй тест:** «Два компетентных эксперта, не сговариваясь, дадут одинаковую оценку результата?»

- Да (при наличии спецификации/тестов) → verifiable
- Нет (оценки расходятся) → non-verifiable

## Дизайн-правило для IWE

При проектировании improvement loop для агента **сначала проверь верифицируемость домена**:

1. **Verifiable** → автономный improvement loop допустим (генерация → метрика → отбор). Подходит: AS.SOTA.007 архитектура (параллельные агенты + shared forum).
2. **Non-verifiable** → одно из трёх:
   - **Human-in-the-loop** обязателен на каждой итерации (вариант по умолчанию)
   - **Переопределить задачу** в измеримый прокси (например, «качество Pack-сущности» → «прошла ли Dedup Gate + формат SPF»)
   - **Не замыкать loop** — агент генерирует, человек оценивает и решает, не пытаясь автоматизировать суждение

## Типичная ошибка

Попытка «сэкономить человека» на non-verifiable задаче. Агент без ground truth попадает в самосогласованный текст: внутренняя непротиворечивость растёт, но полезность для пользователя падает (см. DP.FM.005 Model-Reality Drift). Симптом — результаты всё более уверенные, но менее применимые.

## Следствия для проектирования

1. **Для Scout (R23):** задача «найти новое» — non-verifiable (нет единой метрики «хороший finding»). Решение — Экстрактор как human-in-the-loop + trajectory правила как эмпирический прокси верификации.
2. **Для Verifier (VR.R.001):** задачи сверки артефакта с эталоном — verifiable. Loop допустим (autonomous pass/fail).
3. **Для Навигатора, Диагноста, Портного:** non-verifiable (рекомендация зависит от контекста пользователя). Human gate на каждой рекомендации.
4. **Для Scheduler cron-задач:** должна быть verifiable проверка (exit code, schema valid, row count) — иначе автозапуск накапливает тихие ошибки.

## Связь

- **AS.D.006** (Execution Loop ≠ Improvement Loop): Verifiable/Non-Verifiable = **условие работающего** improvement loop
- **AS.SOTA.007** (Automated Research Agents): кейс Anthropic W2S работал именно потому, что задача была verifiable
- **DP.FM.005** (Model-Reality Drift): failure mode на non-verifiable задачах без human gate

## Источник

Синтез: OpenAI Self-Evolving Cookbook (verifier-based fine-tuning) + o-mega.ai «Top 10 Agent Frameworks 2026» (устойчивость improvement loop по доменам) + Anthropic Alignment «Automated W2S Researcher» (April 2026) — все три независимо выделяют verifiability как ключевую переменную при проектировании self-improvement.
