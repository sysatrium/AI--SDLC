---
title: Active Constraints
type: note
project: lumara
updated: 2026-06-15
tags:
- constraints
- blockers
- rules
permalink: lumara/constraints
---

# Active Constraints

> Временные ограничения — вещи которые НЕЛЬЗЯ делать сейчас, но можно позже.
> Агент обязан проверять этот файл перед предложением любых изменений.

## Active

<!--
Формат строки:
- [constraint] <описание> | until: <дата или событие> | reason: <почему> #тег
-->

<!-- Пример:
- [constraint] No refactor of auth module | until: sprint-12 | reason: feature freeze #auth
- [constraint] iOS 16 minimum — no iOS 17+ only APIs | until: v2.0 | reason: target audience #ios
- [constraint] No new external npm dependencies without team approval | until: always | reason: security policy #deps
-->

## Resolved

<!-- Перемещай сюда когда ограничение снято -->
<!-- - [resolved 2026-06-10] ~~No Redux~~ → replaced by Zustand decision (ADR-002) -->

---

> **Инструкция для агента**: Перед предложением рефакторинга, новых зависимостей
> или изменения архитектуры — проверить этот файл.
> При снятии ограничения — перемещать в секцию Resolved с датой.