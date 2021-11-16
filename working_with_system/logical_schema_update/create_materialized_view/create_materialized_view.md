﻿---
layout: default
title: Создание материализованного представления
nav_order: 8
parent: Управление схемой данных
grand_parent: Работа с системой
has_children: false
---

# Создание материализованного представления {#create_materialized_view}

Чтобы создать [материализованное представление](../../../overview/main_concepts/materialized_view/materialized_view.md) 
в [логической базе данных](../../../overview/main_concepts/logical_db/logical_db.md), 
выполните запрос [CREATE MATERIALIZED VIEW](../../../reference/sql_plus_requests/CREATE_MATERIALIZED_VIEW/CREATE_MATERIALIZED_VIEW.md).
Если материализованное представление нужно создать только на логическом уровне, без 
пересоздания связанных [физических таблиц](../../../overview/main_concepts/physical_table/physical_table.md) 
в хранилище, добавьте в запрос ключевое слово 
[LOGICAL_ONLY](../../../reference/sql_plus_requests/CREATE_MATERIALIZED_VIEW/CREATE_MATERIALIZED_VIEW.md#logical_only).

В текущей версии возможно создание материализованных представлений в ADG на основе данных ADB.
{: .note-wrapper}

Наличие материализованного представления можно проверить, как описано в разделе 
[Проверка наличия материализованного представления](../entity_presence_check/entity_presence_check.md#mat_view_check).
Наличие физических таблиц, связанных с материализованным представлением, можно проверить, как описано в разделе 
[Проверка месторасположения логической сущности](../../../working_with_system/other_features/datasource_check/datasource_check.md).

## Примеры {#examples}

### Создание материализованного представления {#non-logical_example}

```sql
-- выбор базы данных sales по умолчанию
USE sales;

-- создание материализованного представления sales_and_stores
CREATE MATERIALIZED VIEW sales.sales_and_stores (
  id INT NOT NULL,
  transaction_date TIMESTAMP NOT NULL,
  product_code VARCHAR(256) NOT NULL,
  product_units INT NOT NULL,
  description VARCHAR(256),
  store_id INT NOT NULL,
  store_category VARCHAR(256) NOT NULL,
  region VARCHAR(256) NOT NULL,
  PRIMARY KEY (id, region)
)
DISTRIBUTED BY (id)
DATASOURCE_TYPE (adg)
AS SELECT
 s.id, s.transaction_date, s.product_code, s.product_units, s.description,
 st.id AS store_id, st.category as store_category, st.region
 FROM sales.sales AS s
 JOIN sales.stores AS st
 ON s.store_id = st.id
DATASOURCE_TYPE = 'adb';
```

### Создание материализованного представления только на логическом уровне {#logical_example}

```sql
CREATE MATERIALIZED VIEW sales.stores_by_sold_products_matview (
  store_id INT NOT NULL,
  product_amount INT NOT NULL,
  PRIMARY KEY (store_id)
)
DISTRIBUTED BY (store_id)
DATASOURCE_TYPE (adg)
AS SELECT store_id, SUM(product_units) AS product_amount
  FROM sales.sales
  GROUP BY store_id
DATASOURCE_TYPE = 'adb'
LOGICAL_ONLY
```
