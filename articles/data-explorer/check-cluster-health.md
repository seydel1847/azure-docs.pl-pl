---
title: Sprawdzanie kondycji klastra usługi Azure Eksplorator danych
description: W tym artykule opisano kroki w celu ustalenia, czy klaster Eksploratora danych usługi Azure jest w dobrej kondycji.
author: orspod
ms.author: v-orspod
ms.reviewer: mblythe
ms.service: data-explorer
services: data-explorer
ms.topic: conceptual
ms.date: 09/24/2018
ms.openlocfilehash: d07873b34a41ff20b5007a88743f6b150d4d8a3d
ms.sourcegitcommit: 6e09760197a91be564ad60ffd3d6f48a241e083b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/29/2018
ms.locfileid: "50212832"
---
# <a name="check-the-health-of-an-azure-data-explorer-cluster"></a>Sprawdzanie kondycji klastra usługi Azure Eksplorator danych

Istnieje kilka czynników, które mają wpływ na kondycję klastra Eksploratora danych usługi Azure, w tym procesora CPU, pamięci i podsystem dysku. W tym artykule przedstawiono niektóre podstawowe kroki można wykonać w celu oceniania kondycji klastra.

1. Zaloguj się do witryny [https://dataexplorer.azure.com](https://dataexplorer.azure.com).

1. W okienku po lewej stronie wybierz klaster, a następnie uruchom następujące polecenie.

    ```Kusto
    .show diagnostics
    | project IsHealthy
    ```
    Dane wyjściowe 1 jest w dobrej kondycji; dane wyjściowe 0 jest w złej kondycji.

1. Zaloguj się do [witryny Azure portal](https://portal.azure.com), a następnie przejdź do klastra.

1. W obszarze **monitorowanie**, wybierz opcję **metryki**, a następnie wybierz **zachować aktywności**, jak pokazano na poniższej ilustracji. Dane wyjściowe zbliżone do wartości 1 oznacza, że klaster działa prawidłowo.

    ![Metryka zachować aktywności klastra](media/check-cluster-health/portal-metrics.png)

1. Istnieje możliwość dodać innych metryk do wykresu. Następnie wybierz wykres **Dodaj metrykę**. Wybierz inną metrykę — w tym przykładzie **Procesora**.

    ![Dodawanie metryki](media/check-cluster-health/add-metric.png)

1. Jeśli potrzebujesz pomocy w diagnozowaniu problemów z kondycją klastra, otwórz żądanie pomocy technicznej w [witryny Azure portal](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/overview).