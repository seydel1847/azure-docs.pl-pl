---
author: vladvino
ms.service: api-management
ms.topic: include
ms.date: 11/09/2018
ms.author: vlvinogr
ms.openlocfilehash: 2bfa356deeede1c16bd5a464ea7081132a67faf6
ms.sourcegitcommit: 6b7c8b44361e87d18dba8af2da306666c41b9396
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/12/2018
ms.locfileid: "51572477"
---
## <a name="append-other-apis"></a>Dołączanie innych interfejsów API

Interfejs API może składać się z interfejsów API udostępnianych przez różne usługi, w tym specyfikację interfejsu OpenAPI, interfejs API protokołu SOAP, funkcję API Apps usługi Azure App Service, aplikację funkcji platformy Azure, usługę Azure Logic Apps i usługę Azure Service Fabric.

![Importowanie interfejsu API](./media/api-management-append-apis/import.png)

Aby dołączyć inny interfejs API do istniejących interfejsów API, wykonaj następujące kroki. Po zaimportowaniu innego interfejsu API operacje są dołączane do bieżącego interfejsu API.

1. Przejdź do wystąpienia usługi Azure API Management w witrynie Azure Portal.
2. Wybierz pozycję **Interfejsy API** z menu po lewej stronie.
3. Kliknij przycisk **...** obok interfejsu API, który chcesz dołączyć do innego interfejsu API.
4. Z menu rozwijanego wybierz pozycję **Importuj**.
5. Wybierz usługę, z której chcesz zaimportować interfejs API.