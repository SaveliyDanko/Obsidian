---
tags:
  - review
sr-due: 2026-03-20
sr-interval: 75
sr-ease: 250
---

---
**Enterprise Integration Patterns (EIP)** — это набор стандартных архитектурных шаблонов, которые описывают, как правильно проектировать обмен данными между системами.

###### **Основные группы EIP:**
- Message Routing — маршрутизация сообщений (Content-Based Router, Recipient List)
- Message Transformation — преобразование (Message Translator, Enricher)
- Message Construction — формирование сообщений
- Messaging Channels — каналы обмена (Queues, Topics)
- System Management — наблюдение, повторная попытка, ошибки

###### **Примеры популярных паттернов:**
- Filter — пропустить только подходящие сообщения
- Splitter — разделить одно сообщение на несколько
- Aggregator — собрать несколько сообщений в одно
- Content-Based Router — направлять сообщения в зависимости от их содержимого
- Message Translator — преобразовать формат данных
- Dead Letter Channel — обработка ошибок