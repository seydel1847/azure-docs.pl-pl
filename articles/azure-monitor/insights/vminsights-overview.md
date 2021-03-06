---
title: Co to jest usługa Azure Monitor dla maszyn wirtualnych (wersja zapoznawcza)? | Microsoft Docs
description: Usługa Azure Monitor dla maszyn wirtualnych to funkcja usługi Azure monitor, który łączy kondycji i wydajności monitorowania systemu operacyjnego maszyny Wirtualnej platformy Azure, a także automatycznie odnajdywania składników aplikacji i zależności z innymi zasobami oraz mapuje komunikację między nimi. Ten artykuł zawiera omówienie.
services: azure-monitor
documentationcenter: ''
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: ''
ms.service: azure-monitor
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/07/2018
ms.author: magoedte
ms.openlocfilehash: 69aa2cbcaa6861b1d5c5c71769be2fb8046d9ea5
ms.sourcegitcommit: 5b869779fb99d51c1c288bc7122429a3d22a0363
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/10/2018
ms.locfileid: "53188517"
---
# <a name="what-is-azure-monitor-for-vms-preview"></a>Co to jest usługa Azure Monitor dla maszyn wirtualnych (wersja zapoznawcza)?

Usługa Azure Monitor dla maszyn wirtualnych monitoruje usługi Azure virtual machines (VM) i zestawy skalowania maszyn wirtualnych na dużą skalę. Usługa analizuje, wydajności i kondycji Windows i maszyn wirtualnych systemu Linux, monitorowania ich procesów i ich zależności do innych zasobów i procesy zewnętrzne. 

Rozwiązanie usługi Azure Monitor dla maszyn wirtualnych obejmuje obsługę monitorowania wydajności i aplikacji zależności dla maszyn wirtualnych, które są hostowane lokalnie lub u innego dostawcy chmury. Trzy kluczowe funkcje dostarczać dokładniejsze omówienie:

* **Logiczne składniki maszyn wirtualnych platformy Azure, który uruchamiany Windows i Linux**: Są mierzone względem kryteria kondycji wstępnie skonfigurowane, i ich wysyłania alertów, gdy ocenianą warunek jest spełniony.  

* **Wstępnie zdefiniowane, popularne wykresy wydajności**: Wyświetla podstawowe metryki wydajności z systemu operacyjnego gościa maszyny Wirtualnej.

* **Mapa zależności**: Wyświetla powiązanych elementów z maszyną Wirtualną z różnych subskrypcji i grupy zasobów.  

Funkcje są podzielone na trzy perspektyw:

* Health
* Wydajność
* Mapa

>[!NOTE]
>Obecnie funkcję kondycji jest oferowana tylko w przypadku maszyn wirtualnych platformy Azure i skalowania maszyn wirtualnych zestawów. Funkcje wydajności i mapy obsługuje zarówno w przypadku maszyn wirtualnych platformy Azure, jak i maszyny wirtualne, które są hostowane w środowisku lub innych dostawców chmury.

Integracja z usługą Log Analytics oferuje zaawansowane agregacji i filtrowania, a jego analizowanie trendów danych wraz z upływem czasu. Takie obciążenia kompleksowe monitorowanie, nie można osiągnąć za pomocą usługi Azure Monitor, Usługa Service Map lub samej usługi Log Analytics.  

Dane te można wyświetlić bezpośrednio w pojedynczej maszyny Wirtualnej z maszyny wirtualnej lub usługi Azure Monitor umożliwia dostarczanie zagregowany widok maszyn wirtualnych. Ten widok jest oparty na perspektywy każdą z tych funkcji:

* **Kondycja**: Maszyny wirtualne są powiązane z grupą zasobów.
* **Mapa** i **wydajności**: Maszyny wirtualne są skonfigurowane do raportu do określonego obszaru roboczego usługi Log Analytics.

![Maszyna wirtualna perspektywy szczegółowych informacji w witrynie Azure portal](./media/vminsights-overview/vminsights-azmon-directvm-01.png)

Azure DevOps zapewnia przewidywalną wydajność i dostępność ważnych aplikacji. Identyfikuje zdarzeń krytycznych systemu operacyjnego, wąskich gardeł wydajności i problemy z siecią. Azure DevOps może także ułatwić zrozumienie, czy problem jest związany z innych zależności.  

## <a name="data-usage"></a>Użycie danych 

Podczas wdrażania usługi Azure Monitor dla maszyn wirtualnych, danych, które są zbierane przez maszyny wirtualne jest pozyskiwane i przechowywane w usłudze Azure Monitor. Oparte na temat cen, które opublikowano na [usługi Azure Monitor stronę z cennikiem](https://azure.microsoft.com/pricing/details/monitor/), usługi Azure Monitor dla maszyn wirtualnych jest naliczana za:
* Dane pozyskiwane i przechowywane.
* Liczba kondycji kryteria metryki szeregów czasowych są monitorowane.
* Reguły alertów, które są tworzone.
* Powiadomienia, które są wysyłane. 

Rozmiar dziennika jest zależna od długości parametrów liczników i może zwiększyć liczbę dysków logicznych i karty sieciowe. Jeśli już masz obszaru roboczego i są zbierane następujące liczniki są stosowane nie podwójne naliczenie opłaty. Jeśli już korzystasz z rozwiązania Service Map, zobaczysz Jedyna zmiana jest dane dodatkowe połączenie, które są wysyłane do usługi Azure Monitor.

## <a name="next-steps"></a>Kolejne kroki
Aby poznać wymagania i metod, które pomagają monitorować maszyny wirtualne, zobacz [wdrożenia usługi Azure Monitor dla maszyn wirtualnych](vminsights-onboard.md).
