---
title: Omówienie usługi Service Health | Dokumentacja firmy Microsoft
description: Spersonalizowane informacje na temat aplikacji Azure wpływu problemów z obecnym i przyszłym usługi platformy Azure i konserwacji.
services: Resource health
documentationcenter: ''
author: rboucher
manager: ''
editor: ''
ms.assetid: ''
ms.service: service-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 03/27/2018
ms.author: robb
ms.openlocfilehash: aa7a925255b0c30b84c3b32bb53ba3f31c11fa6b
ms.sourcegitcommit: efcd039e5e3de3149c9de7296c57566e0f88b106
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/10/2018
ms.locfileid: "53162294"
---
# <a name="service-health"></a>Service Health
Service Health zapewnia można dostosować pulpit nawigacyjny, który śledzi kondycji usług platformy Azure w regionach, gdzie można ich użyć. Na tym pulpicie nawigacyjnym możesz śledzić aktywne wydarzenia, takich jak problemy z usługą bieżące, zbliżającej się planowanej konserwacji lub porady dotyczące kondycji odpowiednimi. Zdarzenia stają się nieaktywne, są umieszczone w historii kondycji przez 90 dni. Na koniec można użyć pulpitu nawigacyjnego kondycji usługi do tworzenia i obsługi alertów dotyczących kondycji usługi, których aktywnie informujące o problemach z usługą mają wpływ na możesz.

## <a name="service-health-events"></a>Zdarzenia usługi Service Health
Kondycja usługi śledzi trzy rodzaje zdarzenia dotyczące kondycji, które mogą mieć wpływ na Twoje zasoby:
1. **Usługa problemów** — problemy z usługami platformy Azure, wpływających teraz. 
2. **Planowana konserwacja** -nadchodzącej konserwacji, które mogą mieć wpływ na dostępność usług w przyszłości.  
3. **Porady dotyczące kondycji** -zmiany w usługach platformy Azure, które wymagają Twojej uwagi. Przykładami są przestarzałe funkcje systemu Azure lub przekraczają limit przydziału użycia.

## <a name="get-started-with-service-health"></a>Rozpoczynanie pracy z usługą Service Health
Aby uruchomić Pulpit nawigacyjny kondycji usługi, wybierz Kafelek kondycja usługi na pulpicie nawigacyjnym portalu. Jeśli została wcześniej usunięta Kafelek lub korzystania z niestandardowego pulpitu nawigacyjnego, wyszukiwania dla usługi Service Health w "Więcej usług" (dołu z lewej na pulpicie nawigacyjnym).

![Rozpoczynanie pracy z usługą Service Health](./media/service-health-overview/azure-service-health-overview-1.png)

## <a name="see-current-issues-which-impact-your-services"></a>Zobacz bieżące problemy, które mają wpływ usługi
**Usługi problemów** widok pokazuje wszystkie bieżące problemy z usługami platformy Azure, które wpływają na Twoje zasoby. Można zrozumieć, kiedy problem zaczął występować i wpływ na usługach i regionach. Można również przeczytać najnowszej aktualizacji, aby dowiedzieć się, aby rozwiązać ten problem jest działania usługi Azure. 

![Problem z usługą zarządzania](./media/service-health-overview/azure-service-health-overview-2.png)

Wybierz **potencjalny wpływ** kartę, aby zapoznać się z listą określonych zasobów jesteś właścicielem, które mogą mieć wpływ na ten problem. Możesz pobrać listę tych zasobów do udostępnienia swojemu zespołowi w pliku CSV.

![Problem z usługą - wpływ na zarządzanie](./media/service-health-overview/azure-service-health-overview-4.png)

## <a name="get-links-and-downloadable-explanations"></a>Łącza i wyjaśnienia do pobrania 
Możesz uzyskać link do problemu w celu użycia w systemie zarządzania problemami. Możesz pobrać pliki PDF i czasami plików CSV na udostępnianie osobom, które nie mają dostępu do witryny Azure portal.   

![Zarządzanie problem z usługą — Zarządzanie problemami](./media/service-health-overview/azure-service-health-overview-3.png)

## <a name="get-support-from-microsoft"></a>Uzyskaj pomoc techniczną od firmy Microsoft
Jeśli zasób jest w złym stanie nawet po usunięciu problemu, skontaktuj się z pomocą techniczną.  Użyj łącza pomocy technicznej w prawej części strony.  

## <a name="pin-a-personalized-health-map-to-your-dashboard"></a>Przypnij mapę spersonalizowane kondycji do pulpitu nawigacyjnego
Filtruj Service Health, aby wyświetlić swoje subskrypcje krytyczne dla prowadzonej działalności, regionów i typów zasobów. Zapisz filtr i Przypnij mapę świata spersonalizowane kondycji do pulpitu nawigacyjnego portalu. 

![Mapa spersonalizowane kondycji filtru](./media/service-health-overview/azure-service-health-overview-6a.png)

![Przypnij mapę spersonalizowane kondycji](./media/service-health-overview/azure-service-health-overview-6b.png)

## <a name="configure-service-health-alerts"></a>Konfigurowanie alertów dotyczących kondycji usługi
Kondycja usługi integruje się z usługą Azure Monitor w celu powiadamiania o za pośrednictwem wiadomości e-mail, wiadomości SMS i powiadomień webhook o krytyczne dla prowadzonej działalności zasobów ma wpływ. Konfigurowanie alertu dziennika aktywności dla zdarzeń kondycji odpowiednią usługę. Alert ten należy kierować do odpowiednich osób w organizacji za pomocą grup akcji. Aby uzyskać więcej informacji, zobacz [skonfigurować alerty dotyczące kondycji usługi](../azure-monitor/platform/alerts-activity-log-service-notifications.md)

# <a name="next-steps"></a>Następne kroki
Konfigurowanie alertów, dzięki czemu użytkownik jest powiadamiany o problemów z kondycją. Aby uzyskać więcej informacji, zobacz [skonfigurować alerty dotyczące kondycji usługi](../azure-monitor/platform/alerts-activity-log-service-notifications.md). 
