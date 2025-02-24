﻿---
layout: default
title: GET_DELTA_BY_DATETIME
nav_order: 24
parent: Запросы SQL+
grand_parent: Справочная информация
has_children: false
has_toc: false
---

# GET_DELTA_BY_DATETIME

Запрос позволяет получить информацию о последней закрытой [дельте](../../../overview/main_concepts/delta/delta.md) 
на указанные дату и время. Перед выполнением запроса необходимо определить 
[логическую базу данных](../../../overview/main_concepts/logical_db/logical_db.md), 
[используемую по умолчанию](../../../working_with_system/other_features/default_db_set-up/default_db_set-up.md), 
если она еще не определена.

В ответе возвращается:
*   объект ResultSet c одной записью, содержащей информацию о дельте, при успешном выполнении запроса;
*   исключение при неуспешном выполнении запроса.

Возвращаемая информация включает следующие параметры:
*   `delta_num` — номер дельты,
*   `delta_date` — дата и время закрытия дельты,
*   `[cn_from, cn_to]` — диапазон номеров выполненных [операций записи](../../../overview/main_concepts/write_operation/write_operation.md).

## Синтаксис {#syntax}

```sql
GET_DELTA_BY_DATETIME(date_time_expression)
```

Параметры:
*   `date_time_expression` — момент даты-времени вида `'YYYY-MM-DD hh:mm:ss'`. Возможные форматы см. в разделе
    [Форматы даты и времени](../../timestamp_formats/timestamp_formats.md). 

## Пример {#examples}

```sql
GET_DELTA_BY_DATETIME('2021-03-25 07:30:32')
```