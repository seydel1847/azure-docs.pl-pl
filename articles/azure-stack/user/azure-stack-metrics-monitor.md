---
title: Używanie danych monitorowania z usługi Azure Stack | Dokumentacja firmy Microsoft
description: Dowiedz się więcej na temat opcji, co umożliwia korzystanie z danych monitorowania z usługi Azure Stack.
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2018
ms.author: mabrigg
ms.openlocfilehash: fbd4552a9e40f16a6fedec4e04be0d7d6d39351d
ms.sourcegitcommit: 333d4246f62b858e376dcdcda789ecbc0c93cd92
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2018
ms.locfileid: "52724489"
---
# <a name="how-to-consume-monitoring-data-from-azure-stack"></a>Jak używać danych monitorowania z usługi Azure Stack

*Dotyczy: zintegrowane systemy usługi Azure Stack*

Możesz znaleźć dane monitorowania w jednym miejscu za pomocą potoku usługi Azure Monitor, po prostu, takich jak Azure Monitor globalnej platformy Azure. Ale nie wszystkie dane monitorowania znalezionym na platformie Azure globalne są dostępne w usłudze Azure Stack. Ten artykuł zawiera podsumowanie różnych sposobów, aby programowo może pozyskiwać dane monitorowania z usługi.
 
## <a name="options-for-data-consumption"></a>Opcje do użycia danych

| Typ danych | Kategoria | Obsługiwane usługi | Metod dostępu |
|-------------------------------------------------------------|----------|------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------|
| Metryki platformy poziomu usługi Azure Monitor | Metryki | [Obsługiwane metryki z usługą Azure Monitor w usłudze Azure Stack](azure-stack-metrics-supported.md) | Interfejs API REST |
| Obliczenia metryk systemu operacyjnego gościa (na przykład, licznik wydajności) | Metryki | Windows i maszyn wirtualnych systemu Linux | Tabela magazynu lub obiektów blob:<br>Windows lub Diagnostyka Azure dla systemu Linux <br>Centrum zdarzeń:<br>Diagnostyka Azure dla systemu Windows |
| Metryki magazynu | Metryki | Azure Storage | Tabela magazynu:<br>Analityka magazynu |
| Dziennik aktywności | Zdarzenia | Wszystkich usług platformy Azure | INTERFEJS API REST:<br>Usługa Azure Monitor zdarzenia interfejsu API |
| Obliczenia dzienników systemu operacyjnego gościa (na przykład dzienniki usług IIS, ETW SYSLOG) | Zdarzenia | Windows i maszyn wirtualnych systemu Linux | Tabela magazynu lub obiektów blob:<br>Windows lub Diagnostyka Azure dla systemu Linux <br>Centrum zdarzeń:<br>Diagnostyka Azure dla systemu Windows |
| Dzienniki magazynu | Zdarzenia | Azure Storage | Tabela magazynu:<br>Analityka magazynu |

## <a name="next-steps"></a>Kolejne kroki

Dowiedz się więcej o [Azure monitorowanie w usłudze Azure Stack](azure-stack-metrics-azure-data.md).
