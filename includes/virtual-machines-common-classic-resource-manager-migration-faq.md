---
title: Plik dyrektywy include
description: Plik dyrektywy include
services: virtual-machines
author: jpconnock
ms.service: virtual-machines
ms.topic: include
ms.date: 05/18/2018
ms.author: jeconnoc
ms.custom: include file
ms.openlocfilehash: 15cbfb9babe38ba6acaf4312735ab839af3f2d99
ms.sourcegitcommit: b6319f1a87d9316122f96769aab0d92b46a6879a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/20/2018
ms.locfileid: "34371307"
---
# <a name="frequently-asked-questions-about-classic-to-azure-resource-manager-migration"></a>Często zadawane pytania dotyczące migracji z modelu klasycznego do modelu opartego na usłudze Azure Resource Manager

## <a name="does-this-migration-plan-affect-any-of-my-existing-services-or-applications-that-run-on-azure-virtual-machines"></a>Czy ten plan migracji wpływa na moje istniejące usługi lub aplikacje uruchomione na maszynach wirtualnych platformy Azure? 

Nie. Maszyny wirtualne (klasyczne) to w pełni obsługiwane usługi w ramach ogólnej dostępności. Możesz nadal używać tych zasobów do zwiększenia Twojej obecności na platformie Microsoft Azure.

## <a name="what-happens-to-my-vms-if-i-dont-plan-on-migrating-in-the-near-future"></a>Co stanie się z moimi maszynami wirtualnymi, jeśli nie planuję migracji w najbliższej przyszłości? 

Istniejące klasyczne interfejsy API i model zasobów nie są przestarzałe. Chcemy ułatwić migrację, biorąc pod uwagę zaawansowane funkcje, które są dostępne w modelu wdrażania usługi Resource Manager. Zdecydowanie zalecamy przejrzenie [niektórych udoskonaleń](../articles/azure-resource-manager/resource-manager-deployment-model.md), które są częścią infrastruktury IaaS w ramach usługi Resource Manager.

## <a name="what-does-this-migration-plan-mean-for-my-existing-tooling"></a>Co oznacza ten plan migracji dla moich istniejących narzędzi? 

Aktualizacja narzędzi do modelu wdrażania usługi Resource Manager to jedna z najważniejszych zmian, które należy uwzględnić w planach migracji.

## <a name="how-long-will-the-management-plane-downtime-be"></a>Jak długo będzie trwał przestój płaszczyzny zarządzania? 

To zależy od liczby migrowanych zasobów. W przypadku mniejszych wdrożeń (kilkadziesiąt maszyn wirtualnych) cała migracja powinna trwać krócej niż godzinę. W przypadku wdrożeń na dużą skalę (setki maszyn wirtualnych) migracja może zająć kilka godzin.

## <a name="can-i-roll-back-after-my-migrating-resources-are-committed-in-resource-manager"></a>Czy mogę wykonać wycofanie po zatwierdzeniu migrowanych zasobów w usłudze Resource Manager? 

Możesz przerwać migrację, o ile zasoby są w stanie przygotowania. Wycofanie nie jest obsługiwane po pomyślnym zmigrowaniu zasobów za pomocą operacji zatwierdzenia.

## <a name="can-i-roll-back-my-migration-if-the-commit-operation-fails"></a>Czy mogę wycofać migrację w przypadku niepowodzenia operacji zatwierdzenia? 

Nie można przerwać migracji, jeśli operacja zatwierdzenia nie powiedzie się. Wszystkie operacje migracji, w tym operacja zatwierdzenia, są idempotentne. Dlatego zalecamy podjęcie ponownej próby wykonania operacji po chwili. Jeśli błąd będzie występować nadal, utwórz bilet pomocy technicznej lub wpis z tagiem ClassicIaaSMigration na naszym [forum maszyn wirtualnych](https://social.msdn.microsoft.com/Forums/azure/home?forum=WAVirtualMachinesforWindows).

## <a name="do-i-have-to-buy-another-express-route-circuit-if-i-have-to-use-iaas-under-resource-manager"></a>Czy muszę kupić kolejny obwód usługi ExpressRoute, jeśli muszę używać infrastruktury IaaS w ramach usługi Resource Manager? 

Nie. Ostatnio umożliwiliśmy [przenoszenie obwodów usługi ExpressRoute z klasycznego modelu wdrażania do modelu wdrażania usługi Resource Manager](../articles/expressroute/expressroute-move.md). Nie musisz kupować nowego obwodu usługi ExpressRoute, jeśli masz już taki.

## <a name="what-if-i-had-configured-role-based-access-control-policies-for-my-classic-iaas-resources"></a>Co stanie się, jeśli mam skonfigurowane zasady kontroli dostępu opartej na rolach dla moich klasycznych zasobów IaaS? 

Podczas migracji zasoby są przekształcane z klasycznych na zasoby usługi Resource Manager. Dlatego zalecamy zaplanowanie aktualizacji zasad RBAC, które należy wykonać po migracji.

## <a name="i-backed-up-my-classic-vms-in-a-vault-can-i-migrate-my-vms-from-classic-mode-to-resource-manager-mode-and-protect-them-in-a-recovery-services-vault"></a>I kopię zapasową mojej klasycznych maszyn wirtualnych w magazynie. Czy mogę migrować maszyny wirtualne z trybu klasycznego do trybu usługi Resource Manager i chronić je w magazynie usługi Recovery Services?

<a name="vault">Gdy</a> przenieść Maszynę wirtualną z klasycznym tryb Resource Manager, kopie zapasowe wykonane przed migracją nie będą migrowane do właśnie został zmigrowany Menedżera zasobów maszyny Wirtualnej. Jednak jeśli chcesz przechowywać kopie zapasowe klasycznych maszyn wirtualnych, wykonaj następujące kroki przed migracją. 

1. W magazynie usług odzyskiwania przejdź do **chronione elementy** i wybierz maszynę Wirtualną. 
2. Kliknij pozycję [Zatrzymaj ochronę](../articles/backup/backup-azure-manage-vms.md#stop-protecting-virtual-machines). Pozostaw opcję *Usuń powiązane dane kopii zapasowych* **niezaznaczoną**.

> [!NOTE]
> Zostanie naliczona koszt wystąpienia kopii zapasowej do zachowania danych. Kopie zapasowe będą usuwane dla każdego zakresu przechowywania. Jednak ostatniej kopii zapasowej zawsze jest przechowywana, dopóki nie zostaną jawnie usunięte dane kopii zapasowej. Zaleca się po umieszczeniu zakres przechowywania, Sprawdź zakres przechowywania maszyny wirtualnej i wyzwalacza "Usuń dane kopii zapasowej" w elemencie chroniony w magazynie. 
>
>

Aby przeprowadzić migrację maszyny wirtualnej tryb Resource Manager 

1. Usuń rozszerzenie kopii zapasowej/migawki z maszyny wirtualnej.
2. Przeprowadź migrację maszyny wirtualnej z trybu klasycznego do trybu usługi Resource Manager. Upewnij się, że informacje o magazynie i sieci odpowiadające maszynie wirtualnej również zostały zmigrowane do trybu usługi Resource Manager.

Ponadto, jeśli chcesz utworzyć kopię zapasową zmigrowane maszyny Wirtualnej, przejdź do bloku zarządzania maszyny wirtualnej do [włączenia kopii zapasowej](../articles/backup/quick-backup-vm-portal.md#enable-backup-on-a-vm).

## <a name="can-i-validate-my-subscription-or-resources-to-see-if-theyre-capable-of-migration"></a>Czy mogę zwalidować moją subskrypcję lub moje zasoby, aby sprawdzić, czy można je zmigrować? 

Tak. W przypadku opcji migracji obsługiwanej przez platformę pierwszym krokiem przygotowania do migracji jest zwalidowanie zasobów pod kątem możliwości ich migracji. Jeśli operacja walidacji nie powiedzie się, zostaną zgłoszone komunikaty dla wszystkich przyczyn uniemożliwiających wykonanie migracji.

## <a name="what-happens-if-i-run-into-a-quota-error-while-preparing-the-iaas-resources-for-migration"></a>Co stanie się, jeśli wystąpi błąd limitu przydziału podczas przygotowywania zasobów IaaS do migracji? 

Zalecamy przerwanie migracji, a następnie zgłoszenie żądania pomocy technicznej w celu zwiększenia limitów przydziału w regionie, w którym są migrowane maszyny wirtualne. Po zatwierdzeniu żądania dotyczącego limitu przydziału możesz ponownie rozpocząć wykonywanie kroków migracji.

## <a name="how-do-i-report-an-issue"></a>Jak mogę zgłosić problem? 

Problemy i pytania dotyczące migracji można publikować na naszym [forum maszyn wirtualnych](https://social.msdn.microsoft.com/Forums/azure/home?forum=WAVirtualMachinesforWindows), używając słowa kluczowego ClassicIaaSMigration. Zalecamy publikowanie wszystkich pytań na tym forum. Jeśli masz umowę pomocy technicznej, możesz także zgłosić bilet pomocy technicznej.

## <a name="what-if-i-dont-like-the-names-of-the-resources-that-the-platform-chose-during-migration"></a>Co zrobić, jeśli nie podobają mi się nazwy zasobów wybrane przez platformę podczas migracji? 

Wszystkie zasoby z nazwami jawnie podanymi w klasycznym modelu wdrażania zostaną zachowane podczas migracji. W niektórych przypadkach zostaną utworzone nowe zasoby. Na przykład dla każdej maszyny wirtualnej zostanie utworzony interfejs sieciowy. Obecnie nie obsługujemy możliwości kontrolowania nazw nowych zasobów tworzonych podczas migracji. Zagłosuj na tę funkcję na [forum opinii platformy Azure](http://feedback.azure.com).

## <a name="can-i-migrate-expressroute-circuits-used-across-subscriptions-with-authorization-links"></a>Czy mogę zmigrować obwody usługi ExpressRoute używane w subskrypcjach wraz z łączami autoryzacji? 

Obwodów usługi ExpressRoute używających łącz autoryzacji między subskrypcjami nie można zmigrować automatycznie bez przestoju. Udostępniamy przewodnik z opisem wykonywania takiej migracji ręcznie. Kroki i więcej informacji zawiera temat [Migrate ExpressRoute circuits and associated virtual networks from the classic to the Resource Manager deployment model](../articles/expressroute/expressroute-migration-classic-resource-manager.md) (Migrowanie obwodów usługi ExpressRoute i skojarzonych sieci wirtualnych z modelu wdrażania klasycznego do modelu usługi Resource Manager).

## <a name="i-got-the-message-vm-is-reporting-the-overall-agent-status-as-not-ready-hence-the-vm-cannot-be-migrated-ensure-that-the-vm-agent-is-reporting-overall-agent-status-as-ready-or-vm-contains-extension-whose-status-is-not-being-reported-from-the-vm-hence-this-vm-cannot-be-migrated"></a>Otrzymano komunikat *"maszyny Wirtualnej jest raportowania ogólny stan agenta nie jest gotowe. Z tego powodu nie można migrować maszyny wirtualnej. Upewnij się, że Agent maszyny Wirtualnej jest raportowania ogólny stan agenta jako gotowy"* lub *"maszyny Wirtualnej zawiera rozszerzenia, których stan nie jest raportowany przez maszynę Wirtualną. W związku z tym tej maszyny Wirtualnej nie można migrować."*

Ten komunikat jest zgłaszany, jeśli maszyna wirtualna nie ma połączenia wychodzącego do Internetu. Agent maszyny wirtualnej używa połączenia wychodzącego, aby uzyskać dostęp do konta usługi Azure Storage na potrzeby aktualizacji stanu agenta co pięć minut.
