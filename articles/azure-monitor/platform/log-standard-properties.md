---
title: Właściwości standardowe w dokumentacji usługi Azure Monitor Log Analytics | Dokumentacja firmy Microsoft
description: Opisuje właściwości, które są wspólne dla wielu typów danych w usłudze Azure Monitor Log Analytics.
services: log-analytics
documentationcenter: ''
author: bwren
manager: carmonm
editor: ''
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 01/14/2019
ms.author: bwren
ms.openlocfilehash: 27c732a2ddd21401ffbefa727cbb8001ec288293
ms.sourcegitcommit: ba9f95cf821c5af8e24425fd8ce6985b998c2982
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/17/2019
ms.locfileid: "54381949"
---
# <a name="standard-properties-in-log-analytics-records"></a>Właściwości standardowe w rekordach usługi Log Analytics
Dane w [usługi Log Analytics](../log-query/log-query-overview.md) jest przechowywany jako zestaw rekordów, każdy z typem danych, który ma unikatowego zestawu właściwości. Wiele typów danych, ma standardowych właściwości, które są wspólne dla wielu typów. W tym artykule opisano te właściwości i przedstawiono przykłady jak ich używać w zapytaniach.

Niektóre z tych właściwości są nadal w trakcie zaimplementowana, może je wyświetlić, w niektórych typach danych, ale jeszcze nie w innych.

## <a name="timegenerated"></a>TimeGenerated
**TimeGenerated** właściwość zawiera Data i godzina utworzenia rekordu. Zapewnia wspólnej właściwości na potrzeby filtrowania lub podsumowywanie według czasu. Po wybraniu zakres czasu dla widoku lub pulpitu nawigacyjnego w witrynie Azure portal, używa TimeGenerated do filtrowania wyników.

### <a name="examples"></a>Przykłady

Następujące zapytanie zwraca liczbę zdarzeń błędu utworzone dla każdego dnia w poprzednim tygodniu.

```Kusto
Event
| where EventLevelName == "Error" 
| where TimeGenerated between(startofweek(ago(7days))..endofweek(ago(7days))) 
| summarize count() by bin(TimeGenerated, 1day) 
| sort by TimeGenerated asc 
```

## <a name="type"></a>Typ
**Typu** właściwość przechowuje nazwę tabeli, z którego pobrano rekord może również być uważane za typu rekordu. Ta właściwość jest przydatna w zapytaniach, które łączą rekordy z wielu tabel, takich jak implementacje używające `search` operator rozróżnienie między rekordami różnych typów. **$table** mogą być używane zamiast **typu** w jednych miejscach.

### <a name="examples"></a>Przykłady
Następujące zapytanie zwraca liczbę rekordów według typu zebrane w ciągu ostatniej godziny.

```Kusto
search * 
| where TimeGenerated > ago(1h) 
| summarize count() by Type 
```

## <a name="resourceid"></a>\_ResourceId
 **\_ResourceId** właściwość przechowuje unikatowy identyfikator zasobu, który jest skojarzony rekord. Dzięki temu standardowy właściwość użycie ustal zakres zapytania do tylko rekordy z określonego zasobu lub Dołącz do powiązanych danych dla wielu tabel.

Dla zasobów platformy Azure, wartość **_ResourceId** jest [zasobów platformy Azure, adres URL Identyfikatora](../../azure-resource-manager/resource-group-template-functions-resource.md). Właściwość jest obecnie ograniczona do zasobów platformy Azure, ale będzie można rozszerzyć do zasobów spoza platformy Azure, takich jak komputery w środowisku lokalnym.

> [!NOTE]
> Niektóre typy danych mają już pola, które zawierają identyfikator zasobu platformy Azure lub części w co najmniej o takich jak identyfikator subskrypcji. Te pola są zachowywane dla zgodności z poprzednimi wersjami, zaleca się jej na potrzeby _ResourceId wykonywać korelację między, ponieważ będzie bardziej spójny.

### <a name="examples"></a>Przykłady
Następujące zapytanie łączy dane wydajności i zdarzeń dla każdego komputera. Pokazuje wszystkie zdarzenia o identyfikatorze _101_ i użycie procesora przez ponad 50%.

```Kusto
Perf 
| where CounterName == "% User Time" and CounterValue  > 50 and _ResourceId != "" 
| join kind=inner (     
    Event 
    | where EventID == 101 
) on _ResourceId
```

Poniższe zapytanie sprzęga _AzureActivity_ rekordy z _SecurityEvent_ rekordów. Pokazuje wszystkie operacje wykonywane działania użytkowników, które zostały zarejestrowane w na tych maszynach.

```Kusto
AzureActivity 
| where  
    OperationName in ("Restart Virtual Machine", "Create or Update Virtual Machine", "Delete Virtual Machine")  
    and ActivityStatus == "Succeeded"  
| join kind= leftouter (    
   SecurityEvent 
   | where EventID == 4624  
   | summarize LoggedOnAccounts = makeset(Account) by _ResourceId 
) on _ResourceId  
```

## <a name="isbillable"></a>\_IsBillable
 **\_IsBillable** właściwość określa, czy odebrane dane są płatne. Dane za pomocą  **\_IsBillable** równa _false_ są zbierane za darmo i nie są rozliczane na koncie platformy Azure.

### <a name="examples"></a>Przykłady
Aby uzyskać listę komputerów, które wysyłają typy danych rozliczane, użyj następującego zapytania:

> [!NOTE]
> Korzystanie z zapytań za pomocą `union withsource = tt *` oszczędnie skanowania różnych typów danych są drogie do wykonania. 

```Kusto
union withsource = tt * 
| where _IsBillable == true 
| extend computerName = tolower(tostring(split(Computer, '.')[0]))
| where computerName != ""
| summarize TotalVolumeBytes=sum(_BilledSize) by computerName
```

Może to rozszerzona, aby zwrócić liczbę komputerów, na godzinę, które wysyłają rozliczane typów danych:

```Kusto
union withsource = tt * 
| where _IsBillable == true 
| extend computerName = tolower(tostring(split(Computer, '.')[0]))
| where computerName != ""
| summarize dcount(computerName) by bin(TimeGenerated, 1h) | sort by TimeGenerated asc
```

## <a name="billedsize"></a>\_BilledSize
 **\_BilledSize** właściwość określa rozmiar w bajtach, danych, które będzie rozliczane na koncie platformy Azure, jeśli  **\_IsBillable** ma wartość true.

### <a name="examples"></a>Przykłady
Aby wyświetlić rozmiar płatnych zdarzeń wprowadzanych na komputerze, użyj `_BilledSize` właściwość, która zapewnia rozmiar w bajtach:

```Kusto
union withsource = tt * 
| where _IsBillable == true 
| summarize Bytes=sum(_BilledSize) by  Computer | sort by Bytes nulls last 
```

Aby wyświetlić liczbę zdarzeń przetwarzanych na komputerze, użyj następującego zapytania:

```Kusto
union withsource = tt *
| summarize count() by Computer | sort by count_ nulls last
```

Aby wyświetlić liczbę płatnych zdarzeń wprowadzanych na komputerze, użyj następującego zapytania: 

```Kusto
union withsource = tt * 
| where _IsBillable == true 
| summarize count() by Computer  | sort by count_ nulls last
```

Użyj następującego zapytania wyświetlić liczniki dla typów danych płatnych wysyłania danych do konkretnego komputera:

```Kusto
union withsource = tt *
| where Computer == "computer name"
| where _IsBillable == true 
| summarize count() by tt | sort by count_ nulls last 
```


## <a name="next-steps"></a>Kolejne kroki

- Przeczytaj więcej na temat [są przechowywane dane usługi Log Analytics](../log-query/log-query-overview.md).
- Uzyskaj lekcji na [Pisanie zapytań w usłudze Log Analytics](../../azure-monitor/log-query/get-started-queries.md).
- Uzyskaj lekcji na [sprzężenie tabel w zapytań usługi Log Analytics](../../azure-monitor/log-query/joins.md).
