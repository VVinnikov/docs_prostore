---
layout: default
title: Поддержка SQL
nav_order: 2
parent: Справочная информация
has_children: false
has_toc: false
---

# Поддержка SQL {#sql_support}
{: .no_toc }

<details markdown="block">
  <summary>
    Содержание раздела
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

В [SELECT](../sql_plus_requests/SELECT/SELECT.md)-запросах к данным можно использовать функции и операторы, описанные 
в таблице ниже.

[СУБД](../../introduction/supported_DBMS/supported_DBMS.md) [хранилища](../../overview/main_concepts/data_storage/data_storage.md) 
имеют ограничения на использование некоторых функций в запросах, вызванные особенностями этих СУБД. 
Наиболее полный синтаксис запросов доступен в ADB и ADP.

## Функции и операторы соединения {#Joinfunctions}

### UNION {#UnionSQL}

| CURRENT_DATE: ADB, ADQM, ADG, ADP
|:---
| `SELECT a.*
from (
         SELECT b.id
         from (SELECT id from table2) b
         UNION ALL
         SELECT id
         from table1
     ) as a datasource_type = {'ADB' | 'ADP' | 'ADQM' | 'ADG'}`;


## Функции и операторы даты и времени {#Datetimefunctions}

### CURRENT_DATE {#CurrentdateSQL}

| CURRENT_DATE: ADB, ADP
|:---
| `SELECT CAST(CURRENT_DATE AS DATE) FROM table1 datasource_type = {'ADB' | 'ADP'};` |
| `SELECT CURRENT_DATE FROM table1 datasource_type = {'ADB' | 'ADP'};` |

### CURRENT_TIME {#CurrenttimeSQL}

| CURRENT_TIME: ADB, ADP
|:---
| `SELECT CAST(CURRENT_TIME AS TIME) FROM table1 datasource_type = {'ADB' | 'ADP'};` |

| CURRENT_TIME: Не поддерживается
|:---
| `SELECT CURRENT_TIME FROM table1;`|

### CURRENT_TIMESTAMP {#CurrenttimestampSQL}

| CURRENT_TIMESTAMP: ADB, ADP
|:---
| `SELECT CAST(CURRENT_TIMESTAMP AS TIMESTAMP) FROM table1 datasource_type = {'ADB' | 'ADP'};` |
| `SELECT CURRENT_TIMESTAMP FROM table1 datasource_type = {'ADB' | 'ADP'};` |

### EXTRACT {#ExtractSQL}

| EXTRACT(FROM DATE): ADB, ADQM, ADP
|:---
| `SELECT CAST(EXTRACT(EPOCH FROM DATE '2001-02-16') AS INT) FROM table1 datasource_type = {'ADB' | 'ADP'};` |
| `SELECT CAST(EXTRACT(DOY FROM DATE '2001-02-16') AS INT) FROM table1 datasource_type = {'ADB' | 'ADP'};` |
| `SELECT CAST(EXTRACT(DOW FROM DATE '2001-02-16') AS INT) FROM table1 datasource_type = {'ADB' | 'ADP'};` |
| `SELECT CAST(EXTRACT(WEEK FROM DATE '2001-02-16') AS INT) FROM table1 datasource_type = {'ADB' | 'ADP'};` |
| `SELECT CAST(EXTRACT(CENTURY FROM DATE '2001-02-16') AS INT) FROM table1 datasource_type = {'ADB' | 'ADP'};` |
| `SELECT CAST(EXTRACT(QUARTER FROM DATE '2001-02-16') AS INT) FROM table1 datasource_type = {'ADB' | 'ADP'};` |
| `SELECT EXTRACT(QUARTER FROM DATE '2001-02-16') FROM table1 datasource_type = 'ADQM';` |
| `SELECT CAST(EXTRACT(YEAR FROM DATE '2001-02-16') AS INT) FROM table1 datasource_type = {'ADB' | 'ADP'};` |
| `SELECT EXTRACT(YEAR FROM DATE '2001-02-16') FROM table1 datasource_type = 'ADQM';` |
| `SELECT CAST(EXTRACT(MONTH FROM DATE '2001-02-16') AS INT) FROM table1 datasource_type = {'ADB' | 'ADP'};`|
| `SELECT EXTRACT(MONTH FROM DATE '2001-02-16') FROM table1 datasource_type = 'ADQM';`|
| `SELECT CAST(EXTRACT(DAY FROM DATE '2001-02-16') AS INT) FROM table1 datasource_type = {'ADB' | 'ADP'};`|
| `SELECT EXTRACT(DAY FROM DATE '2001-02-16') FROM table1 datasource_type = 'ADQM';`|

| EXTRACT(FROM DATE): ADB, ADP
|:---
| `SELECT CAST(EXTRACT(DECADE FROM DATE '2001-02-16') AS INT) FROM table1 datasource_type = {'ADB' | 'ADP'};`|
| `SELECT CAST(EXTRACT(ISOYEAR FROM DATE '2001-02-16') AS INT) FROM table1 datasource_type = {'ADB' | 'ADP'};`|
| `SELECT CAST(EXTRACT(ISODOW FROM DATE '2001-02-16') AS INT) FROM table1 datasource_type = {'ADB' | 'ADP'};`|

| EXTRACT(FROM TIME): ADB, ADP
|:---
| `SELECT CAST(EXTRACT(HOUR FROM TIME '20:38:40') AS INT) FROM table1 datasource_type = {'ADB' | 'ADP'};` |
| `SELECT CAST(EXTRACT(MINUTE FROM TIME '20:38:40') AS INT) FROM table1 datasource_type = {'ADB' | 'ADP'};` |
| `SELECT CAST(EXTRACT(SECOND FROM TIME '20:38:40') AS INT) FROM table1 datasource_type = {'ADB' | 'ADP'};` |
| `SELECT CAST(EXTRACT(MILLISECOND FROM TIME '20:38:40') AS INT) FROM table1 datasource_type = {'ADB' | 'ADP'};` |
| `SELECT CAST(EXTRACT(MICROSECOND FROM TIME '20:38:40') AS INT) FROM table1 datasource_type = {'ADB' | 'ADP'};` |

| EXTRACT(FROM TIMESTAMP): ADB, ADQM, ADP
|:---
| `SELECT CAST(EXTRACT(DOW FROM TIMESTAMP '2001-02-16 00:00:00') AS INT) FROM table1 datasource_type = {'ADB' | 'ADP'};` |
| `SELECT CAST(EXTRACT(WEEK FROM TIMESTAMP '2001-02-16 00:00:00') AS INT) FROM table1 datasource_type = {'ADB' | 'ADP'};` |
| `SELECT CAST(EXTRACT(CENTURY FROM TIMESTAMP '2001-02-16 00:00:00') AS INT) FROM table1 datasource_type = {'ADB' | 'ADP'};` |
| `SELECT CAST(EXTRACT(QUARTER FROM TIMESTAMP '2001-02-16 00:00:00') AS INT) FROM table1 datasource_type = {'ADB' | 'ADP'};` |
| `SELECT EXTRACT(QUARTER FROM TIMESTAMP '2001-02-16 20:38:40') FROM table1 datasource_type = 'ADQM';` |
| `SELECT CAST(EXTRACT(YEAR FROM TIMESTAMP '2001-02-16 20:38:40') AS INT) FROM table1 datasource_type = {'ADB' | 'ADP'};` |
| `SELECT EXTRACT(YEAR FROM TIMESTAMP '2001-02-16 20:38:40') FROM table1 datasource_type = 'ADQM';` |
| `SELECT CAST(EXTRACT(MONTH FROM TIMESTAMP '2001-02-16 20:38:40') AS INT) FROM table1 datasource_type = {'ADB' | 'ADP'};` |
| `SELECT EXTRACT(MONTH FROM TIMESTAMP '2001-02-16 20:38:40') FROM table1 datasource_type = 'ADQM';` |
| `SELECT CAST(EXTRACT(DAY FROM TIMESTAMP '2001-02-16 20:38:40') AS INT) FROM table1 datasource_type = {'ADB' | 'ADP'};` |
| `SELECT EXTRACT(DAY FROM TIMESTAMP '2001-02-16 20:38:40') FROM table1 datasource_type = 'ADQM';` |
| `SELECT CAST(EXTRACT(HOUR FROM TIMESTAMP '2001-02-16 20:38:40') AS INT) FROM table1 datasource_type = {'ADB' | 'ADP'};` |
| `SELECT EXTRACT(HOUR FROM TIMESTAMP '2001-02-16 20:38:40') FROM table1 datasource_type = 'ADQM';` |
| `SELECT CAST(EXTRACT(MINUTE FROM TIMESTAMP '2001-02-16 20:38:40') AS INT) FROM table1 datasource_type = {'ADB' | 'ADP'};` |
| `SELECT EXTRACT(MINUTE FROM TIMESTAMP '2001-02-16 20:38:40') FROM table1 datasource_type = 'ADQM';` |
| `SELECT CAST(EXTRACT(SECOND FROM TIMESTAMP '2001-02-16 20:38:40') AS INT) FROM table1 datasource_type = {'ADB' | 'ADP'};` |
| `SELECT EXTRACT(SECOND FROM TIMESTAMP '2001-02-16 20:38:40') FROM table1 datasource_type = 'ADQM';` |
| `SELECT CAST(EXTRACT(MILLISECOND FROM TIMESTAMP '2001-02-16 20:38:40') AS INT) FROM table1 datasource_type = {'ADB' | 'ADP'};` |
| `SELECT CAST(EXTRACT(MICROSECOND FROM TIMESTAMP '2001-02-16 20:38:40') AS INT) FROM table1 datasource_type = {'ADB' | 'ADP'};` |

### LOCALTIME {#LocaltimeSQL}

| LOCALTIME, LOCALTIME(precision): ADB, ADP
|:---
| `SELECT LOCALTIME FROM table1 datasource_type = {'ADB' | 'ADP'};` |
| `SELECT CAST(LOCALTIME AS TIME) FROM table1 datasource_type = {'ADB' | 'ADP'};` |
| `SELECT LOCALTIME(3) FROM table1 datasource_type = {'ADB' | 'ADP'};` |
| `SELECT CAST(LOCALTIME(3) AS TIME) FROM table1 datasource_type = {'ADB' | 'ADP'};` |

### LOCALTIMESTAMP {#LocaltimestampSQL}

| LOCALTIMESTAMP, LOCALTIMESTAMP(precision): ADB, ADP
|:---
| `SELECT LOCALTIMESTAMP FROM table1 datasource_type = {'ADB' | 'ADP'};` |
| `SELECT CAST(LOCALTIMESTAMP AS TIMESTAMP) FROM table1 datasource_type = {'ADB' | 'ADP'};` |
| `SELECT LOCALTIMESTAMP(3) FROM table1 datasource_type = {'ADB' | 'ADP'};` |
| `SELECT CAST(LOCALTIMESTAMP(3) AS TIMESTAMP) FROM table1 datasource_type = {'ADB' | 'ADP'};` |

### MONTH, QUARTER, WEEK, YEAR {#MonthSQL}

| MONTH, QUARTER, WEEK, YEAR: ADB, ADP
|:---
| `SELECT CAST(MONTH(DATE '2001-02-16') AS INT) FROM table1 datasource_type = {'ADB' | 'ADP'};` |
| `SELECT CAST(MONTH(TIMESTAMP '2001-02-16 20:38:40') AS INT) FROM table1 datasource_type = {'ADB' | 'ADP'};` |
| `SELECT CAST(QUARTER(DATE '2001-02-16') AS INT) FROM table1 datasource_type = {'ADB' | 'ADP'};` |
| `SELECT CAST(QUARTER(DATE '2001-02-16') AS INT) FROM table1 datasource_type = 'ADP';` |
| `SELECT CAST(QUARTER(TIMESTAMP '2001-02-16 20:38:40') AS INT) FROM table1 datasource_type = {'ADB' | 'ADP'};` |
| `SELECT CAST(QUARTER(TIMESTAMP '2001-02-16 20:38:40') AS INT) FROM table1 datasource_type = 'ADP';` |
| `SELECT CAST(WEEK(DATE '2001-02-16') AS INT) FROM table1 datasource_type = {'ADB' | 'ADP'};` |
| `SELECT CAST(WEEK(TIMESTAMP '2001-02-16 20:38:40') AS INT) FROM table1 datasource_type = {'ADB' | 'ADP'};` |
| `SELECT CAST(YEAR(DATE '2001-02-16') AS INT) FROM table1 datasource_type = {'ADB' | 'ADP'};` |
| `SELECT CAST(YEAR(TIMESTAMP '2001-02-16 20:38:40') AS INT) FROM table1 datasource_type = {'ADB' | 'ADP'};` |

## Системные функции и операторы {#Systemfunctions}

| CURRENT_USER, SESSION_USER, CURRENT_ROLE, CURRENT_SCHEMA: ADB, ADP
|:---
| `SELECT CURRENT_USER FROM table1 datasource_type = {'ADB' | 'ADP'};` |
| `SELECT SESSION_USER FROM table1 datasource_type = {'ADB' | 'ADP'};` |
| `SELECT CURRENT_ROLE FROM table1 datasource_type = {'ADB' | 'ADP'};` |
| `SELECT CURRENT_SCHEMA FROM table1 datasource_type = {'ADB' | 'ADP'};` |

## Строковые функции и операторы {#Stringfunctions}

### POSITION {#PositionSQL}

| POSITION: ADB, ADP
|:---
| `SELECT POSITION('c' IN 'abcdef') FROM table1 datasource_type = 'ADB' | 'ADP'};` |

### UPPER {#UpperSQL}

| UPPER: ADB, ADQM, ADG, ADP
|:---
| `SELECT UPPER('abcdef') FROM table1 datasource_type = {'ADB' | 'ADP' | 'ADQM' | 'ADG'};` |

### LOWER {#LowerSQL}

| LOWER: ADB, ADP
|:---
| `SELECT LOWER('ABCDEG') FROM table1 datasource_type = {'ADB' | 'ADP' | 'ADQM' | 'ADG'};` |

### SUBSTRING {#SubstringSQL}

| SUBSTRING: ADB, ADQM, ADP
|:---
| `SELECT SUBSTRING('ABCDEG', 3, 2) FROM table1 datasource_type = {'ADB' | 'ADP' | 'ADQM'};` |

### COALESCE {#CoalesceSQL}

| COALESCE: ADB, ADG, ADP
|:---
| `SELECT COALESCE(boolean_col,true) FROM table1 datasource_type = {'ADB' | 'ADP' | 'ADG'};` |

| COALESCE: ADB, ADQM, ADG, ADP
|:---
| `SELECT COALESCE(int_col,1) FROM table1 datasource_type = {'ADB' | 'ADP' | 'ADQM' | 'ADG'};` |

| COALESCE: ADB, ADQM, ADP
|:---
| `SELECT COALESCE(bigint_col,1) FROM table1 datasource_type = {'ADB' | 'ADP' | 'ADQM'};` |

| COALESCE: ADB, ADQM, ADG, ADP
|:---
| `SELECT COALESCE(int32_col,1) FROM table1 datasource_type = {'ADB' | 'ADP' | 'ADQM' | 'ADG'};` |

| COALESCE: ADB, ADP
|:---
| `SELECT COALESCE(float_col,1.0) FROM table1 datasource_type = {'ADB' | 'ADP'};` |

| COALESCE: ADB, ADP
|:---
| `SELECT COALESCE(double_col,1.0) FROM table1 datasource_type = {'ADB' | 'ADP'};` |

| COALESCE: ADB, ADQM, ADG, ADP
|:---
| `SELECT COALESCE(varchar_col,'1.0') FROM table1 datasource_type = {'ADB' | 'ADP' | 'ADG'};` |
| `SELECT COALESCE(CAST(varchar_col AS VARCHAR),'1.0') FROM table1 datasource_type = 'ADQM';` |


| COALESCE: ADB, ADQM*, ADP
|:---
| `SELECT COALESCE(date_col,'2001-01-01') FROM table1 datasource_type = {'ADB' | 'ADP' | 'ADQM'};` |
| * возвращает дату как число

| COALESCE: ADB, ADQM, ADP
|:---
| `SELECT COALESCE(date_col,CAST('2001-01-01' AS DATE)) FROM table1 datasource_type = {'ADB' | 'ADP' | 'ADQM'};` |

| COALESCE: ADB, ADQM, ADP
|:---
| `SELECT COALESCE(time_col,'11:12:13') FROM table1 datasource_type = {'ADB' | 'ADP' | 'ADQM'};` |

| COALESCE: ADB, ADQM*, ADG, ADP
|:---
| `SELECT COALESCE(timestamp_col,'2001-01-01 11:12:13') FROM table1 datasource_type = {'ADB' | 'ADP' | 'ADQM' | 'ADG'};` |
| * возвращает дату как число

| COALESCE: ADB, ADQM, ADP
|:---
| `SELECT COALESCE(uuid_col,'1') FROM table1 datasource_type = {'ADB' | 'ADP' | 'ADQM'};` |

| COALESCE: ADB, ADG, ADP
|:---
| `SELECT COALESCE(char_col,'1') FROM table1 datasource_type = {'ADB' | 'ADP' | 'ADG'};` |

| COALESCE: ADB, ADQM, ADP
|:---
| `SELECT COALESCE(link_col,'http://www.google.com') FROM table1 datasource_type = {'ADB' | 'ADP' | 'ADQM'};` |

### TRIM {#TrimSQL}

| TRIM: ADB, ADQM, ADG, ADP
|:---
| `SELECT TRIM('   ABC XYZ   ') FROM table1 datasource_type = {'ADB' | 'ADP' | 'ADQM' | 'ADG'};` |

### REPLACE {#ReplaceSQL}

| REPLACE: ADB, ADQM, ADG, ADP
|:---
| `SELECT REPLACE('  abc xyz  ','ab', 'x') FROM table1 datasource_type = {'ADB' | 'ADP' | 'ADQM' | 'ADG'};` |

### CONCATENATION {#ConcatenationSQL}

| CONCATENATION: ADB, ADQM, ADG, ADP
|:---
| `SELECT 'abc' || 'xyz' FROM table1 datasource_type = {'ADB' | 'ADP' | 'ADQM' | 'ADG'};` |

### INITCAP {#InitcapSQL}

| INITCAP: ADB, ADP
|:---
| `SELECT INITCAP('abc def ghi xyz') FROM table1 datasource_type = {'ADB' | 'ADP'};` |

## Математические функции и операторы {#Mathfunctions}

### ABS {#AbsSQL}

| ABS: ADB, ADQM, ADG, ADP |
|: ---
| `SELECT ABS(-2.0) FROM table1 datasource_type = {'ADB' | 'ADP' | 'ADG'};` |
| `SELECT ABS(-2) FROM table1 datasource_type = 'ADQM';` |

### ROUND {#RoundSQL}

| ROUND: ADB, ADQM, ADG, ADP |
|:---
| `SELECT ROUND(-2.5) FROM table1 datasource_type = {'ADB' | 'ADP' | 'ADQM' | 'ADG'};` |

### FLOOR {#FloorSQL}

| FLOOR: ADB, ADQM, ADP |
|:---
| `SELECT FLOOR(-2.5) FROM table1 datasource_type = {'ADB' | 'ADP' | 'ADQM'};` |

### CEIL {#CeilSQL}

| CEIL: ADB, ADQM, ADP |
|:---
| `SELECT CEIL(-2.5) FROM table1 datasource_type = {'ADB' | 'ADP' | 'ADQM'};` |

### CEILING {#CeilingSQL}

| CEILING: ADB, ADQM, ADP |
|:---
| `SELECT CEILING(-2.5) FROM table1 datasource_type = {'ADB' | 'ADP' | 'ADQM'};` |

### BIT_AND {#BitandSQL}

| BIT_AND: ADB, ADP |
|:---
| `SELECT BIT_AND(numeric_col) FROM table1 datasource_type = {'ADB' | 'ADP'};` |

### BIT_OR {#BitorSQL}

| BIT_OR: ADB, ADP |
|:---
| `SELECT BIT_OR(numeric_col) FROM table1 datasource_type = {'ADB' | 'ADP'};` |

### DEGREES {#DegreesSQL}

| DEGREES: ADB, ADP |
|:---
| `SELECT DEGREES(3.1415269) FROM table1 datasource_type = {'ADB' | 'ADP'};` |

### RADIANS {#RadiansSQL}

| RADIANS: ADB, ADP |
|:---
| `SELECT RADIANS(180.0) FROM table1 datasource_type = {'ADB' | 'ADP'};` |

### SIGN {#SignSQL}

| RADIANS: ADB, ADP |
|:---
| `SELECT SIGN(-2.0) FROM table1 datasource_type = {'ADB' | 'ADP'};` |
| `SELECT SIGN(CAST(-2 AS FLOAT)) FROM table1 datasource_type = {'ADB' | 'ADP'};` |

### SIN, COS, TAN, COT {#SincostancotSQL}

| SIN, COS, TAN, COT: ADB, ADQM, ADP |
|:---
| `SELECT SIN(-2.0) FROM table1 datasource_type = {'ADB' | 'ADP' | 'ADQM'};` |
| `SELECT COS(-2.0) FROM table1 datasource_type = {'ADB' | 'ADP' | 'ADQM'};` |
| `SELECT TAN(-2.0) FROM table1 datasource_type = {'ADB' | 'ADP' | 'ADQM'};` |
| `SELECT COT(-2.0) FROM table1 datasource_type = {'ADB' | 'ADP' | 'ADQM'};` |

### ASIN, ACOS, ATAN, ATAN2 {#Asinacosatanatan2SQL}

| SIN, COS, TAN, COT: ADB, ADQM, ADP |
|:---
| `SELECT ASIN(0.5) FROM table1 datasource_type = {'ADB' | 'ADP' | 'ADQM'};` |
| `SELECT ACOS(0.5) FROM table1 datasource_type = {'ADB' | 'ADP' | 'ADQM'};` |
| `SELECT ATAN(0.5) FROM table1 datasource_type = {'ADB' | 'ADP' | 'ADQM'};` |
| `SELECT ATAN2(3.0,2.0) FROM table1 datasource_type = {'ADB' | 'ADP' | 'ADQM'};` |

### POWER, EXP*, LOG* {#PowerexplogSQL}

| POWER, EXP, LN: ADB, ADQM*, ADP |
|:---
| `SELECT POWER(0.5,2) FROM table1 datasource_type = {'ADB' | 'ADP' | 'ADQM'};` |
| `SELECT EXP(1.0) FROM table1 datasource_type = {'ADB' | 'ADP' | 'ADQM'};` |
| `SELECT LN(2.18281828) FROM table1 datasource_type = {'ADB' | 'ADP' | 'ADQM'};` |
| * Возвращает недостаточно точные значения для EXP и LN |

### SQRT, CBRT {#SqrtcbrtSQL}

| SQRT: ADB, ADQM, ADP |
|:---
| `SELECT SQRT(4) FROM table1 datasource_type = {'ADB' | 'ADP' | 'ADQM'};` |

| CBRT: ADB, ADP |
|:---
| `SELECT CBRT(-8) FROM table1 datasource_type = {'ADB' | 'ADP'};` |

### MOD {#ModSQL}

| MOD: ADB, ADP |
|:---
| `SELECT MOD(8,3) FROM table1 datasource_type = {'ADB' | 'ADP'};` |

### MAX, MIN {#MaxminSQL}

| MAX: ADB, ADQM, ADG, ADP |
|:---
| `SELECT MAX(numeric_col) FROM table1 datasource_type = {'ADB' | 'ADP' | 'ADQM' | 'ADG'};` |

| MIN: ADB, ADQM, ADG, ADP |
|:---
| `SELECT MIN(numeric_col) FROM table1 datasource_type = {'ADB' | 'ADP' | 'ADQM' | 'ADG'};` |

### SUM, COUNT {#SumcountSQL}

| SUM: ADB, ADQM, ADG, ADP |
|:---
| `SELECT SUM(numeric_col) FROM table1 datasource_type = {'ADB' | 'ADP' | 'ADQM' | 'ADG'};` |

| COUNT: ADB, ADQM, ADG, ADP |
|:---
| `SELECT COUNT(numeric_col) FROM table1 datasource_type = {'ADB' | 'ADP' | 'ADQM' | 'ADG'};` |

### AVG {#AvgSQL}

| AVG: ADB*, ADQM*, ADG**, ADP* |
|:---
| `SELECT AVG(CAST(numeric_col AS DOUBLE)) FROM table1 datasource_type = {'ADB' | 'ADP' | 'ADG'};` |
| `SELECT AVG(CAST(numeric_col AS FLOAT)) FROM table1 datasource_type = 'ADQM';` |
| `SELECT AVG(numeric_col) FROM table1 datasource_type = 'ADG';` |
| * Нет неявного преобразования из целочисленного типа |
| ** Результат возвращается по каждому шарду |

### COVAR {#CovarSQL}

| COVAR_POP: ADB, ADQM, ADP |
|:---
| `SELECT COVAR_POP(CAST(numeric_col1 AS DOUBLE), numeric_col2) FROM table1 datasource_type = {'ADB' | 'ADP'};` |
| `SELECT COVAR_POP(CAST(numeric_col1 AS FLOAT), numeric_col2) FROM table1 datasource_type = 'ADQM';` |
| `SELECT CAST(COVAR_POP(numeric_col1, numeric_col2) AS FLOAT) FROM table1 datasource_type = 'ADQM';` |

| COVAR_SAMP: ADB, ADQM, ADP |
|:---
| `SELECT COVAR_SAMP(CAST(numeric_col1 AS DOUBLE), numeric_col2) FROM table1 datasource_type = {'ADB' | 'ADP'};` |
| `SELECT COVAR_SAMP(CAST(numeric_col1 AS FLOAT), numeric_col2) FROM table1 datasource_type = 'ADQM';` |
| `SELECT CAST(COVAR_SAMP(numeric_col1, numeric_col2) AS FLOAT) FROM table1 datasource_type = 'ADQM';` |

### VAR {#VarSQL}

| VAR_POP: ADB, ADQM, ADP |
|:---
| `SELECT CAST(VAR_POP(numeric_col, numeric_col) AS DOUBLE) FROM table1 datasource_type = {'ADB' | 'ADP'};` |
| `SELECT CAST(VAR_POP(numeric_col, numeric_col) AS FLOAT) FROM table1 datasource_type = 'ADQM';` |
| `SELECT VAR_POP(CAST(numeric_col AS FLOAT)) FROM table1 datasource_type = 'ADQM';` |

| VAR_SAMP: ADB, ADQM, ADP |
|:---
| `SELECT CAST(VAR_SAMP(numeric_col, numeric_col) AS DOUBLE) FROM table1 datasource_type = {'ADB' | 'ADP'};` |
| `SELECT CAST(VAR_POP(numeric_col, numeric_col) AS FLOAT) FROM table1 datasource_type = 'ADQM';` |
| `SELECT VAR_POP(CAST(numeric_col AS FLOAT)) FROM table1 datasource_type = 'ADQM';` |

### STDDEV {#StddevSQL}

| STDDEV_POP: ADB, ADQM, ADP |
|:---
| `SELECT CAST(STDDEV_POP(numeric_col, numeric_col) AS DOUBLE) FROM table1 datasource_type = {'ADB' | 'ADP'};` |
| `SELECT CAST(STDDEV_POP(numeric_col, numeric_col) AS FLOAT) FROM table1 datasource_type = 'ADQM';` |
| `SELECT STDDEV_POP(CAST(numeric_col AS FLOAT)) FROM table1 datasource_type = 'ADQM';` |

| STDDEV_SAMP: ADB, ADQM, ADP |
|:---
| `SELECT CAST(STDDEV_SAMP(numeric_col, numeric_col) AS DOUBLE) FROM table1 datasource_type = {'ADB' | 'ADP'};` |
| `SELECT CAST(STDDEV_POP(numeric_col, numeric_col) AS FLOAT) FROM table1 datasource_type = 'ADQM';` |
| `SELECT STDDEV_POP(CAST(numeric_col AS FLOAT)) FROM table1 datasource_type = 'ADQM';` |

<details markdown="block">
  <summary>

CURRENT_DATE

  </summary>
  {: .text-delta }

ADB, ADP

```sql
SELECT CAST(CURRENT_DATE AS DATE) FROM table1 datasource_type = 'ADB';
SELECT CAST(CURRENT_DATE AS DATE) FROM table1 datasource_type = 'ADP';
```
  
---

ADB, ADP

```sql
SELECT CAST(CURRENT_DATE AS DATE) FROM table1 datasource_type = 'ADB';
SELECT CAST(CURRENT_DATE AS DATE) FROM table1 datasource_type = 'ADP';
```

---

ADB, ADP

```sql
SELECT CURRENT_DATE FROM table1 datasource_type = 'ADB';
SELECT CURRENT_DATE FROM table1 datasource_type = 'ADP';
```

---

</details>

<details markdown="block">
  <summary>
CURRENT_TIME
  </summary>
  {: .text-delta }

ADB, ADP

```sql
SELECT CAST(CURRENT_TIME AS TIME) FROM table1 datasource_type = 'ADB';
SELECT CAST(CURRENT_TIME AS TIME) FROM table1 datasource_type = 'ADP';
```

---

НЕ ПОДДЕРЖИВАЕТСЯ

```sql
SELECT CURRENT_TIME FROM table1 datasource_type = '*';
```

---

ADB, ADP

```sql
SELECT CAST(CURRENT_TIMESTAMP AS TIMESTAMP) FROM table1 datasource_type = 'ADB';
SELECT CAST(CURRENT_TIMESTAMP AS TIMESTAMP) FROM table1 datasource_type = 'ADP';
```

---

ADB, ADP

```sql
SELECT CURRENT_TIMESTAMP FROM table1 datasource_type = 'ADB';
SELECT CURRENT_TIMESTAMP FROM table1 datasource_type = 'ADP';
```

---

</details>

<details markdown="block">
  <summary>
EXTRACT(FROM DATE)
  </summary>
  {: .text-delta }

ADB, ADQM, ADP

```sql
SELECT CAST(EXTRACT(EPOCH FROM DATE '2001-02-16') AS INT) FROM table1 datasource_type = 'ADB';
SELECT CAST(EXTRACT(DOY FROM DATE '2001-02-16') AS INT) FROM table1 datasource_type = 'ADB';
SELECT CAST(EXTRACT(DOW FROM DATE '2001-02-16') AS INT) FROM table1 datasource_type = 'ADB';
SELECT CAST(EXTRACT(WEEK FROM DATE '2001-02-16') AS INT) FROM table1 datasource_type = 'ADB';
SELECT CAST(EXTRACT(CENTURY FROM DATE '2001-02-16') AS INT) FROM table1 datasource_type = 'ADB';
SELECT CAST(EXTRACT(QUARTER FROM DATE '2001-02-16') AS INT) FROM table1 datasource_type = 'ADB';
SELECT EXTRACT(QUARTER FROM DATE '2001-02-16') FROM table1 datasource_type = 'ADQM';
SELECT CAST(EXTRACT(YEAR FROM DATE '2001-02-16') AS INT) FROM table1 datasource_type = 'ADB';
SELECT EXTRACT(YEAR FROM DATE '2001-02-16') FROM table1 datasource_type = 'ADQM';
SELECT CAST(EXTRACT(MONTH FROM DATE '2001-02-16') AS INT) FROM table1 datasource_type = 'ADB';
SELECT EXTRACT(MONTH FROM DATE '2001-02-16') FROM table1 datasource_type = 'ADQM';
SELECT CAST(EXTRACT(MONTH FROM DATE '2001-02-16') AS INT) FROM table1 datasource_type = 'ADP';
SELECT CAST(EXTRACT(DAY FROM DATE '2001-02-16') AS INT) FROM table1 datasource_type = 'ADB';
SELECT EXTRACT(DAY FROM DATE '2001-02-16') FROM table1 datasource_type = 'ADQM';
SELECT CAST(EXTRACT(DAY FROM DATE '2001-02-16') AS INT) FROM table1 datasource_type = 'ADP';
```

---

ADB, ADP

 ```sql
SELECT CAST(EXTRACT(DECADE FROM DATE '2001-02-16') AS INT) FROM table1 datasource_type = 'ADB';
SELECT CAST(EXTRACT(DECADE FROM DATE '2001-02-16') AS INT) FROM table1 datasource_type = 'ADP';
SELECT CAST(EXTRACT(ISOYEAR FROM DATE '2001-02-16') AS INT) FROM table1 datasource_type = 'ADB';
SELECT CAST(EXTRACT(ISOYEAR FROM DATE '2001-02-16') AS INT) FROM table1 datasource_type = 'ADP';
SELECT CAST(EXTRACT(ISODOW FROM DATE '2001-02-16') AS INT) FROM table1 datasource_type = 'ADB';
SELECT CAST(EXTRACT(ISODOW FROM DATE '2001-02-16') AS INT) FROM table1 datasource_type = 'ADP';
```

---

</details>

<details markdown="block">
  <summary>
EXTRACT(FROM TIME)
  </summary>
  {: .text-delta }

ADB, ADP

```sql
SELECT CAST(EXTRACT(HOUR FROM TIME '20:38:40') AS INT) FROM table1 datasource_type = 'ADB';
SELECT CAST(EXTRACT(MINUTE FROM TIME '20:38:40') AS INT) FROM table1 datasource_type = 'ADB';
SELECT CAST(EXTRACT(SECOND FROM TIME '20:38:40') AS INT) FROM table1 datasource_type = 'ADB';
SELECT CAST(EXTRACT(MILLISECOND FROM TIME '20:38:40') AS INT) FROM table1 datasource_type = 'ADB';
SELECT CAST(EXTRACT(MICROSECOND FROM TIME '20:38:40') AS INT) FROM table1 datasource_type = 'ADB';
```

---

</details>

<details markdown="block">
  <summary>
EXTRACT(FROM TIMESTAMP)
  </summary>
  {: .text-delta }

ADB, ADQM, ADP

```sql
SELECT CAST(EXTRACT(DOW FROM TIMESTAMP '2001-02-16 00:00:00') AS INT) FROM table1 datasource_type = 'ADB';
SELECT CAST(EXTRACT(WEEK FROM TIMESTAMP '2001-02-16 00:00:00') AS INT) FROM table1 datasource_type = 'ADB';
SELECT CAST(EXTRACT(CENTURY FROM TIMESTAMP '2001-02-16 00:00:00') AS INT) FROM table1 datasource_type = 'ADB';
SELECT CAST(EXTRACT(QUARTER FROM TIMESTAMP '2001-02-16 00:00:00') AS INT) FROM table1 datasource_type = 'ADB';
SELECT EXTRACT(QUARTER FROM TIMESTAMP '2001-02-16 20:38:40') FROM table1 datasource_type = 'ADQM';
SELECT CAST(EXTRACT(YEAR FROM TIMESTAMP '2001-02-16 20:38:40') AS INT) FROM table1 datasource_type = 'ADB';
SELECT EXTRACT(YEAR FROM TIMESTAMP '2001-02-16 20:38:40') FROM table1 datasource_type = 'ADQM';
SELECT CAST(EXTRACT(MONTH FROM TIMESTAMP '2001-02-16 20:38:40') AS INT) FROM table1 datasource_type = 'ADB';
SELECT EXTRACT(MONTH FROM TIMESTAMP '2001-02-16 20:38:40') FROM table1 datasource_type = 'ADQM';
SELECT CAST(EXTRACT(DAY FROM TIMESTAMP '2001-02-16 20:38:40') AS INT) FROM table1 datasource_type = 'ADB';
SELECT EXTRACT(DAY FROM TIMESTAMP '2001-02-16 20:38:40') FROM table1 datasource_type = 'ADQM';
SELECT CAST(EXTRACT(HOUR FROM TIMESTAMP '2001-02-16 20:38:40') AS INT) FROM table1 datasource_type = 'ADB';
SELECT EXTRACT(HOUR FROM TIMESTAMP '2001-02-16 20:38:40') FROM table1 datasource_type = 'ADQM';
SELECT CAST(EXTRACT(MINUTE FROM TIMESTAMP '2001-02-16 20:38:40') AS INT) FROM table1 datasource_type = 'ADB';
SELECT EXTRACT(MINUTE FROM TIMESTAMP '2001-02-16 20:38:40') FROM table1 datasource_type = 'ADQM';
SELECT CAST(EXTRACT(SECOND FROM TIMESTAMP '2001-02-16 20:38:40') AS INT) FROM table1 datasource_type = 'ADB';
SELECT EXTRACT(SECOND FROM TIMESTAMP '2001-02-16 20:38:40') FROM table1 datasource_type = 'ADQM';
SELECT CAST(EXTRACT(MILLISECOND FROM TIMESTAMP '2001-02-16 20:38:40') AS INT) FROM table1 datasource_type = 'ADB';
SELECT CAST(EXTRACT(MICROSECOND FROM TIMESTAMP '2001-02-16 20:38:40') AS INT) FROM table1 datasource_type = 'ADB';
```

---

</details>

<details markdown="block">
  <summary>
LOCALTIME, LOCALTIME(precision)
  </summary>
  {: .text-delta }

ADB, ADP

```sql
SELECT LOCALTIME FROM table1 datasource_type = 'ADB';
SELECT LOCALTIME FROM table1 datasource_type = 'ADP';
SELECT CAST(LOCALTIME AS TIME) FROM table1 datasource_type = 'ADB';
SELECT CAST(LOCALTIME AS TIME) FROM table1 datasource_type = 'ADP';
```

---

ADB, ADP

```sql
SELECT LOCALTIME(3) FROM table1 datasource_type = 'ADB';
SELECT LOCALTIME(3) FROM table1 datasource_type = 'ADP';
SELECT CAST(LOCALTIME(3) AS TIME) FROM table1 datasource_type = 'ADB';
SELECT CAST(LOCALTIME(3) AS TIME) FROM table1 datasource_type = 'ADP';
```

---

</details>

<details markdown="block">
  <summary>
LOCALTIMESTAMP, LOCALTIMESTAMP(precision)
  </summary>
  {: .text-delta }

ADB, ADP

```sql
SELECT LOCALTIMESTAMP FROM table1 datasource_type = 'ADB';
SELECT LOCALTIMESTAMP FROM table1 datasource_type = 'ADP';
SELECT CAST(LOCALTIMESTAMP AS TIMESTAMP) FROM table1 datasource_type = 'ADB';
SELECT CAST(LOCALTIMESTAMP AS TIMESTAMP) FROM table1 datasource_type = 'ADP';
```

---

ADB, ADP

```sql
SELECT LOCALTIMESTAMP(3) FROM table1 datasource_type = 'ADB';
SELECT LOCALTIMESTAMP(3) FROM table1 datasource_type = 'ADP';
SELECT CAST(LOCALTIMESTAMP(3) AS TIMESTAMP) FROM table1 datasource_type = 'ADB';
SELECT CAST(LOCALTIMESTAMP(3) AS TIMESTAMP) FROM table1 datasource_type = 'ADP';
```

---

</details>

<details markdown="block">
  <summary>
MONTH(), QUARTER(), WEEK(), YEAR()
  </summary>
  {: .text-delta }

ADB, ADP

```sql
SELECT CAST(MONTH(DATE '2001-02-16') AS INT) FROM table1 datasource_type = 'ADB';
SELECT CAST(MONTH(DATE '2001-02-16') AS INT) FROM table1 datasource_type = 'ADP';
SELECT CAST(MONTH(TIMESTAMP '2001-02-16 20:38:40') AS INT) FROM table1 datasource_type = 'ADB';
SELECT CAST(MONTH(TIMESTAMP '2001-02-16 20:38:40') AS INT) FROM table1 datasource_type = 'ADP';
```

---

ADB, ADP

```sql
SELECT CAST(QUARTER(DATE '2001-02-16') AS INT) FROM table1 datasource_type = 'ADB';
SELECT CAST(QUARTER(DATE '2001-02-16') AS INT) FROM table1 datasource_type = 'ADP';
SELECT CAST(QUARTER(TIMESTAMP '2001-02-16 20:38:40') AS INT) FROM table1 datasource_type = 'ADB';
SELECT CAST(QUARTER(TIMESTAMP '2001-02-16 20:38:40') AS INT) FROM table1 datasource_type = 'ADP';
```

---

ADB, ADP

```sql
SELECT CAST(WEEK(DATE '2001-02-16') AS INT) FROM table1 datasource_type = 'ADB';
SELECT CAST(WEEK(DATE '2001-02-16') AS INT) FROM table1 datasource_type = 'ADP';
SELECT CAST(WEEK(TIMESTAMP '2001-02-16 20:38:40') AS INT) FROM table1 datasource_type = 'ADB';
SELECT CAST(WEEK(TIMESTAMP '2001-02-16 20:38:40') AS INT) FROM table1 datasource_type = 'ADP';
```

---

ADB, ADP

```sql
SELECT CAST(YEAR(DATE '2001-02-16') AS INT) FROM table1 datasource_type = 'ADB';
SELECT CAST(YEAR(TIMESTAMP '2001-02-16 20:38:40') AS INT) FROM table1 datasource_type = 'ADB';
```

---

</details>

*Системные функции и операторы*

<details markdown="block">
  <summary>

CURRENT_USER, SESSION_USER, CURRENT_ROLE, CURRENT_SCHEMA

  </summary>
  {: .text-delta }

ADB, ADP

```sql
SELECT CURRENT_USER FROM table1 datasource_type = 'ADB';
SELECT CURRENT_USER FROM table1 datasource_type = 'ADP';
```

---

ADB, ADP

```sql
SELECT SESSION_USER FROM table1 datasource_type = 'ADB';
SELECT SESSION_USER FROM table1 datasource_type = 'ADP';
```

---

ADB, ADP

```sql
SELECT CURRENT_ROLE FROM table1 datasource_type = 'ADB';
SELECT CURRENT_ROLE FROM table1 datasource_type = 'ADP';
```

---

ADB, ADP

```sql
SELECT CURRENT_SCHEMA FROM table1 datasource_type = 'ADB';
SELECT CURRENT_SCHEMA FROM table1 datasource_type = 'ADP';
```

---

</details>

*Строковые функции и операторы*

<details markdown="block">
  <summary>

POSITION

  </summary>
  {: .text-delta }

ADB, ADP

```sql
SELECT POSITION('c' IN 'abcdef') FROM table1 datasource_type = 'ADB';
SELECT POSITION('z' IN 'abcdef') FROM table1 datasource_type = 'ADP';
```

---

</details>

<details markdown="block">
  <summary>

UPPER

  </summary>
  {: .text-delta }

ADB, ADQM, ADG, ADP

```sql
SELECT UPPER('abcdef') FROM table1 datasource_type = 'ADB';
SELECT UPPER('abcdef') FROM table1 datasource_type = 'ADQM';
SELECT UPPER('abcdef') FROM table1 datasource_type = 'ADG';
SELECT UPPER('abcdef') FROM table1 datasource_type = 'ADP';
```

---

</details>

<details markdown="block">
  <summary>

LOWER

  </summary>
  {: .text-delta }

ADB, ADP

```sql
SELECT LOWER('ABCDEG') FROM table1 datasource_type = 'ADB';
SELECT LOWER('ABCDEG') FROM table1 datasource_type = 'ADQM';
SELECT LOWER('ABCDEG') FROM table1 datasource_type = 'ADG';
SELECT LOWER('ABCDEG') FROM table1 datasource_type = 'ADP';
```

---

</details>

<details markdown="block">
  <summary>

SUBSTRING

  </summary>
  {: .text-delta }

ADB, ADQM, ADP

```sql
SELECT SUBSTRING('ABCDEG', 3, 2) FROM table1 datasource_type = 'ADB';
SELECT SUBSTRING('ABCDEG', 3, 2) FROM table1 datasource_type = 'ADQM';
SELECT SUBSTRING('ABCDEG', 3, 2) FROM table1 datasource_type = 'ADP';
```

---

</details>

<details markdown="block">
  <summary>

COALESCE

  </summary>
  {: .text-delta }

ADB, ADG, ADP

```sql
SELECT COALESCE(boolean_col,true) from table1 datasource_type = 'ADB';
SELECT COALESCE(boolean_col,true) from table1 datasource_type = 'ADG';
SELECT COALESCE(boolean_col,true) from table1 datasource_type = 'ADP';
```

---

ADB, ADQM, ADG, ADP

```sql
SELECT COALESCE(int_col,1) from db99990.accounts datasource_type = 'ADB';
SELECT COALESCE(int_col,1) from db99990.accounts datasource_type = 'ADQM';
SELECT COALESCE(int_col,1) from db99990.accounts datasource_type = 'ADG';
SELECT COALESCE(int_col,1) from db99990.accounts datasource_type = 'ADP';
```

---

ADB, ADQM, ADP

```sql
SELECT COALESCE(bigint_col,1) FROM table1 datasource_type = 'ADB';
SELECT COALESCE(bigint_col,1) FROM table1 datasource_type = 'ADQM';
SELECT COALESCE(bigint_col,1) FROM table1 datasource_type = 'ADP';
```

---

ADB, ADQM, ADG, ADP

```sql
SELECT COALESCE(int32_col,1) FROM table1 datasource_type = 'ADB';
SELECT COALESCE(int32_col,1) FROM table1 datasource_type = 'ADQM';
SELECT COALESCE(int32_col,1) FROM table1 datasource_type = 'ADG';
SELECT COALESCE(int32_col,1) FROM table1 datasource_type = 'ADP';
```

---

ADB, ADP

```sql
SELECT COALESCE(float_col,1.0) FROM table1 datasource_type = 'ADB';
SELECT COALESCE(float_col,1.0) FROM table1 datasource_type = 'ADP';
```

---

ADB, ADP

```sql
SELECT COALESCE(double_col,1.0) FROM table1 datasource_type = 'ADB';
SELECT COALESCE(double_col,1.0) FROM table1 datasource_type = 'ADP';
```

---

ADB, ADQM, ADG, ADP

```sql
SELECT COALESCE(varchar_col,'1.0') FROM table1 datasource_type = 'ADB';
SELECT COALESCE(CAST(varchar_col AS VARCHAR),'1.0') FROM table1 datasource_type = 'ADQM';
SELECT COALESCE(varchar_col,'1.0') FROM table1 datasource_type = 'ADG';
SELECT COALESCE(varchar_col,'1.0') FROM table1 datasource_type = 'ADP';
```

---

ADB, ADQM*, ADP

```sql
SELECT COALESCE(date_col,'2001-01-01') FROM table1 datasource_type = 'ADB';
SELECT COALESCE(date_col,'2001-01-01') FROM table1 datasource_type = 'ADQM';
SELECT COALESCE(date_col,'2001-01-01') FROM table1 datasource_type = 'ADP';
```

---

ADB, ADQM, ADP

```sql
SELECT COALESCE(date_col,CAST('2001-01-01' AS DATE)) FROM table1 datasource_type = 'ADB';
SELECT COALESCE(date_col,CAST('2001-01-01' AS DATE)) FROM table1 datasource_type = 'ADQM';
SELECT COALESCE(date_col,CAST('2001-01-01' AS DATE)) FROM table1 datasource_type = 'ADP';
```

---

ADB, ADQM, ADP

```sql
SELECT COALESCE(time_col,'11:12:13') FROM table1 datasource_type = 'ADB';
SELECT COALESCE(time_col,'11:12:13') FROM table1 datasource_type = 'ADQM';
SELECT COALESCE(time_col,'11:12:13') FROM table1 datasource_type = 'ADP';
```

---

ADB, ADQM*, ADG, ADP

```sql
SELECT COALESCE(timestamp_col,'2001-01-01 11:12:13') FROM table1 datasource_type = 'ADB';
SELECT COALESCE(timestamp_col,'2001-01-01 11:12:13') FROM table1 datasource_type = 'ADQM';
SELECT COALESCE(timestamp_col,'2001-01-01 11:12:13') FROM table1 datasource_type = 'ADP';
```

---

ADB, ADQM, ADP

```sql
SELECT COALESCE(uuid_col,'1') FROM table1 datasource_type = 'ADB';
SELECT COALESCE(uuid_col,'1') FROM table1 datasource_type = 'ADQM';
SELECT COALESCE(uuid_col,'1') FROM table1 datasource_type = 'ADP';
```

---

ADB, ADG, ADP

```sql
SELECT COALESCE(char_col,'1') FROM table1 datasource_type = 'ADB';
SELECT COALESCE(char_col,'1') FROM table1 datasource_type = 'ADG';
SELECT COALESCE(char_col,'1') FROM table1 datasource_type = 'ADP';
```

---

ADB, ADQM, ADP

```sql
SELECT COALESCE(link_col,'http://www.google.com') FROM table1 datasource_type = 'ADB';
SELECT COALESCE(link_col,'http://www.google.com') FROM table1 datasource_type = 'ADQM';
SELECT COALESCE(link_col,'http://www.google.com') FROM table1 datasource_type = 'ADP';
```

---

</details>

<details markdown="block">
  <summary>

TRIM

  </summary>
  {: .text-delta }

ADB, ADQM, ADG, ADP

```sql
SELECT TRIM('   ABC XYZ   ') FROM table1 datasource_type = 'ADB';
SELECT TRIM('   ABC XYZ   ') FROM table1 datasource_type = 'ADQM';
SELECT TRIM('   ABC XYZ   ') FROM table1 datasource_type = 'ADG';
SELECT TRIM('   ABC XYZ   ') FROM table1 datasource_type = 'ADP';
```

---

ADB, ADG, ADP

```sql
SELECT COALESCE(boolean_col,true) from table1 datasource_type = 'ADB';
SELECT COALESCE(boolean_col,true) from table1 datasource_type = 'ADG';
SELECT COALESCE(boolean_col,true) from table1 datasource_type = 'ADP';
```

---

</details>

<details markdown="block">
  <summary>

REPLACE

  </summary>
  {: .text-delta }

ADB, ADQM, ADG, ADP

```sql
SELECT REPLACE('  abc xyz  ','ab', 'x') FROM table1 datasource_type = 'ADB';
SELECT REPLACE('  abc xyz  ','ab', 'x') FROM table1 datasource_type = 'ADQM';
SELECT REPLACE('  abc xyz  ','ab', 'x') FROM table1 datasource_type = 'ADG';
SELECT REPLACE('  abc xyz  ','ab', 'x') FROM table1 datasource_type = 'ADP';
```

---

</details>

<details markdown="block">
  <summary>

CONCATENATION

  </summary>
  {: .text-delta }

ADB, ADQM, ADG, ADP

```sql
SELECT 'abc' || 'xyz' FROM table1 datasource_type = 'ADB';
SELECT 'abc' || 'xyz' FROM table1 datasource_type = 'ADQM';
SELECT 'abc' || 'xyz' FROM table1 datasource_type = 'ADG';
SELECT 'abc' || 'xyz' FROM table1 datasource_type = 'ADP';
```

---

</details>

<details markdown="block">
  <summary>

INITCAP

  </summary>
  {: .text-delta }

ADB, ADP

```sql
SELECT INITCAP('abc def ghi xyz') FROM table1 datasource_type = 'ADB';
SELECT INITCAP('abc def ghi xyz') FROM table1 datasource_type = 'ADP';
```

---

</details>

*Математические функции и операторы*

<details markdown="block">
  <summary>

ABS

  </summary>
  {: .text-delta }

ADB, ADQM, ADG, ADP

```sql
SELECT ABS(-2.0) FROM table1 datasource_type = 'ADB';
SELECT ABS(-2) FROM table1 datasource_type = 'ADQM';
SELECT ABS(2.0) FROM table1 datasource_type = 'ADG';
SELECT ABS(-2.5) FROM table1 datasource_type = 'ADP';
```

---

</details>

<details markdown="block">
  <summary>

ROUND

  </summary>
  {: .text-delta }

ADB, ADQM, ADG, ADP

```sql
SELECT ROUND(-2.5) FROM table1 datasource_type = 'ADB';
SELECT ROUND(-2.3) FROM table1 datasource_type = 'ADQM';
SELECT ROUND(-2.3) FROM table1 datasource_type = 'ADG';
SELECT ROUND(2.5) FROM table1 datasource_type = 'ADP';
```

---

</details>
