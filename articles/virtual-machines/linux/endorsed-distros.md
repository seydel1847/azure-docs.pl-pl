---
title: Dystrybucje systemu Linux zalecanych dla na platformie Azure | Dokumentacja firmy Microsoft
description: Dowiedz się więcej o systemie Linux w dystrybucjach zatwierdzone na platformie Azure, takich jak wskazówki dla Ubuntu, CentOS, Oracle i SUSE.
services: virtual-machines-linux
documentationcenter: ''
author: szarkos
manager: jeconnoc
editor: tysonn
tags: azure-service-management,azure-resource-manager
ms.assetid: 2777a526-c260-4cb9-a31a-bdfe1a55fffc
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/21/2017
ms.author: szark
ms.openlocfilehash: 3c904dadcb01dc889b159dff9ce1b9114db8103e
ms.sourcegitcommit: cd0a1514bb5300d69c626ef9984049e9d62c7237
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/30/2018
ms.locfileid: "52681810"
---
# <a name="linux-distributions-endorsed-on-azure"></a>Dystrybucje systemu Linux zalecanych dla na platformie Azure
Etap to udostępnienie obrazów systemu Linux w witrynie Azure Marketplace. Współpracujemy z wieloma społecznościami systemu Linux, aby dodać jeszcze więcej pozycji do listy dystrybucyjnej zatwierdzone. W międzyczasie dystrybucji, które nie są dostępne w portalu Marketplace, zawsze Przenoszenie własnych Linux postępując zgodnie ze wskazówkami w temacie [tworzenie i przekazywanie wirtualnego dysku twardego zawierającego system operacyjny Linux](https://docs.microsoft.com/azure/virtual-machines/linux/create-upload-generic).

## <a name="supported-distributions-and-versions"></a>Obsługiwane dystrybucje i wersje
W poniższej tabeli wymieniono dystrybucje systemu Linux i wersji, które są obsługiwane na platformie Azure. Zapoznaj się [pomocy technicznej dla obrazów systemu Linux na platformie Microsoft Azure](https://support.microsoft.com/help/2941892/support-for-linux-and-open-source-technology-in-azure) Aby uzyskać szczegółowe informacje dotyczące pomocy technicznej dla systemu Linux i technologii typu open source na platformie Azure.

Sterowniki usługi LIS (Linux Integration) dla funkcji Hyper-V i platformą Azure są modułów jądra, których Microsoft przyczynia się bezpośrednio do nadrzędnego jądra systemu Linux.  Niektórych sterowników LIS są wbudowane w jądra dystrybucji domyślnie. Starsze dystrybucje, które są oparte na systemie Red Hat Enterprise (RHEL) / CentOS są dostępne do pobrania osobno na [Linux integracji usług w wersji 4.2 dla funkcji Hyper-V i Azure](https://www.microsoft.com/en-us/download/details.aspx?id=55106). Zobacz [wymagania jądra systemu Linux](create-upload-generic.md#linux-kernel-requirements) Aby uzyskać więcej informacji na temat sterowników LIS.

Agent systemu Linux platformy Azure wstępnie zainstalowanym systemem obrazów portalu Azure Marketplace i są zazwyczaj dostępne z repozytorium pakietów dystrybucji. Kod źródłowy znajduje się na [GitHub](https://github.com/azure/walinuxagent).

  
| Dystrybucja | Wersja | Sterowniki | Agent |
| --- | --- | --- | --- |
| CentOS |CentOS 6.3+, 7.0+ |CentOS 6.3: [pobrania LIS](https://www.microsoft.com/en-us/download/details.aspx?id=55106)<p>CentOS 6.4 +: W jądrze |Pakiet: W [repozytorium](http://olcentgbl.trafficmanager.net/openlogic/6/openlogic/x86_64/RPMS/) w obszarze "WALinuxAgent" <br/>Kod źródłowy: [GitHub](https://github.com/Azure/WALinuxAgent) |
| [CoreOS](https://coreos.com/docs/running-coreos/cloud-providers/azure/) |494.4.0+ |Jądra |Kod źródłowy: [GitHub](https://github.com/coreos/coreos-overlay/tree/master/app-emulation/wa-linux-agent) |
| Debian |Debian 7,9 +, 8.2 + |Jądra |Pakiet: W repozytorium, w obszarze "waagent" <br/>Kod źródłowy: [GitHub](https://github.com/Azure/WALinuxAgent) |
| Oracle Linux |6.4+, 7.0+ |Jądra |Pakiet: W repozytorium, w obszarze "WALinuxAgent" <br/>Kod źródłowy: [GitHub](https://go.microsoft.com/fwlink/p/?LinkID=250998) |
| Red Hat Enterprise Linux |RHEL 6.7+, 7.1+ |Jądra |Pakiet: W repozytorium, w obszarze "WALinuxAgent" <br/>Kod źródłowy: [GitHub](https://github.com/Azure/WALinuxAgent) |
| SUSE Linux Enterprise |SLES/SLES for SAP<br>11 SP4<br>12 SP1+<br>15|Jądra |Pakiet:<p> 11 WE [chmury: narzędzia](https://build.opensuse.org/project/show/Cloud:Tools) repozytorium<br>Aby uzyskać 12 zawartych w Module "Chmura publiczna" w obszarze "python-azure-agent"<br/>Kod źródłowy: [GitHub](https://go.microsoft.com/fwlink/p/?LinkID=250998) |
| openSUSE |openSUSE Leap 42.2+ |Jądra |Pakiet: W [chmury: narzędzia](https://build.opensuse.org/project/show/Cloud:Tools) repozytorium w obszarze "python-azure-agent" <br/>Kod źródłowy: [GitHub](https://github.com/Azure/WALinuxAgent) |
| Ubuntu |Ubuntu 12.04+ **<sup>1</sup>** |Jądra |Pakiet: W repozytorium, w obszarze "walinuxagent" <br/>Kod źródłowy: [GitHub](https://github.com/Azure/WALinuxAgent) |

  - **<sup>1</sup>**  Ubuntu 12.04 obsługi na platformie Azure można znaleźć [powiadomienie EOL](https://azure.microsoft.com/blog/ubuntu-12-04-precise-pangolin-nearing-end-of-life/).


## <a name="partners"></a>Partnerzy

### <a name="coreos"></a>CoreOS
[https://coreos.com/docs/running-coreos/cloud-providers/azure/](https://coreos.com/docs/running-coreos/cloud-providers/azure/)

Z systemu CoreOS witryny sieci Web:

*CoreOS jest przeznaczona dla zabezpieczeń, zgodności i niezawodności. Zamiast instalowania pakietów za pomocą narzędzia yum lub apt, CoreOS używa kontenerów systemu Linux w celu zarządzania usługami na wyższym poziomie abstrakcji. Kod pojedynczą usługę i wszystkie zależności są spakowane w kontenerze, który może działać na jednej lub wielu maszynach CoreOS.*

### <a name="credativ"></a>credativ
[http://www.credativ.co.uk/credativ-blog/debian-images-microsoft-azure](http://www.credativ.co.uk/credativ-blog/debian-images-microsoft-azure)

Credativ to niezależne konsultacji i usług firmy, która specjalizuje się w projektowania i implementacji profesjonalnych rozwiązań przy użyciu bezpłatnego oprogramowania. Jako wiodących specjalistów typu open source Credativ ma międzynarodowy uznanie z wielu działów IT, korzystających z pomocy technicznej. Wspólnie z firmą Microsoft Credativ obecnie przygotowuje odpowiednie obrazy systemu Debian dla Debian 8 (Jessie) oraz Debian przed 7 (Wheezy). Oba obrazy są specjalnie zaprojektowane do uruchamiania na platformie Azure i można łatwo zarządzać za pomocą platformy. Credativ będzie również obsługiwać długotrwałe utrzymanie i aktualizowanie obrazów systemu Debian dla platformy Azure za pośrednictwem jej centrów Otwórz źródło pomocy technicznej.

### <a name="oracle"></a>Oracle
[http://www.oracle.com/technetwork/topics/cloud/faq-1963009.html](http://www.oracle.com/technetwork/topics/cloud/faq-1963009.html)

Firmy Oracle strategia polega na oferują szeroką gamę rozwiązań dla chmur prywatnych i publicznych. Ta strategia zapewnia wybór i elastyczność, w jaki sposób wdrożenia oprogramowania Oracle w chmurach programu Oracle i innych chmur. Partnerstwo firmy Oracle z firmą Microsoft umożliwia klientom wdrażanie oprogramowania Oracle w chmurach publicznych i prywatnych firmy Microsoft przy zapewnieniu certyfikacji i wsparcia firmy Oracle.  Zobowiązanie firmy Oracle oraz zwrot z inwestycji w rozwiązania chmur publicznych i prywatnych firmy Oracle ulega zmianie.

### <a name="red-hat"></a>Red Hat
[http://www.redhat.com/en/partners/strategic-alliance/microsoft](http://www.redhat.com/en/partners/strategic-alliance/microsoft)

Na świecie wiodący dostawca rozwiązań typu open source, Red Hat ułatwia ponad 90% firm z rankingu Fortune 500 rozwiązywania problemów biznesowych i IT i strategii biznesowej i przygotowania przyszłość technologii. Red Hat robi to, zapewniając bezpiecznych rozwiązań za pośrednictwem modelu biznesowego otwarte i niedrogie stała, przewidywalna subskrypcji.

### <a name="suse"></a>SUSE
[http://www.suse.com/suse-linux-enterprise-server-on-azure](http://www.suse.com/suse-linux-enterprise-server-on-azure)

SUSE Linux Enterprise Server na platformie Azure jest sprawdzonej platformie, która zapewnia doskonałą niezawodność i bezpieczeństwo chmury obliczeniowej. Wszechstronna platforma systemu Linux firmy SUSE bezproblemowo integruje się z usług Azure cloud services w celu dostarczenia środowiska chmury łatwe w zarządzaniu. Z więcej niż 9,200 certyfikowanych aplikacji od ponad 1800 niezależnych dostawców oprogramowania dla systemu SUSE Linux Enterprise Server SUSE gwarantuje, że obciążeń obsługiwanych w centrum danych można bez obaw wdrożyć na platformie Azure.

### <a name="canonical"></a>Canonical
[http://www.ubuntu.com/cloud/azure](http://www.ubuntu.com/cloud/azure)

Canonical inżynierii i nadzór społeczności open dysku sukcesu firmy Ubuntu w klienta, serwera i chmury obliczeniowej, w tym lokacjach chmury osobistej usług dla konsumentów. Wizja firmy Canonical ujednolicone, bezpłatne platformy w systemie Ubuntu z telefonu w chmurze, zapewnia rodziny spójnych interfejsów telefon, tablet, takich jak Telewizor i pulpitu. Tę wizję sprawia, że Ubuntu pierwszy wybór różnych mogą odnieść instytucje od dostawców chmury publicznej twórcy elektronicznych i ulubionych między poszczególne technologists.

Z deweloperami i inżynierów centrach na całym świecie firmy Canonical jednoznacznie znajduje się do współpracy z twórcami sprzętu, dostawców zawartości i deweloperów oprogramowania wprowadzanie Ubuntu rozwiązań na rynek, na którym komputerami, serwerami i urządzeń przenośnych.
