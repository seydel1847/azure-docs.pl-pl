---
title: Usługa Azure Advisor zaleceń dotyczących wysokiej dostępności | Dokumentacja firmy Microsoft
description: Użyj usługi Azure Advisor, aby poprawić wysoką dostępność wdrożeń platformy Azure.
services: advisor
documentationcenter: NA
author: kasparks
manager: carmonm
editor: ''
ms.assetid: ''
ms.service: advisor
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kasparks
ms.openlocfilehash: 928fb5421297fedbffabc45db35a89a74026477e
ms.sourcegitcommit: 70471c4febc7835e643207420e515b6436235d29
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/15/2019
ms.locfileid: "54305075"
---
# <a name="advisor-high-availability-recommendations"></a>Zalecenia dotyczące wysokiej dostępności usługi Advisor

Usługa Azure Advisor ułatwia upewnij się, a ciągłość aplikacje krytyczne dla prowadzonej działalności. Można uzyskać zaleceń dotyczących wysokiej dostępności przez usługę Advisor z **wysokiej dostępności** karty Pulpit nawigacyjny usługi Advisor.

## <a name="ensure-virtual-machine-fault-tolerance"></a>Upewnij się, odporność na uszkodzenia maszyny wirtualnej

Aby zapewnić nadmiarowość aplikacji, zalecamy grupowanie co najmniej dwóch maszyn wirtualnych w zestawie dostępności. Klasyfikator identyfikuje maszyny wirtualne, które nie są częścią zestawu dostępności i zaleca przenoszenia ich do zestawu dostępności. Ta konfiguracja gwarantuje, że podczas każdej planowanego lub nieplanowanego zdarzenia konserwacji, co najmniej jedna maszyna wirtualna jest dostępna i spełnia warunki umowy SLA maszyn wirtualnych platformy Azure. Można wybrać, aby utworzyć zestaw dostępności dla maszyny wirtualnej lub Dodaj maszynę wirtualną do istniejącego zestawu dostępności.

> [!NOTE]
> Jeśli zdecydujesz się utworzyć zestaw dostępności, należy dodać co najmniej jedną maszynę wirtualną do niego. Firma Microsoft zaleca tego należy co najmniej dwóch maszyn wirtualnych w dostępności zestawu grup aby upewnić się, że co najmniej jedna maszyna jest dostępny podczas awarii.

## <a name="ensure-availability-set-fault-tolerance"></a>Upewnij się, że zestaw dostępności, odporności na uszkodzenia 

Aby zapewnić nadmiarowość aplikacji, zalecamy grupowanie co najmniej dwóch maszyn wirtualnych w zestawie dostępności. Advisor ustala zestawów dostępności, które zawierają pojedynczą maszynę wirtualną i zaleca dodanie co najmniej jednej maszyny wirtualnej do niego. Ta konfiguracja gwarantuje, że podczas każdej planowanego lub nieplanowanego zdarzenia konserwacji, co najmniej jedna maszyna wirtualna jest dostępna i spełnia warunki umowy SLA maszyn wirtualnych platformy Azure. Możesz wybrać do utworzenia maszyny wirtualnej, lub można dodać istniejącej maszyny wirtualnej do zestawu dostępności.  

## <a name="use-managed-disks-to-improve-data-reliability"></a>Skorzystaj z usługi Managed Disks, aby zwiększyć niezawodność danych
Maszyny wirtualne, które znajdują się w zestaw dostępności z dyskami współużytkującymi konta magazynu lub jednostki skali magazynu nie są odporne na błędy jednostki skali magazynu jednego podczas awarii. Klasyfikator zidentyfikuje te zestawy dostępności i zaleca się migrację do usługi Azure Managed Disks. Pozwoli to zagwarantować, że dyski różnych maszyn wirtualnych w zestawie dostępności są wystarczająco izolowane pod kątem uniknięcia pojedynczego punktu awarii. 

## <a name="ensure-application-gateway-fault-tolerance"></a>Upewnij się, odporność na uszkodzenia bramy aplikacji

W celu zapewnienia ciągłości biznesowej aplikacji o kluczowym znaczeniu, które są obsługiwane przez bramy application Gateway Advisor identyfikuje wystąpienia bramy aplikacji, które nie są skonfigurowane dla odporności na uszkodzenia i sugerują one akcji korygowania, które należy wykonać. Klasyfikator identyfikuje średnich i dużych aplikacja o pojedynczym wystąpieniu bramy i zaleca się dodanie co najmniej jedno wystąpienie więcej. Ponadto identyfikuje instance jednego lub wielu małych bramach aplikacji i zaleca się migrację do średnich i dużych jednostek SKU. Klasyfikator zaleca tych akcji, aby upewnić się, że Twoje wystąpienia bramy aplikacji są skonfigurowane do spełnić bieżące wymagania umowy SLA dla tych zasobów.

## <a name="protect-your-virtual-machine-data-from-accidental-deletion"></a>Chronić dane maszyny wirtualnej przed przypadkowym usunięciem

Konfigurowanie kopii zapasowej maszyny wirtualnej zapewnia dostępność danych krytyczne dla prowadzonej działalności i zapewnia ochronę przed przypadkowym uszkodzeniem lub usunięciem. Klasyfikator identyfikuje maszyny wirtualne, których kopia zapasowa nie jest włączona i zaleca się włączenie kopii zapasowej. 

## <a name="ensure-you-have-access-to-azure-cloud-experts-when-you-need-it"></a>Upewnij się, że masz dostęp do ekspertów ds. chmury platformy Azure, gdy jej potrzebujesz

Podczas uruchamiania obciążenia krytyczne dla prowadzonej działalności, należy mieć dostęp do pomocy technicznej potrzebnych. Klasyfikator identyfikuje potencjalne krytyczne dla prowadzonej działalności subskrypcje, które nie mają pomocy technicznej uwzględnione w ich plan pomocy technicznej i zaleca się uaktualnienie do opcja, która obejmuje pomoc techniczną.

## <a name="create-azure-service-health-alerts-to-be-notified-when-azure-issues-affect-you"></a>Tworzenie alertów usługi Azure Service Health, aby otrzymywać powiadomienia, gdy napotkasz problemy z platformy Azure

Firma Microsoft zaleca skonfigurowanie alerty dotyczące kondycji usługi platformy Azure, aby otrzymywać powiadomienia, gdy napotkasz problemy z usługą Azure. [Usługa Azure Service Health](https://azure.microsoft.com/features/service-health/) to bezpłatna usługa, która zapewnia spersonalizowane wskazówki i pomoc techniczna, gdy mają wpływ problemu usługi platformy Azure. Advisor ustala subskrypcje, które nie mają skonfigurowano alertów i zaleca się tworzenie katalogu.

## <a name="configure-traffic-manager-endpoints-for-resiliency"></a>Skonfiguruj punkty końcowe usługi Traffic Manager w celu zapewnienia odporności

Profile usługi Traffic Manager z więcej niż jednym punktem końcowym środowiska wyższą dostępność, jeśli dowolnego danego punktu końcowego nie powiedzie się. Wprowadzenie do punktów końcowych w różnych regionach dalsze zwiększa niezawodność usług. Advisor identyfikuje profile Menedżer ruchu, gdy istnieje tylko jeden punkt końcowy i zaleca dodanie co najmniej jeden punkt końcowy więcej w innym regionie.

W przypadku wszystkich punktów końcowych w profilu usługi Traffic Manager, który jest skonfigurowany dla routingu odległości między elementami w tym samym regionie, użytkownicy z innych regionów, mogą wystąpić opóźnienia w połączeniu. Dodanie lub usunięcie punktu końcowego w innym regionie spowoduje zwiększenia ogólnej wydajności i zapewnienie wyższej dostępności, jeśli wszystkie punkty końcowe w jednym regionie nie powiedzie się. Advisor ustala profile usługi Traffic Manager skonfigurowany dla odległości routingu, gdy wszystkie punkty końcowe są w tym samym regionie i zaleca się dodanie lub usunięcie punktu końcowego w innym regionie platformy Azure.

Jeśli profil usługi Traffic Manager jest skonfigurowany dla geograficznego routingu, ruch jest kierowany do punktów końcowych na podstawie określonych regionów. Region nie powiedzie się, czy wstępnie zdefiniowane trybu failover. O punkt końcowy, w której grupowanie regionalne jest skonfigurowana pod kątem "Wszystkie (World)" uniknąć ruchu sieciowego pomijanego i zwiększyć dostępność usług. Klasyfikator identyfikuje skonfigurowano geograficznego routingu, gdy nie ma punktu końcowego skonfigurowaną grupowanie regionalne jako "Wszystkie (World)" i zaleca zastosowanie tej zmiany konfiguracji profilów usługi Traffic Manager.

## <a name="use-soft-delete-on-your-azure-storage-account-to-save-and-recover-data-in-the-event-of-accidental-overwrite-or-deletion"></a>Użyj nietrwałego usuwania na swoim koncie magazynu platformy Azure, aby zapisać i odzyskiwanie danych w razie przypadkowego zastępowania lub usuwania

Włącz [usuwania nietrwałego](https://docs.microsoft.com/azure/storage/blobs/storage-blob-soft-delete) na swoim koncie magazynu, aby usunąć obiekty BLOB przejście do stanu usunięcia nietrwałego zamiast trwale usunięte. Gdy dane są zastępowane, nietrwałe Usunięto migawkę jest generowany ma być zapisany stan zastąpione danych. To umożliwia odzyskanie danych w razie przypadkowego usunięcia lub zastąpienie. Advisor ustala kontach magazynu Azure, które nie mają włączone usuwanie nietrwałe i sugeruje, że można ją włączyć.

## <a name="configure-your-vpn-gateway-to-active-active-for-connection-resiliency"></a>Konfigurowanie bramy sieci VPN w taki sposób, aby aktywne aktywne dla połączeń

W konfiguracji aktywne aktywne oba wystąpienia bramy sieci VPN ustanowią tunele S2S sieci VPN do urządzenia sieci VPN w środowisku lokalnym. Sytuacji zdarzenie planowanej konserwacji lub nieplanowanego zdarzenia dotyczącego jednego wystąpienia bramy ruchu umożliwić przełączenie do innego aktywnego tunelu IPsec automatycznie. Usługa Azure Advisor zidentyfikuje bram sieci VPN, które nie są skonfigurowane jako aktywny aktywny i sugeruje, że można je skonfigurować wysoką dostępność.

## <a name="how-to-access-high-availability-recommendations-in-advisor"></a>Jak uzyskać dostęp do zaleceń dotyczących wysokiej dostępności w programie Advisor

1. Zaloguj się do [witryny Azure portal](https://portal.azure.com), a następnie otwórz [Advisor](https://aka.ms/azureadvisordashboard).

2.  Na pulpicie nawigacyjnym usługi Advisor kliknij **wysokiej dostępności** kartę.

## <a name="next-steps"></a>Kolejne kroki

Aby uzyskać więcej informacji na temat zalecenia usługi Advisor zobacz:
* [Wprowadzenie do usługi Azure Advisor](advisor-overview.md)
* [Wprowadzenie do usługi Advisor](advisor-get-started.md)
* [Rekomendacji dotyczących kosztu usługi Advisor](advisor-cost-recommendations.md)
* [Zalecenia dotyczące wydajności usługi Advisor](advisor-performance-recommendations.md)
* [Zalecenia dotyczące zabezpieczeń usługi Advisor](advisor-security-recommendations.md)

