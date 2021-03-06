---
title: Zaawansowane zadania dotyczące oceny usługi Azure Stack | Dokumentacja firmy Microsoft
description: W tym artykule opisano zaawansowane zadania dotyczące oceny usługi Azure Stack.
services: azure-stack
documentationcenter: ''
author: jeffgilb
manager: femila
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/16/2018
ms.author: jeffgilb
ms.reviewer: misainat
ms.openlocfilehash: 185c4685de0c889c3b6e7b173445546ed5b7d921
ms.sourcegitcommit: 5d837a7557363424e0183d5f04dcb23a8ff966bb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/06/2018
ms.locfileid: "52955416"
---
# <a name="advanced-azure-stack-development-kit-evaluation-tasks"></a>Zaawansowane zadania dotyczące oceny usługi Azure Stack Development Kit
Po weszły znasz podstawowe funkcje usługi Azure Stack Development Kit (ASDK) i możliwości, można także dogłębnie zrozumieć usługi Azure Stack dodatkowo, w celu przetestowania bardziej zaawansowanych scenariuszy. Te bardziej zaawansowane zadania dotyczące oceny są w pełni udokumentowane w artykule w dokumentacji usługi Azure Stack operatora.

> [!NOTE]
> Wiele zadań operator są obsługiwane zarówno w ASDK, jak i w środowisku produkcyjnym, wdrożeniach z wieloma węzłami usługi Azure Stack, nie wszystkie scenariusze użycia są obsługiwane dla wdrożeń ASDK. Zobacz [ASDK i różnice w usłudze Azure Stack wielowęzłowego](asdk-what-is.md#asdk-and-multi-node-azure-stack-differences) Aby uzyskać więcej informacji.

## <a name="delegate-offers-in-azure-stack"></a>Delegowanie ofert w usłudze Azure Stack
Jako operatora usługi Azure Stack często ma być umieszczony innym osobom odpowiedzialnym za tworzenie oferty i rejestracji użytkowników. Na przykład jeśli jesteś dostawcą usługi, możesz zechcieć odsprzedawców, aby zarejestrować się klientów i zarządzanie nimi w Twoim imieniu. Jeśli jesteś częścią centralna grupa IT w przedsiębiorstwie, można też zależnych, aby tworzyć konta użytkowników bez interwencji użytkownika.

[Delegowanie oferty w usłudze Azure Stack](../azure-stack-delegated-provider.md) ułatwia te zadania, dzięki czemu można dotrzeć do użytkowników i zarządzać nimi więcej niż bezpośrednio.

## <a name="make-sql-databases-available-to-your-azure-stack-users"></a>Udostępnij baz danych SQL dla użytkowników usługi Azure Stack
Operator usługi Azure Stack, można utworzyć oferty, które pozwalają użytkownikom (dzierżawcy) Tworzenie baz danych SQL, których mogą używać ich natywnych aplikacji w chmurze, witryn sieci Web i obciążeń. Dostarczając użytkownikom tych baz danych niestandardowych, na żądanie, oparte na chmurze, można zapisać ich czas i zasoby.

Użyj karty dostawcy zasobów programu SQL Server do [udostępnić baz danych SQL dla użytkowników usługi Azure Stack](../azure-stack-tutorial-sql-server.md) jako usługi Azure Stack. Po zainstalowaniu dostawcy zasobów podłącz je do jednego lub większej liczby wystąpień programu SQL Server.

## <a name="make-web-and-api-apps-available-to-your-azure-stack-users"></a>Udostępnij aplikacji interfejsu API sieci web i użytkownicy usługi Azure Stack
Operator usługi Azure Stack, można utworzyć oferty, które pozwalają użytkownikom (dzierżawcy) tworzenie aplikacji usługi Azure Functions i sieci web i interfejsów API. Zapewniając użytkownikom dostęp do tych aplikacji na żądanie, oparte na chmurze, możesz je oszczędność czasu i zasobów.

Wdrażanie dostawcy zasobów usługi App Service, aby [udostępnić w sieci web i aplikacje interfejsu API użytkowników usługi Azure Stack](../azure-stack-tutorial-app-service.md)

## <a name="next-steps"></a>Kolejne kroki

[Dowiedz się więcej o oferty usług przy użyciu systemów zintegrowanych w usłudze Azure Stack](../azure-stack-offer-services-overview.md)
