---
title: Plik dyrektywy include
description: Plik dyrektywy include
services: load balancer
author: KumudD
ms.service: load-balancer
ms.topic: include
ms.date: 01/09/2018
ms.author: kumud
ms.custom: include file
ms.openlocfilehash: c4989016d31880e1c1990c0eb46091c8f50018bc
ms.sourcegitcommit: d4f728095cf52b109b3117be9059809c12b69e32
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/10/2019
ms.locfileid: "54211884"
---
| | Standardowy SKU | Podstawowy SKU |
| --- | --- | --- |
| Rozmiar puli zaplecza | Obsługuje do 1000 wystąpień. | Obsługuje do 100 wystąpień. |
| Punkty końcowe puli zaplecza | Każda maszyna wirtualna w jednej sieci wirtualnej, w tym połączenie maszyn wirtualnych, zestawów dostępności i zestawów skalowania maszyn wirtualnych. | Maszyny wirtualne w jednym zestawie dostępności lub zestaw skalowania maszyn wirtualnych. |
| [Sondy kondycji](../articles/load-balancer/load-balancer-custom-probe-overview.md#types) | TCP, HTTP, HTTPS | TCP, HTTP |
| [Zachowanie sondy kondycji podczas niepowodzenia](../articles/load-balancer/load-balancer-custom-probe-overview.md#probedown) | Połączenia TCP pozostają aktywne na niedziałającej sondzie wystąpienia __i__ na wszystkich niedziałających sondach. | Połączenia TCP pozostają aktywne na niedziałającej sondzie wystąpienia. Wszystkie połączenia TCP są przerywane, jeśli nie działają wszystkie sondy. |
| Strefy dostępności | W jednostce SKU w warstwie Standardowa, strefowo nadmiarowych i strefowych frontonach dla ruchu przychodzącego i wychodzącego, awaria strefy przetrwania mapowania przepływów wychodzących, równoważenie obciążenia między strefami. | Niedostępne. |
| Diagnostyka | Usługa Azure Monitor, metryki wielowymiarowe obejmujące liczniki bajtów i pakietów, stan sondy kondycji, próby nawiązania połączenia (TCP SYN), kondycja połączenia wychodzącego (udane i nieudane przepływy SNAT), aktywne pomiary płaszczyzny danych | Usługa Azure Log Analytics tylko dla publicznej usługi Load Balancer, alert wyczerpania SNAT, liczba kondycji puli zaplecza. |
| Porty wysokiej dostępności | Wewnętrzny moduł równoważenia obciążenia | Niedostępne. |
| Zabezpieczenie domyślne | Publiczny adres IP, publiczne punkty końcowe usługi Load Balancer i wewnętrzne punkty końcowe usługi Load Balancer są zamknięte dla przepływów przychodzących, chyba że zostaną dodane do listy dozwolonych przez sieciową grupę zabezpieczeń. | Domyślnie otwarte, opcjonalnie sieciowa grupa zabezpieczeń. |
| [Połączenia wychodzące](../articles/load-balancer/load-balancer-outbound-connections.md) | Można jawnie zdefiniować oparty na puli translator adresów sieciowych ruchu wychodzącego za pomocą [reguł ruchu wychodzącego](../articles/load-balancer/load-balancer-outbound-rules-overview.md). Można użyć wielu frontonów z regułą rezygnacji na moduł równoważenia obciążenia. Scenariusz ruchu wychodzącego _musi_ być utworzony jawnie, aby maszyna wirtualna, zestaw dostępności lub zestaw skalowania maszyn wirtualnych mógł używać łączności wychodzącej.  Dostęp do punktów końcowych usługi Virtual Network Service można uzyskać bez definiowania łączności wychodzącej i nie wlicza się on w przetworzone dane.  Dostęp do wszystkich publicznych adresów IP, łącznie z usługami PaaS platformy Azure, które nie są dostępne jako punkty końcowe usługi sieci wirtualnej, musi być uzyskiwany za pośrednictwem łączności wychodzącej i wlicza się w przetworzone dane. Kiedy maszyna wirtualna, zestaw dostępności lub zestaw skalowania maszyn wirtualnych jest obsługiwana tylko przez wewnętrzną usługę Load Balancer, połączenia wychodzące przy użyciu domyślnej translacji adresów sieciowych źródła (SNAT) nie są dostępne; w zamian należy użyć [reguł dla ruchu wychodzącego](../articles/load-balancer/load-balancer-outbound-rules-overview.md). Programowanie SNAT dla ruchu wychodzącego jest specyficzne dla protokołu transportu na podstawie protokołu reguły równoważenia obciążenia ruchu przychodzącego. | Pojedynczy fronton wybrany losowo, jeśli obecnych jest wiele frontonów.  Kiedy maszyna wirtualna, zestaw dostępności lub zestaw skalowania maszyn wirtualnych jest obsługiwany tylko przez wewnętrzną usługę Load Balancer, używana jest domyślna translacja adresów sieciowych źródła. |
| [Reguły ruchu wychodzącego](../articles/load-balancer/load-balancer-outbound-rules-overview.md) | Deklaratywna konfiguracja translatora adresów sieciowych ruchu wychodzącego przy użyciu publicznych adresów IP lub prefiksów publicznych adresów IP lub jednych i drugich, konfigurowalny limit czasu bezczynności ruchu wychodzącego, niestandardowa alokacja portów SNAT | Niedostępne. |
|  [Resetowanie protokołu TCP w wyniku bezczynności](../articles/load-balancer/load-balancer-tcp-reset.md) | Włączanie resetowania protokołu TCP (TCP RST) w wyniku upływu limitu czasu bezczynności dla dowolnej reguły | Niedostępne |
| [Wiele frontonów](../articles/load-balancer/load-balancer-multivip-overview.md) | Ruch przychodzący i [wychodzący](../articles/load-balancer/load-balancer-outbound-connections.md) | Tylko ruch przychodzący |
| Operacje zarządzania | Większość operacji < 30 sekund | Na ogół 60–90 sekund lub więcej. |
| Umowa SLA | 99,99% dla ścieżki danych z dwoma maszynami wirtualnymi w dobrej kondycji. | Nie dotyczy. | 
| Cennik | Rozliczane na podstawie liczby reguł, przetworzonych dane przychodzących i wychodzących skojarzonych z zasobem.  | Bez opłat. |
|  |  |  |
