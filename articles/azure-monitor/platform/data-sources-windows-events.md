---
title: Zbieranie i analizowanie dzienników zdarzeń Windows w usłudze Log Analytics | Dokumentacja firmy Microsoft
description: W tym artykule opisano sposób konfigurowania zbierania dzienników zdarzeń Windows przez usługę Log Analytics i szczegółowe informacje o rekordy, które tworzą.
services: log-analytics
documentationcenter: ''
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: ee52f564-995b-450f-a6ba-0d7b1dac3f32
ms.service: log-analytics
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/28/2018
ms.author: bwren
ms.openlocfilehash: a60c5c41c3f7f0c26788aa9f986af076d9e82c2f
ms.sourcegitcommit: 30d23a9d270e10bb87b6bfc13e789b9de300dc6b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/08/2019
ms.locfileid: "54102605"
---
# <a name="windows-event-log-data-sources-in-log-analytics"></a>Źródła danych dziennika zdarzeń Windows w usłudze Log Analytics
Dzienniki zdarzeń Windows są jedną z najbardziej typowych [źródeł danych](agent-data-sources.md) do zbierania danych przy użyciu agentów Windows, ponieważ wiele aplikacji zapisu w dzienniku zdarzeń Windows.  Oprócz określenia żadnych dzienników niestandardowych utworzone przez aplikacje, które są potrzebne do monitorowania może zbierać zdarzenia z dzienników standardowych, takich jak systemu i aplikacji.

![Zdarzenia Windows](media/data-sources-windows-events/overview.png)     

## <a name="configuring-windows-event-logs"></a>Dzienniki konfigurowanie zdarzeń Windows
Skonfiguruj dzienniki zdarzeń Windows z [menu danych w zaawansowanych ustawieniach](agent-data-sources.md#configuring-data-sources).

Usługa log Analytics zbiera tylko zdarzenia z dzienników zdarzeń Windows, które są określone w ustawieniach.  Możesz dodać dziennik zdarzeń przez wpisanie nazwy dziennika, a następnie klikając polecenie **+**.  Dla każdego dziennika są zbierane tylko zdarzenia o ważności wybranych.  Zaznacz ważności dla określonego dziennika, które mają być zbierane.  Nie można podać wszelkie dodatkowe kryteria, aby filtrować zdarzenia.

Podczas wpisywania nazwy dziennika zdarzeń, usługa Log Analytics oferuje sugestie dotyczące nazw pospolitych dziennika zdarzeń. Jeśli dziennik, który chcesz dodać, nie ma na liście, możesz je dodać, wpisując pełną nazwę dziennika. Pełna nazwa dziennika można znaleźć za pomocą Podglądu zdarzeń. W Podglądzie zdarzeń, otwórz *właściwości* strony dziennika i skopiuj ciąg z *imię i nazwisko* pola.

![Konfiguruj zdarzenia Windows](media/data-sources-windows-events/configure.png)

## <a name="data-collection"></a>Zbieranie danych
Usługa log Analytics zbiera każdego zdarzenia, które odpowiada wybranej ważności z monitorowanych dziennika zdarzeń, podczas tworzenia zdarzenia.  Agent rejestruje jej miejscu w każdym dzienniku zdarzeń, który zbiera z.  Jeśli agent przejdzie do trybu offline w okresie czasu, następnie zbiera zdarzenia z tam, gdzie ją ostatnia przerwaliśmy, nawet jeśli te zdarzenia zostały utworzone, gdy agent był w trybie offline.  Istnieje możliwość dla tych zdarzeń nie można pobrać, jeśli w dzienniku zdarzeń opakowuje ze zdarzeniami niepobranych zostaną zastąpione, gdy agent jest w trybie offline.

>[!NOTE]
>Usługa log Analytics nie są zbierane zdarzenia inspekcji utworzone przez program SQL Server ze źródła *MSSQLSERVER* z Identyfikatorem zdarzenia 18453, który zawiera słowa kluczowe — *klasycznego* lub *Sukces inspekcji* i słowo kluczowe *0xa0000000000000*.
>

## <a name="windows-event-records-properties"></a>Właściwości rekordy zdarzeń Windows
Rekordy zdarzeń Windows mają typ **zdarzeń** i mają właściwości podane w poniższej tabeli:

| Właściwość | Opis |
|:--- |:--- |
| Computer (Komputer) |Nazwa komputera, na którym zostały zebrane zdarzenia. |
| EventCategory |Kategoria zdarzenia. |
| EventData |Wszystkie dane zdarzeń w formacie nieprzetworzonym. |
| Identyfikator zdarzenia |Numer zdarzenia. |
| eventLevel |Ważność zdarzenia w forma liczbowa. |
| EventLevelName |Ważność zdarzenia w postaci tekstu. |
| Dziennik zdarzeń |Nazwa dziennika zdarzeń, które zostały zebrane zdarzenia. |
| ParameterXml |Wartości parametrów zdarzenia w formacie XML. |
| ManagementGroupName |Nazwa grupy zarządzania agentów programu System Center Operations Manager.  W innych agentów ta wartość to AOI-<workspace ID> |
| RenderedDescription |Opis zdarzenia przy użyciu wartości parametrów |
| Element źródłowy |Źródło zdarzenia. |
| SourceSystem |Typ agenta, które zostały zebrane zdarzenia. <br> Łączenie OpsManager — Windows agent, bezpośrednio lub zarządzania programu Operations Manager <br> Linux — Wszyscy agenci systemu Linux  <br> AzureStorage — Diagnostyka Azure |
| TimeGenerated |Data i godzina utworzenia zdarzenia w Windows. |
| UserName |Nazwa użytkownika konta, które są rejestrowane zdarzenia. |

## <a name="log-queries-with-windows-events"></a>Dziennik zapytań ze zdarzeniami Windows
Poniższa tabela zawiera przykłady różnych zapytań dziennika, które pobierają rekordy zdarzeń Windows.

| Zapytanie | Opis |
|:---|:---|
| Wydarzenie |Wszystkie zdarzenia Windows. |
| Zdarzenie &#124; gdzie EventLevelName == "error" |Windows wszystkich zdarzeń o ważności błędu. |
| Zdarzenie &#124; Podsumuj count() według źródła |Liczba Windows zdarzenia według źródła. |
| Zdarzenie &#124; gdzie EventLevelName == "error" &#124; Podsumuj count() według źródła |Zdarzenia błędu liczba Windows według źródła. |


## <a name="next-steps"></a>Kolejne kroki
* Skonfiguruj usługę Log Analytics do gromadzenia innych [źródeł danych](agent-data-sources.md) do analizy.
* Dowiedz się więcej o [rejestrowania zapytań](../../log-analytics/log-analytics-queries.md) analizować dane zbierane z innych źródeł danych i rozwiązań.  
* Konfigurowanie [zbieranie liczników wydajności](data-sources-performance-counters.md) z agentów użytkownika Windows.
