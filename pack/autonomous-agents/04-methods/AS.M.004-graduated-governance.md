---
id: AS.M.004
name: "Graduated Governance Implementation"
type: method
status: active
created: 2026-03-23
source: "WEF/Singapore IMDA 2026, Scout 22 мар 2026"
related: [AS.M.001, AS.SOTA.003, AS.D.001]
s2r_families: [F8]
---

# AS.M.004: Graduated Governance — метод поэтапного наращивания автономии

## 1. Назначение

Систематический подход к масштабированию автономии агентов через поэтапное governance. Решает проблему: 40% failures из-за risk management, 35% из-за cybersecurity при развёртывании без структурированного governance.

## 2. Метод

### Фаза 1: Start Bounded (L1-L2)

1. Определить роль агента (узкий scope)
2. Установить операционные лимиты (whitelist действий)
3. Внедрить approval gates (human-in-loop для всех действий)
4. Развернуть с базовым logging

### Фаза 2: Monitor & Earn Trust (L2 → L3)

1. **Собрать метрики:**
   - Success rate (% корректных действий)
   - Escalation rate (% требующих human intervention)
   - Time-to-value (speed vs quality tradeoff)

2. **Определить критерии доверия:**
   - Success rate >95% за 30 дней → промоушн на L3
   - Escalation rate <10% → снижение approval gates
   - Zero critical failures → расширение scope

3. **Audit review:**
   - Еженедельный разбор audit logs
   - Идентификация edge cases, failure modes
   - Обновление guardrails

### Фаза 3: Scale with Guardrails (L3 → L4)

1. **Автоматические guardrails:**
   - Budget limits (max spend per action/day)
   - Scope limits (allowed domains, APIs, actions)
   - Output validation (automated checks before delivery)

2. **Continuous monitoring:**
   - Real-time anomaly detection (drift от expected behavior)
   - Automated rollback при threshold breach
   - Human escalation для novel situations

3. **Regulatory compliance:**
   - Audit trails для каждого решения
   - Explainability requirements (legible reasoning)
   - Insurance/liability frameworks (L4)

## 3. Критерии перехода между уровнями

| Переход | Условие | Метрика |
|---------|---------|---------|
| L1 → L2 | Стабильная работа | Success rate >90%, 14 дней без critical failures |
| L2 → L3 | Заработанное доверие | Success rate >95%, escalation <10%, 30 дней |
| L3 → L4 | Полная автономия | Success rate >99%, zero critical failures за 90 дней, regulatory audit passed |

## 4. Failure modes

- **FM.001:** Premature promotion — агент получает L3 без достаточной истории → catastrophic failure
- **FM.002:** No rollback — агент на L3+ без способности откатить → cascading damage
- **FM.003:** Metric gaming — метрики хорошие, но agent избегает сложных задач

## 5. Применение к IWE

| Агент | Текущий уровень | Целевой | Что нужно для перехода |
|-------|----------------|---------|----------------------|
| scheduler.sh | L1 | L1 (автоматизация, не автономия) | — |
| Scout | L2 | L3 | Trajectory cache + 30 дней + human review captures |
| Strategist | L1-L2 | L2 | Audit dayplan quality, approval gate |

## Источники

- WEF «AI Agents in Action» (январь 2026)
- Singapore IMDA Model AI Governance Framework for Agentic AI (2026)
