---
title: Wysoka dostępność — sprzętowego modułu zabezpieczeń platformy Azure w wersji dedykowanej | Dokumentacja firmy Microsoft
description: Przykład wysokiej dostępności w usłudze Azure w wersji dedykowanej przez moduł HSM i podstawowe zagadnienia
services: dedicated-hsm
author: barclayn
manager: mbaldwin
ms.custom: mvc, seodec18
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 12/07/2018
ms.author: barclayn
ms.openlocfilehash: 991482d3d6be4d09b37014e5bb03708987e0f74e
ms.sourcegitcommit: 9fb6f44dbdaf9002ac4f411781bf1bd25c191e26
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/08/2018
ms.locfileid: "53078178"
---
# <a name="azure-dedicated-hsm-high-availability"></a>Platformy Azure w wersji dedykowanej HSM wysokiej dostępności.

Azure w wersji dedykowanej przez sprzętowy moduł zabezpieczeń jest wspierane przez firmy Microsoft o wysokiej dostępności w centrach danych. Jednak wszelkie wysoce dostępnego centrum danych jest narażony na zlokalizowanymi awariami i w ekstremalnych przypadkach regionalnymi awariami poziomu. Firma Microsoft wdraża urządzenia sprzętowego modułu zabezpieczeń w różnych centrach danych w danym regionie, aby upewnić się, że inicjowanie obsługi administracyjnej wielu urządzeń nie prowadzi do tych urządzeń do udostępniania jednym stojaku. Dodatkowego poziomu wysoką dostępność można osiągnąć, łącząc te moduły HSM w centrach danych w regionie. Istnieje również możliwość parę urządzeń regionach adresu regionalnej pracy awaryjnej w sytuacji odzyskiwania po awarii. W przypadku tej konfiguracji wielowarstwowych wysokiej dostępności jakiekolwiek niepowodzenie urządzenia zostanie automatycznie rozwiązany do zachowania aplikacji. Wszystkie centra danych również miały wolnym urządzenia i składniki na miejscu, dzięki czemu można zastąpić dowolnego urządzenia nie powiodło się w odpowiednim czasie.

## <a name="high-availability-example"></a>Przykład wysokiej dostępności

Informacji na temat sposobu konfigurowania urządzeń przez moduł HSM w celu zapewnienia wysokiej dostępności na poziomie oprogramowania znajduje się w "Firmy Gemalto Luna sieciowych przez moduł HSM podręczniku administratora". W tym dokumencie jest dostępny w [Portal obsługi klienta firmy Gemalto](https://supportportal.gemalto.com/csm/).

Na poniższym diagramie przedstawiono architekturę wysokiej dostępności. Korzysta ona z wielu urządzeń w regionie i wiele urządzeń sparowane w osobnym regionie. Ta architektura używa co najmniej cztery urządzenia HSM i składniki sieci wirtualnej.

![Diagram wysokiej dostępności](media/high-availability/high-availability.png)

## <a name="next-steps"></a>Kolejne kroki

Zalecane jest, wszystkie najważniejsze pojęcia związane z usługi, takie jak wysoka dostępność i bezpieczeństwo, są dobrze zrozumiałe przed Inicjowanie obsługi administracyjnej urządzeń i projektu aplikacji lub wdrożenia.
Dodatkowe tematy poziomu pojęcia:

* [Architektura wdrożenia](deployment-architecture.md)
* [Zabezpieczenia fizyczne](physical-security.md)
* [Sieć](networking.md)
* [Możliwości obsługi](supportability.md)
* [Monitorowanie](monitoring.md)

Aby uzyskać szczegółowe informacje na temat konfigurowania urządzenia HSM wysokiej dostępności można znaleźć Portal obsługi klienta firmy Gemalto przewodniki administratora i sekcja 6.
