---
title: Dynamics 365 for Customer Engagement oferuje wstępnie wymagane składniki — portalu Azure Marketplace | Dokumentacja firmy Microsoft
description: Wymagania wstępne dotyczące publikowania aplikacji systemu Azure oferują w portalu Azure Marketplace.
services: Dynamics 365 for Customer Engagement offer, Azure, Marketplace, Cloud Partner Portal,
documentationcenter: ''
author: v-miclar
manager: Patrick.Butler
editor: ''
ms.assetid: ''
ms.service: marketplace
ms.workload: ''
ms.tgt_pltfrm: ''
ms.devlang: ''
ms.topic: conceptual
ms.date: 12/20/2018
ms.author: pbutlerm
ms.openlocfilehash: 4b4859c41e7a3903de68b62e8587f1c85805a782
ms.sourcegitcommit: fbf0124ae39fa526fc7e7768952efe32093e3591
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/08/2019
ms.locfileid: "54083036"
---
# <a name="dynamics-365-for-customer-engagement-prerequisites"></a>Dynamics 365 Customer Engagement wstępnie wymaganych składników

W tym artykule opisano wymagania wstępne techniczne i biznesowe dotyczące publikowania Dynamics 365 Customer Engagement aplikacji oferty w witrynie Marketplace usługi AppSource.


## <a name="technical-requirements"></a>Wymagania techniczne

Usługi Dynamics 365 Customer Engagement aplikacji musi być zgodna z [wytyczne przeglądu aplikacji Microsoft AppSource](https://smp-cdn-prod.azureedge.net/documents/AppsourceGuidelines/Microsoft%20AppSource%20app%20review%20guidelines_v5.pdf), która obejmuje następujące wymagania:


|              Wymaganie             |        Opis           |
|            ---------------           |      ---------------         |
| Integracja z usługą Azure Active Directory   | Aplikacja musi zezwalać na usługi Azure Active Directory federacyjnego logowania jednokrotnego (AAD Federacyjna usługa rejestracji Jednokrotnej) za zgodą włączone. Aby uzyskać więcej informacji, zobacz [sposób uzyskiwania certyfikatu AppSource dla usługi Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/howto-get-appsource-certified). |
| Integracja z usługami Microsoft Cloud (opcjonalnie) | W przypadku, gdy jest to wymagane, aplikację należy zintegrować z innych usług Microsoft Cloud, takich jak usługi Microsoft Power BI, Microsoft Flow lub Microsoft Azure, takich jak machine learning i cognitive services. |
| Line-of-business fokus            |  Aplikacji należy skupić się na proces biznesowy dobrze zdefiniowanych lub wystawiania, przede wszystkim informacje skierowane do klientów biznesowych i użytkownicy mogą zalogować się przy użyciu poświadczeń służbowych (nazwa użytkownika i hasło).  |
| Okres bezpłatnej wersji próbnej i wersja próbna |  Klient musi mieć możliwość bezpłatnego korzystania z aplikacji przez ograniczony czas: "Pobierz teraz" bezpłatnie aplikacji "bezpłatna wersja próbna" w określonym przedziale demonstrator "Wersja testowa" lub "kontakt ze mną" żądania opcji.  |
| Lub z niewielką ilością bez konfiguracji                 | Aplikacja musi być łatwo i szybko skonfigurować i skonfigurować (nie rozwoju lub dostosowanie jest wymagane).  |
| Obsługa klienta                     | Pomoc techniczna dla aplikacji mogą zawierać łącza pomocy technicznej, gdzie klienci mogą znaleźć Pomoc.  |
| Dostępność/czas pracy                  | Aplikacja musi mieć czas działania co najmniej 99,9%. |
|  |  |


## <a name="business-requirements"></a>Wymagania biznesowe

Wymagania biznesowe obejmują następujące obowiązki umowne stosowane w UE i prawne proceduralne:

* Musi być zarejestrowana we [Microsoft Partner Network (MPN)](https://partners.microsoft.com/PartnerProgram/simplifiedenrollment.aspx) lub zostać zarejestrowane wydawcy chmury w witrynie Marketplace. Jeśli nie są zarejestrowane, postępuj zgodnie z instrukcjami [stają się wydawcy w witrynie Marketplace chmury](../../become-publisher.md).  (Trzeci krok zamiast tego użyć [formularz nominacji partnera usługi AppSource](https://appsource.microsoft.com/partners/signup)). 

    >[!NOTE]
    >Zalogować się do portalu Cloud Partner, należy używać tego samego konta Microsoft Developer Center w rejestracji. Powinna mieć tylko jedno konto Microsoft, dla ofert portalu Azure Marketplace. To konto nie powinny być specyficzne dla poszczególnych usług lub oferty.

* Ponieważ usługi AppSource nie oferuje opcji publikowania z włączoną commerce, należy użyć używanych bieżącego porządkowanie i rozliczeń infrastruktury bez dodatkowej inwestycji ani zmian.
* Jesteś odpowiedzialny za wprowadzanie pomocy technicznej dostępne dla klientów w sposób rozsądny z komercyjnego punktu widzenia. Może to mieć wolne, płatną lub za pośrednictwem metody społeczności.
* Jesteś odpowiedzialny za Licencjonowanie oprogramowania oraz wszystkie zależności oprogramowania innych firm.
* Należy utworzyć skojarzone materiały marketingowe, np. nazwę aplikacji oficjalne, opis (format HTML), logo obrazy w formacie PNG (w pikselach 40 x 40, 90 x 90, 115 x 115 i 255 x 115) i warunki użytkowania i zasady zachowania poufności informacji.  


## <a name="next-steps"></a>Kolejne kroki

Po zostały spełnione następujące wymagania, możesz [Utwórz ofertę platformy Dynamics 365 Customer Engagement](./cpp-create-offer.md) 
