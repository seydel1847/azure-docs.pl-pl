---
title: Przydatne operatorów zapytań usługi Azure Log Analytics | Dokumentacja firmy Microsoft
description: Typowe funkcje do użycia w różnych scenariuszach zapytań usługi Log Analytics.
services: log-analytics
documentationcenter: ''
author: bwren
manager: carmonm
editor: ''
ms.assetid: ''
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.topic: conceptual
ms.date: 08/21/2018
ms.author: bwren
ms.openlocfilehash: 060b1e469a31c335f062ccd332157d13e64f9318
ms.sourcegitcommit: 5b869779fb99d51c1c288bc7122429a3d22a0363
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/10/2018
ms.locfileid: "53183986"
---
# <a name="useful-operators-in-log-analytics-queries"></a>Przydatne operatorów zapytań usługi Log Analytics

W poniższej tabeli przedstawiono niektóre typowe funkcje do użycia w różnych scenariuszach zapytań usługi Log Analytics.

## <a name="useful-operators"></a>Przydatne operatory

Kategoria                                |Funkcja analizy odpowiednie
----------------------------------------|----------------------------------------
Wybór i kolumny aliasów            |`project`, `project-away`, `extend`
Tabele tymczasowe i stałe          |`let scalar_alias_name = …;` <br> `let table_alias_name =  …  …  … ;`| 
Porównywanie i operatory ciągów         |`startswith`, `!startswith`, `has`, `!has` <br> `contains`, `!contains`, `containscs` <br> `hasprefix`, `!hasprefix`, `hassuffix`, `!hassuffix`, `in`, `!in` <br> `matches regex` <br> `==`, `=~`, `!=`, `!~`
Typowe funkcje ciągów                 |`strcat()`, `replace()`, `tolower()`, `toupper()`, `substring()`, `strlen()`
Typowe funkcje matematyczne                   |`sqrt()`, `abs()` <br> `exp()`, `exp2()`, `exp10()`, `log()`, `log2()`, `log10()`, `pow()` <br> `gamma()`, `gammaln()`
Analiza tekstu                            |`extract()`, `extractjson()`, `parse`, `split()`
Ograniczanie danych wyjściowych                         |`take`, `limit`, `top`, `sample`
Funkcje daty                          |`now()`, `ago()` <br> `datetime()`, `datepart()`, `timespan` <br> `startofday()`, `startofweek()`, `startofmonth()`, `startofyear()` <br> `endofday()`, `endofweek()`, `endofmonth()`, `endofyear()` <br> `dayofweek()`, `dayofmonth()`, `dayofyear()` <br> `getmonth()`, `getyear()`, `weekofyear()`, `monthofyear()`
Grupowanie i agregacji                |`summarize by` <br> `max()`, `min()`, `count()`, `dcount()`, `avg()`, `sum()` <br> `stddev()`, `countif()`, `dcountif()`, `argmax()`, `argmin()` <br> `percentiles()`, `percentile_array()`
Sprzężenia i unie                        |`join kind=leftouter`, `inner`, `rightouter`, `fullouter`, `leftanti` <br> `union`
Sortowania, kolejność                             |`sort`, `order` 
Obiekt dynamiczny (JSON i array)         |`parsejson()` <br> `makeset()`, `makelist()` <br> `split()`, `arraylength()` <br> `zip()`, `pack()`
Operatory logiczne                       |`and`, `or`, `iff(condition, value_t, value_f)` <br> `binary_and()`, `binary_or()`, `binary_not()`, `binary_xor()`
Uczenie maszynowe                        |`evaluate autocluster`, `basket`, `diffpatterns`, `extractcolumns`


## <a name="next-steps"></a>Kolejne kroki

- Przejdź przez lekcji [Pisanie zapytań w usłudze Log Analytics](get-started-queries.md).
