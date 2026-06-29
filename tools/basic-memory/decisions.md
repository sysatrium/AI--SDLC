---
title: Architecture Decision Records
type: decision
project: project-alpha
updated: 2026-06-15
tags: [decisions, ADR, architecture]
---

# Architecture Decision Records (ADR)

> Каждое значимое решение фиксируется здесь.
> Агент должен проверять этот файл перед предложением альтернатив уже решённым вопросам.

## ADR Template

<!--
## ADR-NNN: <Название>
- [decision] <Что решили> | status: proposed | accepted | deprecated | superseded #тег
- [context] <Почему стоял вопрос>
- [rationale] <Почему выбрали именно это>
- [consequence] <Что изменится в результате>
- [tradeoff] <Что теряем>
- [date] YYYY-MM-DD
-->

## Accepted Decisions

<!-- Пример:
## ADR-001: Navigation Library
- [decision] expo-router (file-based routing) | status: accepted #navigation
- [context] Нужна навигация для React Native + Expo проекта
- [rationale] Нативная интеграция с Expo, file-based == меньше boilerplate
- [consequence] Структура папок определяется маршрутами
- [tradeoff] Меньше гибкости чем React Navigation при нестандартных сценариях
- [date] 2026-06-14
-->

## Deprecated / Superseded

<!-- Решения которые были отменены или заменены -->

## Relations

- relates_to [[facts]]
- relates_to [[open-questions]]
- constrained_by [[constraints]]

---

> **Инструкция для агента**: При принятии нового архитектурного решения
> в ходе сессии — немедленно создавать новый ADR-NNN блок.
> Нумерация сквозная. Статус менять при изменении решения.
