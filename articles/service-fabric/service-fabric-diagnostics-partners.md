---
title: Usługa Azure Service Fabric monitorowania partnerów | Dokumentacja firmy Microsoft
description: Dowiedz się, jak monitorować usługi Azure Service Fabric za pomocą monitorowanie rozwiązań partnerskich
services: service-fabric
documentationcenter: .net
author: srrengar
manager: timlt
editor: ''
ms.assetid: ''
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 10/16/2018
ms.author: srrengar
ms.openlocfilehash: f7bf5d521f4bcb5672ff1d710a08bed2e0872545
ms.sourcegitcommit: 803e66de6de4a094c6ae9cde7b76f5f4b622a7bb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/02/2019
ms.locfileid: "53974407"
---
# <a name="azure-service-fabric-monitoring-partners"></a>Usługa Azure Service Fabric monitorowania partnerów

W tym artykule pokazano, jak jeden monitorować ich aplikacji usługi Service Fabric, klastrów i infrastruktury za pomocą kliku rozwiązań partnerskich. Współpracowaliśmy z każdą z partnerów wymienionych poniżej, aby utworzyć integracji ofert dla usługi Service Fabric.

## <a name="dynatrace"></a>Rozwiązania Dynatrace

Naszej integracji za pomocą rozwiązania Dynatrace zapewnia wiele poza pole funkcje do monitorowania klastrów usługi Service Fabric. Instalowanie Dynatrace OneAgent na wystąpieniach zestawu skalowania maszyn wirtualnych zapewnia liczniki wydajności i topologii wdrożenia usługi Service Fabric do poziomu aplikacji. Dynatrace również jest doskonałym wyborem dla monitorowania lokalnego. Zapoznaj się z jedną z wymienionych w funkcji [ogłoszenie](https://www.dynatrace.com/news/blog/automatic-end-to-end-service-fabric-monitoring-with-dynatrace/) i [instrukcje](https://www.dynatrace.com/news/blog/automatic-end-to-end-service-fabric-monitoring-with-dynatrace/) umożliwiające Dynatrace w klastrze. 

## <a name="datadog"></a>Pomocą usługi Datadog

Pomocą usługi Datadog ma rozszerzenie dla zestawu skalowania maszyn wirtualnych dla wystąpień systemów Windows i Linux. Przy użyciu pomocą usługi Datadog można zebrać dzienniki zdarzeń Windows i tym samym zbierania zdarzeń platformy usługi Service Fabric na Windows. Zapoznaj się z instrukcjami, w jaki sposób wysyłać dane diagnostyczne do pomocą usługi Datadog [tutaj](https://www.datadoghq.com/blog/azure-monitoring-enhancements/#integrate-with-azure-service-fabric).

## <a name="appdynamics"></a>AppDynamics

Integracja usługi Service Fabric z oprogramowaniem AppDynamics znajduje się na poziomie aplikacji. Aktualizowanie zmiennych środowiskowych i używając rozszerzeń Nuget Dynamics aplikacji, może wysyłać dane telemetryczne aplikacji do AppDynamics. Użyj tych [instrukcje](https://docs.appdynamics.com/display/AZURE/Install+AppDynamics+for+Azure+Service+Fabric) dotyczące sposobów integracji aplikacji .NET usługi Service Fabric z oprogramowaniem AppDynamics.

## <a name="new-relic"></a>New Relic

New Relic to kolejne narzędzie zarządzania wydajnością aplikacji, które dobrze integruje się z aplikacji usługi Service Fabric. Można zainstalować nowe pakiety Relic i Dodaj określonych zmiennych środowiskowych w plikach manifestu wysyłać dane telemetryczne aplikacji New Relic. Zapoznaj się z tymi [instrukcje](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/install-net-agent-azure-service-fabric) włączyć telemetrię New Relic dla aplikacji .NET usługi Service Fabric.

## <a name="elk"></a>ELK 

Stos ELK to zbiór technologie typu open source: Usługa Elasticsearch, Logstash i Kibana. Używając tych w połączeniu, można zbierać, przechowywać i analizować dane monitorowania i diagnostyki usługi Service Fabric. Mamy zapoznać się z samouczkiem jak to zrobić przy użyciu natywnych aplikacji Java usługi Service Fabric [tutaj](service-fabric-tutorial-java-elk.md). 


## <a name="next-steps"></a>Kolejne kroki

* Pobierz [omówienie monitorowania i diagnostyki](service-fabric-diagnostics-overview.md) w usłudze Service Fabric
* Dowiedz się, jak [zdiagnozować typowe scenariusze](service-fabric-diagnostics-common-scenarios.md) za pomocą naszych pierwszy narzędzi innych firm
