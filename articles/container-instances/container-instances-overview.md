---
title: Co to jest usługa Azure Container Instances?
description: Usługa Azure Container Instances to najszybszy i najprostszy sposób uruchamiania wyizolowanych kontenerów na platformie Azure, bez konieczności zarządzania jakimikolwiek maszynami wirtualnymi ani korzystania z orkiestratora wyższego poziomu.
services: container-instances
author: seanmck
manager: jeconnoc
ms.service: container-instances
ms.topic: overview
ms.date: 11/30/2018
ms.author: seanmck
ms.custom: seodec18, mvc
ms.openlocfilehash: ba454965ff2bb78ebe526e71d9280200b1f4b08b
ms.sourcegitcommit: 5b869779fb99d51c1c288bc7122429a3d22a0363
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/10/2018
ms.locfileid: "53187198"
---
# <a name="what-is-azure-container-instances"></a>Co to jest usługa Azure Container Instances?

Kontenery stają się preferowanym sposobem tworzenia pakietów aplikacji w chmurze, ich wdrażania oraz zarządzania nimi. Usługa Azure Container Instances to najszybszy i najprostszy sposób uruchomienia kontenera na platformie Azure, bez konieczności zarządzania jakimikolwiek maszynami wirtualnymi ani korzystania z usługi wyższego poziomu.

Usługa Azure Container Instances to doskonałe rozwiązanie dla wszystkich scenariuszy, które może działać w kontenerach izolowanych, w tym w przypadku prostych aplikacji, automatyzacji zadań i zadań kompilacji. W przypadku scenariuszy, w których potrzebujesz pełnej orkiestracji kontenerów, w tym opcji odnajdowania usług w wielu kontenerach, automatycznego skalowania i skoordynowanych uaktualnień aplikacji, zalecamy skorzystanie z usługi [Azure Kubernetes Service](../aks/index.yml) (AKS).

## <a name="fast-startup-times"></a>Krótki czas uruchamiania

Kontenery oferują znaczące korzyści związane z uruchamianiem w porównaniu do maszyn wirtualnych. Usługa Azure Container Instances umożliwia uruchamianie kontenera na platformie Azure w ciągu kilku sekund bez konieczności aprowizowania maszyn wirtualnych i zarządzania nimi.

## <a name="public-ip-connectivity-and-dns-name"></a>Łączność przy użyciu publicznych adresów IP i nazwa DNS

Usługa Azure Container Instances umożliwia uwidacznianie kontenerów bezpośrednio w Internecie za pomocą adresu IP i w pełni kwalifikowanej nazwy domeny (FQDN, fully qualified domain name). Podczas tworzenia wystąpienia kontenera możesz określić niestandardową etykietę nazwy DNS, dzięki czemu aplikacja będzie dostępna pod adresem *etykieta_niestandardowa*.*region_świadczenia_usługi_Azure*.azurecontainer.io.

## <a name="hypervisor-level-security"></a>Zabezpieczenia na poziomie funkcji hypervisor

W przeszłości kontenery oferowały zarządzanie zasobami i izolację zależności aplikacji, ale nie były wystarczająco odporne na użycie wielu obcych dzierżaw. Usługa Azure Container Instances gwarantuje, że aplikacja jest izolowana w kontenerze w takim samym stopniu, w jakim byłaby na maszynie wirtualnej.

## <a name="custom-sizes"></a>Rozmiary niestandardowe

Kontenery są przeważnie optymalizowane do uruchamiania tylko jednej aplikacji, ale szczegółowe potrzeby poszczególnych aplikacji mogą się bardzo różnić. Usługa Azure Container Instances zapewnia optymalne wykorzystanie, zezwalając na korzystanie z dokładnych specyfikacji rdzeni procesora i pamięci. Opłaty są naliczane zgodnie z zapotrzebowaniem i za sekundę, dlatego można skutecznie dostosować wydatki w oparciu o potrzeby.

W przypadku zadań wykorzystujących znaczną moc obliczeniową, takich jak uczenie maszynowe, usługa Azure Container Instances może zaplanować używanie [zasobów procesorów GPU](container-instances-gpu.md) NVIDIA Tesla (wersja zapoznawcza) przez kontenery systemu Linux.

## <a name="persistent-storage"></a>Magazyn trwały

Aby umożliwić pobieranie i utrwalanie stanu przy użyciu usługi Azure Container Instances, firma Microsoft oferuje bezpośrednie [instalowanie udziałów usługi Azure Files](container-instances-mounting-azure-files-volume.md).

## <a name="linux-and-windows-containers"></a>Kontenery systemów Linux i Windows

Usługa Azure Container Instances umożliwia planowanie kontenerów systemów Windows i Linux przy użyciu tego samego interfejsu API. Podczas tworzenia [grup kontenerów](container-instances-container-groups.md) po prostu określ typ systemu operacyjnego.

Niektóre funkcje są obecnie ograniczone do kontenerów systemu Linux. Podczas gdy pracujemy, aby udostępnić równoważność funkcji na potrzeby kontenerów systemu Windows, bieżące różnice dotyczące platform możesz znaleźć w temacie [Limity przydziałów i dostępność regionów dla usługi Azure Container Instances](container-instances-quotas.md).

Usługa Azure Container Instances obsługuje obrazy systemu Windows na podstawie wersji kanału Long-Term Servicing Channel (LTSC). Obrazy systemu Windows z wersjami kanału Semi-Annual Channel (SAC), takimi jak 1709 i 1803, nie są obsługiwane.

## <a name="co-scheduled-groups"></a>Grupy planowane wspólnie

Usługa Azure Container Instances obsługuje planowanie [grup wielu kontenerów](container-instances-container-groups.md), które współużytkują maszynę hosta, sieć lokalną, magazyn i cykl życia. Dzięki temu można łączyć główny kontener aplikacji z innymi kontenerami pełniącymi rolę pomocniczą, np. przyczepkami rejestrowania.

## <a name="virtual-network-deployment-preview"></a>Wdrażanie sieci wirtualnej (wersja zapoznawcza)

Ta funkcja usługi Azure Container Instances (obecnie dostępna w wersji zapoznawczej) umożliwia [wdrażanie wystąpień kontenerów w sieci wirtualnej platformy Azure](container-instances-vnet.md). Wdrożenie wystąpień kontenerów w podsieci w sieci wirtualnej umożliwia bezpieczną komunikację z innymi zasobami w sieci wirtualnej, w tym z zasobami lokalnymi (przy użyciu [bramy sieci VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md) lub [usługi ExpressRoute](../expressroute/expressroute-introduction.md)).

> [!IMPORTANT]
> Niektóre funkcje usługi Azure Container Instances są w wersji zapoznawczej i [obowiązują pewne ograniczenia](container-instances-vnet.md#preview-limitations). Wersje zapoznawcze są udostępniane pod warunkiem udzielenia zgody na [dodatkowe warunki użytkowania][terms-of-use]. Niektóre cechy tych funkcji mogą ulec zmianie, zanim stanie się ona ogólnie dostępna.

## <a name="next-steps"></a>Następne kroki

Spróbuj wdrożyć kontener na platformie Azure za pomocą jednego polecenia, korzystając z naszego przewodnika Szybki start:

> [!div class="nextstepaction"]
> [Azure Container Instances — Szybki start](container-instances-quickstart.md)

<!-- LINKS - External -->
[terms-of-use]: https://azure.microsoft.com/support/legal/preview-supplemental-terms/
