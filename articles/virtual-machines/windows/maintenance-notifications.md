---
title: Obsługa powiadomienia o konserwacji dla maszyn wirtualnych Windows na platformie Azure | Dokumentacja firmy Microsoft
description: Wyświetl powiadomienia o konserwacji dla maszyn wirtualnych Windows działających na platformie Azure i uruchomić konserwacji samoobsługowej.
services: virtual-machines-windows
documentationcenter: ''
author: shants123
editor: ''
tags: azure-service-management,azure-resource-manager
ms.assetid: ''
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/02/2018
ms.author: shants
ms.openlocfilehash: f8cac174844d7f87687d08975b6fbf17ed47b03e
ms.sourcegitcommit: 71ee622bdba6e24db4d7ce92107b1ef1a4fa2600
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/17/2018
ms.locfileid: "53543295"
---
# <a name="handling-planned-maintenance-notifications-for-windows-virtual-machines"></a>Obsługa Planned maintenance notifications zaplanowanej dla maszyn wirtualnych Windows

Platforma Azure jest co pewien czas aktualizowana w celu poprawy niezawodności, wydajności i zabezpieczeń infrastruktury hostowania maszyn wirtualnych. Aktualizacje są zmiany, takie jak stosowanie poprawek środowiska macierzystego lub uaktualniania i likwidowaniu sprzętu. Większość tych aktualizacji jest przeprowadzana bez żadnego wpływu na obsługiwanych maszynach wirtualnych. Jednakże istnieją przypadki, w których aktualizacje mają wpływ:

- Jeśli konserwacja nie wymaga ponownego uruchomienia systemu, platforma Azure używa migracji w miejscu wstrzymać maszyny Wirtualnej, gdy host jest aktualizowana. Te operacje konserwacji bez rebootful są domena błędów zastosowane przez domenę błędów, a postęp zostanie zatrzymany, jeśli wszystkie sygnały kondycji ostrzeżenia są odbierane. 

- Jeśli przeprowadzenia konserwacji wymagane jest ponowne uruchomienie komputera, otrzymasz powiadomienie o podczas planowanej konserwacji. W takich przypadkach są podane przedział czasu, w którym możesz uruchomić konserwację samodzielnie, kiedy pracuje dla Ciebie.


Planowana konserwacja, która wymaga ponownego uruchomienia, zaplanowano etapami. Każdy etap ma inny zakres (regiony).

- Falą rozpoczyna się od powiadomienie dla klientów. Domyślnie powiadomienia są wysyłane do właściciela subskrypcji i współwłaścicieli. Możesz dodać więcej adresatów i opcje obsługi komunikatów, takie jak wiadomości e-mail, wiadomości SMS i elementy Webhook, do powiadomienia za pomocą platformy Azure [alertów dziennika aktywności](../../azure-monitor/platform/activity-logs-overview.md).  
- W momencie zgłoszenia *samoobsługi okna* ma zostać udostępnione. W tym oknie możesz znaleźć, w której maszyny wirtualne znajdują się w tej fazie badania i aktywnie Uruchom konserwację zgodnie z potrzebami planowania.
- Po oknie samoobsługi *zaplanowanego okna obsługi* rozpoczyna się. W pewnym momencie podczas tego okna platforma Azure planuje i dotyczy wymagane konserwacji maszyny wirtualnej. 

Cel, że dwa okna jest zapewnienie wystarczająco dużo czasu, aby uruchomić konserwacji i ponowne uruchomienie maszyny wirtualnej codzienne, gdy Azure nastąpi automatyczne uruchomienie konserwacji.


Można znaleźć okna obsługi dla maszyn wirtualnych, a następnie uruchomić konserwacji samoobsługowej, można użyć witryny Azure portal, programu PowerShell, interfejsu API REST i interfejsu wiersza polecenia.

  
## <a name="should-you-start-maintenance-during-the-self-service-window"></a>W oknie samoobsługi należy rozpocząć konserwacji?  

Poniższe wskazówki powinny pomóc w zdecyduj, czy chcesz używać tej funkcji i uruchomić własny czas konserwacji.

> [!NOTE] 
> Konserwacji samoobsługowej może nie być dostępne dla wszystkich maszyn wirtualnych. Aby ustalić, czy aktywnego ponownego wdrożenia jest dostępna dla maszyny Wirtualnej, poszukaj **teraz uruchomić** stanu konserwacji. Konserwacji samoobsługowej nie jest obecnie dostępna w przypadku usług Cloud Services (internetowy proces roboczy) i usługi Service Fabric.


Konserwacji samoobsługowej nie jest zalecane w przypadku wdrożeń za pomocą **zestawy dostępności** ponieważ te konfiguracje o wysokiej dostępności, której dotyczy to tylko jedna domena aktualizacji w dowolnym momencie. 
- Pozwól Azure wyzwolić konserwacji. Konserwacji, która wymaga ponownego uruchomienia należy pamiętać, że konserwacja będzie odbywać się domena aktualizacji według domeny aktualizacji, że domenach aktualizacji nie otrzymywać konserwację sekwencyjnie, oraz czy 30-minutowe pauzę między domenami aktualizacji. 
- Jeśli do tymczasowej utraty niektórych pojemności (liczba domen aktualizacji/1) ma znaczenie, jego można łatwo skompensować przydzielając dodatkowe wystąpienia w okresie konserwacji.
- Konserwacji, który nie jest wymagane ponowne uruchomienie, aktualizacje są stosowane na poziomie domeny błędów.
    
**Nie** Użyj konserwacji samoobsługowej w następujących scenariuszach: 
- Jeśli wyłączysz maszyn wirtualnych, albo ręcznie, za pomocą usługi DevTest Labs przy użyciu automatycznego zamykania lub zgodnie z harmonogramem, może cofnąć stanu konserwacji i w związku z tym spowodować przestój dodatkowe.
- Na maszynach wirtualnych krótkotrwałe czy wiesz, zostaną usunięte przed upływem fala konserwacji. 
- W przypadku obciążeń o dużych stanie przechowywanych w (efemeryczne) dysk lokalny, który jest pożądane, aby zachować przy aktualizacji. 
- W przypadkach, w którym możesz zmienić rozmiar maszyny Wirtualnej często ponieważ można przywrócić stanu konserwacji.
- Jeśli zdecydowali się zaplanowanych zdarzeń, umożliwiające proaktywne trybu failover lub łagodne zamykanie obciążenie, 15 minut przed rozpoczęciem konserwacji zamknięcia

**Użyj** konserwacji samoobsługowej, jeśli zamierzasz uruchomić nieprzerwaną podczas fazy zaplanowanej konserwacji maszyny Wirtualnej i żadna oznaczeń zaradcze wymienione powyżej nie ma zastosowania. 

Najlepiej użyć konserwacji samoobsługowej w następujących przypadkach:

- Musisz przekazać dokładnie konserwacyjne do zarządzania lub odbiorcy końcowego. 
- Trzeba wykonać konserwacji przed upływem określonego terminu. 
- Wymagane jest sterowanie sekwencję konserwacji, na przykład wielowarstwową aplikację w celu zagwarantowania bezpiecznej odzyskiwania.
- Potrzebujesz więcej niż 30 minut czasu odzyskiwania maszyny Wirtualnej między dwiema domenami aktualizacji (domenami aktualizacji). Aby kontrolować czas między domenami aktualizacji, możesz wyzwolić konserwacji w sieci maszyn wirtualnych z jednej domeny aktualizacji (UD) w danym momencie.

 

[!INCLUDE [virtual-machines-common-maintenance-notifications](../../../includes/virtual-machines-common-maintenance-notifications.md)]

## <a name="check-maintenance-status-using-powershell"></a>Sprawdzanie stanu konserwacji przy użyciu programu PowerShell

Można również użyć programu Azure Powershell pozwalają zobaczyć, kiedy maszyn wirtualnych jest zaplanowana do konserwacji. Informacje o planowanej konserwacji jest dostępne z [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) polecenia cmdlet, gdy używasz `-status` parametru.
 
Informacje o konserwacji jest zwracany tylko wtedy, gdy planowanej konserwacji. Nie konserwacja jest zaplanowana, która ma wpływ na maszynę Wirtualną, polecenie cmdlet nie zwraca żadnych informacji konserwacji. 

```powershell
Get-AzureRmVM -ResourceGroupName rgName -Name vmName -Status
```

W obszarze MaintenanceRedeployStatus zwracane są następujące właściwości: 
| Wartość | Opis   |
|-------|---------------|
| IsCustomerInitiatedMaintenanceAllowed | Wskazuje, czy możesz uruchomić konserwację na maszynie Wirtualnej, w tym momencie ||
| PreMaintenanceWindowStartTime         | Początek okna obsługi samoobsługi podczas można zainicjować obsługi na maszynie Wirtualnej ||
| PreMaintenanceWindowEndTime           | Koniec samoobsługi oknem obsługi po można zainicjować obsługi na maszynie Wirtualnej ||
| MaintenanceWindowStartTime            | Na początek zaplanowanej konserwacji, w którym Azure powoduje zainicjowanie konserwacji na maszynie Wirtualnej ||
| MaintenanceWindowEndTime              | Koniec okna zaplanowanych konserwacji, w którym Azure powoduje zainicjowanie konserwacji na maszynie Wirtualnej ||
| LastOperationResultCode               | Wynik ostatniej próby umożliwiającej samodzielne zainicjowanie konserwacji na maszynie Wirtualnej ||



Można również uzyskać stanu konserwacji dla wszystkich maszyn wirtualnych w grupie zasobów, za pomocą [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) i nie został podany maszyny Wirtualnej.
 
```powershell
Get-AzureRmVM -ResourceGroupName rgName -Status
```

Używając następującej funkcji programu PowerShell ma identyfikator subskrypcji i wyświetla listę maszyn wirtualnych, które jest zaplanowana do konserwacji.

```powershell

function MaintenanceIterator
{
    Select-AzureRmSubscription -SubscriptionId $args[0]

    $rgList= Get-AzureRmResourceGroup 

    for ($rgIdx=0; $rgIdx -lt $rgList.Length ; $rgIdx++)
    {
        $rg = $rgList[$rgIdx]        
    $vmList = Get-AzureRMVM -ResourceGroupName $rg.ResourceGroupName 
        for ($vmIdx=0; $vmIdx -lt $vmList.Length ; $vmIdx++)
        {
            $vm = $vmList[$vmIdx]
            $vmDetails = Get-AzureRMVM -ResourceGroupName $rg.ResourceGroupName -Name $vm.Name -Status
              if ($vmDetails.MaintenanceRedeployStatus )
            {
                Write-Output "VM: $($vmDetails.Name)  IsCustomerInitiatedMaintenanceAllowed: $($vmDetails.MaintenanceRedeployStatus.IsCustomerInitiatedMaintenanceAllowed) $($vmDetails.MaintenanceRedeployStatus.LastOperationMessage)"               
            }
          }
    }
}

```

### <a name="start-maintenance-on-your-vm-using-powershell"></a>Uruchom konserwację na maszynie Wirtualnej przy użyciu programu PowerShell

Korzystając z informacji z funkcji, w poprzedniej sekcji, następujące rozpoczęciem konserwacji na maszynie Wirtualnej Jeśli **IsCustomerInitiatedMaintenanceAllowed** jest ustawiona na wartość true.

```powershell
Restart-AzureRmVM -PerformMaintenance -name $vm.Name -ResourceGroupName $rg.ResourceGroupName 
```

## <a name="classic-deployments"></a>Klasyczne wdrożenia

Jeśli nadal masz starsze maszyny wirtualne, które zostały wdrożone za pomocą klasycznego modelu wdrażania, można za pomocą programu PowerShell zapytania dla maszyn wirtualnych i zainicjowanie konserwacji.

Aby uzyskać stan konserwacji maszyny wirtualnej, wpisz:

```
Get-AzureVM -ServiceName <Service name> -Name <VM name>
```

Aby uruchomić konserwację na klasycznej maszynie Wirtualnej, wpisz:

```
Restart-AzureVM -InitiateMaintenance -ServiceName <service name> -Name <VM name>
```


## <a name="faq"></a>Często zadawane pytania


**PYT.: Dlaczego należy teraz przeprowadzić ponowny rozruch maszyny wirtualne?**

**ODP.:** Chociaż większość aktualizacji i uaktualnień do platformy Azure nie miało wpływu na dostępność maszyn wirtualnych, są przypadki, w których nie możemy uniknąć, ponowne uruchamianie maszyn wirtualnych hostowanych na platformie Azure. Zakumulowaliśmy kilka zmian, które wymagają ponownego uruchomienia naszych serwerów, które będą powodować ponowny rozruch maszyn wirtualnych.

**PYT.: Jeśli I postępuj zgodnie z zaleceniami, usługi wysokiej dostępności przy użyciu zestawu dostępności, mogę bezpieczne?**

**ODP.:** Maszyny wirtualne wdrożone w zestawie dostępności lub zestawach skalowania maszyn wirtualnych obsługują pojęcie domen aktualizacji (UD). Podczas przeprowadzania konserwacji platforma Azure honoruje ograniczenia domen aktualizacji i nie zostanie wykonany ponowny rozruch maszyn wirtualnych z różnych UD (w tym samym zestawie dostępności).  Azure oczekuje również co najmniej 30 minut przed przejściem do następnej grupy maszyn wirtualnych. 

Aby uzyskać więcej informacji na temat wysokiej dostępności, zobacz [regiony i dostępność maszyn wirtualnych na platformie Azure](regions-and-availability.MD).

**PYT.: Jak otrzymywanie powiadomień o planowanej konserwacji?**

**ODP.:** Uruchamia planowanej konserwacji przez ustawienie harmonogramu na jednym lub wielu regionach platformy Azure. Wkrótce po wiadomość e-mail z powiadomieniem są wysyłane do właścicieli subskrypcji (jedną wiadomość e-mail na subskrypcję). Dodatkowe kanały i adresatów dla tego powiadomienia można konfigurować za pomocą alertów dziennika aktywności. W przypadku, gdy wdrożono maszynę wirtualną w regionie, gdzie jest już zaplanowana planowanej konserwacji, nie będą otrzymywać powiadomienia, ale raczej muszą sprawdzać stan konserwacji maszyny wirtualnej.

**PYT.: Nie widzę żadnego wskazania dotyczącego planowanej konserwacji w portalu, programu Powershell lub interfejsu wiersza polecenia. Co jest nie tak?**

**ODP.:** Informacje dotyczące planowanej konserwacji jest dostępne podczas fali planowanej konserwacji tylko dla maszyn wirtualnych, które będą mieć wpływ na jej. Innymi słowy Jeśli dane nie są wyświetlane, możliwe że fala konserwacji została już zakończona (lub Nierozpoczęte) lub maszyny wirtualnej jest już hostowana na zaktualizowanym serwerze.

**PYT.: Czy istnieje sposób, aby dowiedzieć się, kiedy będzie mieć wpływ na mojej maszynie wirtualnej?**

**ODP.:** Gdy ustawienia harmonogramu, definiujemy przedział czasu w kilka dni. Jednak dokładne sekwencjonowanie serwerów (i maszyn wirtualnych), w tym przedziale czasu jest nieznany. Klienci, którzy chcieliby wiedzieć dokładny czas dla maszyn wirtualnych, można użyć [zaplanowane zdarzenia](scheduled-events.md) zapytania z poziomu maszyny wirtualnej i Otrzymuj powiadomienie 15 minut przed ponownym rozruchem maszyny Wirtualnej.

**PYT.: Jak długo potrwa ponowne uruchomienie mojej maszyny wirtualnej?**

**ODP.:**  W zależności od rozmiaru maszyny Wirtualnej ponowne uruchomienie komputera może zająć do kilku minut w oknie konserwacji samoobsługowej. Podczas Azure zainicjował ponowne uruchomienia w okna zaplanowanej konserwacji podczas ponownego rozruchu zwykle zajmie około 25 minut. Należy pamiętać, że w przypadku, gdy używasz usługi Cloud Services (internetowy proces roboczy), zestawy skalowania maszyn wirtualnych lub zestawów dostępności, będziesz mieć możliwość wybrania 30 minut między poszczególnymi grupami z maszyn wirtualnych (UD) podczas okna zaplanowanej konserwacji. 

**PYT.: Co to jest środowisko w przypadku zestawów skalowania maszyn wirtualnych?**

**ODP.:** Planowana konserwacja jest teraz dostępna dla zestawów skalowania maszyn wirtualnych. Aby uzyskać instrukcje dotyczące sposobu inicjowania konserwacji samoobsługowej, zobacz [planowanej konserwacji dla zestawu skalowania maszyn wirtualnych](../../virtual-machine-scale-sets/virtual-machine-scale-sets-maintenance-notifications.md) dokumentu.

**PYT.: Co to jest środowisko w przypadku usług Cloud Services (internetowy proces roboczy) i usługi Service Fabric?**

**ODP.:** Mimo że planowana konserwacja ma wpływ na te platformy, klienci korzystający z tych platform są uznawani za bezpiecznych, o ile w danym momencie konserwacja będzie miała wpływ tylko na maszyny wirtualne w jednej domenie uaktualnienia. Konserwacji samoobsługowej nie jest obecnie dostępna w przypadku usług Cloud Services (internetowy proces roboczy) i usługi Service Fabric.

**PYT.: Nie widzę żadnych informacji konserwacji na moich maszynach wirtualnych. Czym jest problem?**

**ODP.:** Istnieje kilka powodów dlaczego nie widzisz żadnych informacji konserwacji na maszynach wirtualnych:
1.  Używane są oznaczone jako Microsoft wewnętrzne subskrypcji.
2.  Maszyny wirtualne nie jest zaplanowana do konserwacji. Możliwe, że fala konserwacji została zakończona, anulowana lub zmodyfikować tak, aby maszyny wirtualne są nie wpływa już go.
3.  Nie masz **konserwacji** kolumną dodaną do widoku listy maszyn wirtualnych. Dodaliśmy tę kolumnę do widoku domyślnego, klienci, którzy skonfigurowali, aby zobaczyć kolumn innych niż domyślne należy ręcznie dodać **konserwacji** kolumnę do widoku listy ich maszyn wirtualnych.

**PYT.: Moja maszyna wirtualna jest zaplanowana do konserwacji po raz drugi. Dlaczego?**

**ODP.:** Istnieje kilka przypadków użycia, w których zobaczysz, że maszyna wirtualna została zaplanowana do konserwacji po zakończeniu konserwacji i ponownego wdrożenia:
1.  Firma Microsoft ma anulowane fala konserwacji i ponownego uruchomienia go przy użyciu różnych ładunku. Możliwe, że Wykryliśmy, że ładunek błędowi i po prostu należy wdrożyć dodatkowe ładunku.
2.  Maszyna wirtualna działała *usługi naprawiane* do innego węzła ze względu na usterkę sprzętową.
3.  Wybrano, aby zatrzymać (Cofnij ich przydział) i uruchom ponownie maszynę Wirtualną
4.  Masz **automatyczne zamknięcie** włączone dla maszyny Wirtualnej


## <a name="next-steps"></a>Kolejne kroki

Dowiedz się, jak możesz się zarejestrować zdarzenia konserwacji z w ramach maszyny Wirtualnej przy użyciu [Scheduled Events](scheduled-events.md).
