---
title: Dokumentacja języka w usłudze Azure Monitor Log Analytics | Dokumentacja firmy Microsoft
description: Informacje referencyjne dotyczące języka zapytań Eksploratora danych używane przez usługę Log Analytics. Zawiera dodatkowe elementy specyficzne dla usługi Log Analytics i elementy nieobsługiwane w zapytaniach usługi Log Analytics.
services: log-analytics
documentationcenter: ''
author: bwren
manager: carmonm
editor: ''
ms.assetid: ''
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 10/31/2018
ms.author: bwren
ms.openlocfilehash: 645750ec40f0aba2ef58c096a72125fad2947719
ms.sourcegitcommit: 5b869779fb99d51c1c288bc7122429a3d22a0363
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/10/2018
ms.locfileid: "53186263"
---
# <a name="log-analytics-query-language-differences"></a>Zaloguj się różnice języka zapytań usługi Analytics

Gdy [usługi Log Analytics](log-query-overview.md) jest oparta na [Eksploratora danych usługi Azure](/azure/data-explorer) i używa [sam język zapytań](/azure/kusto/query), wersję języka ma pewne różnice. W tym artykule identyfikuje elementy, które różnią się między wersją język używany do Eksploratora danych i wersja używana do zapytań usługi Log Analytics.

## <a name="data-explorer-elements-not-supported-in-log-analytics"></a>Elementy Eksploratora danych nie jest obsługiwane w usłudze Log Analytics
W poniższych sekcjach opisano elementy języka zapytań Eksploratora danych, które nie są obsługiwane przez usługę Log Analytics.

### <a name="statements-not-supported-in-log-analytics"></a>Instrukcje nie są obsługiwane w usłudze Log Analytics

* [Alias](/azure/kusto/query/aliasstatement)
* [Parametry zapytania](/azure/kusto/query/queryparametersstatement)

### <a name="functions-not-supported-in-log-analytics"></a>Funkcje nieobsługiwane w usłudze Log Analytics

* [cluster()](/azure/kusto/query/clusterfunction)
* [cursor_after()](/azure/kusto/query/cursorafterfunction)
* [cursor_before_or_at()](/azure/kusto/query/cursorbeforeoratfunction)
* [cursor_current(), current_cursor()](/azure/kusto/query/cursorcurrent)
* [Database()](/azure/kusto/query/databasefunction)
* [current_principal()](/azure/kusto/query/current-principalfunction)
* [extent_id()](/azure/kusto/query/extentidfunction)
* [extent_tags()](/azure/kusto/query/extenttagsfunction)

### <a name="operators-not-supported-in-log-analytics"></a>Operatory nie obsługiwane w usłudze Log Analytics

* [Sprzężenie krzyżowe klastra](/azure/kusto/query/joincrosscluster)
* [externaldata operator](/azure/kusto/query/externaldata-operator)

### <a name="plugins-not-supported-in-log-analytics"></a>Dodatki nie są obsługiwane w usłudze Log Analytics

* [Wtyczka sql_request](/azure/kusto/query/sqlrequestplugin)


## <a name="additional-operators-in-log-analytics"></a>Dodatkowe operatory w usłudze Log Analytics
Następujące operatory obsługi określonych funkcji usługi Log Analytics i nie są dostępne poza usługą Log Analytics.

* [metodzie App()](app-expression.md)
* [Workspace()](workspace-expression.md)

## <a name="next-steps"></a>Kolejne kroki

- Pobieranie odwołań do różnych [zasoby dotyczące pisania zapytań usługi Log Analytics](query-language.md).
- Dostęp do pełnego [odwoływać się do dokumentacji języka zapytań w Eksploratorze danych](/azure/kusto/query/).
