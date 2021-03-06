---
title: Przenoszenie maszyn wirtualnych IaaS platformy Azure do innego regionu świadczenia usługi Azure przy użyciu usługi Azure Site Recovery | Microsoft Docs
description: Używanie usługi Azure Site Recovery do przenoszenia maszyn wirtualnych IaaS platformy Azure z jednego regionu świadczenia usługi Azure do innego.
services: site-recovery
author: rayne-wiselman
ms.service: site-recovery
ms.topic: tutorial
ms.date: 12/27/2018
ms.author: raynew
ms.custom: MVC
ms.openlocfilehash: 2ce9c486dee3f26d23db5da67abfea4701f85796
ms.sourcegitcommit: 8330a262abaddaafd4acb04016b68486fba5835b
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/04/2019
ms.locfileid: "54040478"
---
# <a name="move-azure-vms-to-another-region"></a>Przenoszenie maszyn wirtualnych platformy Azure do innego regionu

Oprócz używania usługi [Azure Site Recovery](site-recovery-overview.md) do zarządzania odzyskiwaniem maszyn lokalnych i maszyn wirtualnych platformy Azure po awarii oraz ich organizowania dla celów zapewniania ciągłości działania i odzyskiwania po awarii (BCDR, business continuity and disaster recovery) można ją stosować również do zarządzania przenoszeniem maszyn wirtualnych platformy Azure do regionu pomocniczego. Aby przenieść maszyny wirtualne platformy Azure, należy włączyć ich replikację, a następnie przełączyć je w tryb failover z regionu podstawowego do wybranego regionu pomocniczego.

Ten samouczek przedstawia sposób przenoszenia maszyn wirtualnych platformy Azure do innego regionu. Ten samouczek zawiera informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Tworzenie magazynu usługi Recovery Services
> * Włączanie replikacji maszyny wirtualnej
> * Uruchamianie trybu failover w celu przeniesienia maszyny wirtualnej

W tym samouczku założono, że masz już subskrypcję platformy Azure. Jeśli jeszcze jej nie masz, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/pricing/free-trial/).





## <a name="prerequisites"></a>Wymagania wstępne

- Upewnij się, że w regionie świadczenia usługi Azure, z którego chcesz przenieść, znajdują się maszyny wirtualne platformy Azure.
- Przeanalizuj informacje o [składnikach i architekturze scenariusza](azure-to-azure-architecture.md).
- Zapoznaj się z [ograniczeniami i wymaganiami dotyczącymi pomocy technicznej](azure-to-azure-support-matrix.md).



## <a name="before-you-start"></a>Przed rozpoczęciem

Przed skonfigurowaniem replikacji wykonaj poniższe czynności.


### <a name="verify-target-resources"></a>Sprawdzanie zasobów docelowych

1. Sprawdź, czy Twoja subskrypcja platformy Azure umożliwia tworzenie maszyn wirtualnych w regionie docelowym używanym do odzyskiwania po awarii. Skontaktuj się z pomocą techniczną, aby włączyć wymagany limit przydziału.

2. Upewnij się, że zasoby subskrypcji są wystarczające do obsługi maszyn wirtualnych o rozmiarach odpowiadających źródłowym maszynom wirtualnym. Usługa Site Recovery wybiera ten sam lub najbardziej zbliżony rozmiar dla docelowej maszyny wirtualnej.


### <a name="verify-account-permissions"></a>Sprawdzanie uprawnień konta

Jeśli bezpłatne konto platformy Azure zostało właśnie utworzone, jesteś administratorem subskrypcji. Jeśli nie jesteś administratorem subskrypcji, współpracuj z administratorem w celu przypisania potrzebnych uprawnień. Aby włączyć replikację nowej maszyny wirtualnej, musisz mieć:

1. Uprawnienia do tworzenia maszyny wirtualnej w ramach zasobów platformy Azure. Wbudowana rola „Współautor maszyny wirtualnej” ma te uprawnienia. Obejmują one:
    - Uprawnienie do tworzenia maszyny wirtualnej w wybranej grupie zasobów
    - Uprawnienie do tworzenia maszyny wirtualnej w wybranej sieci wirtualnej
    - Uprawnienie do zapisu na wybranym koncie magazynu

2. Musisz mieć również uprawnienie do zarządzania operacjami usługi Azure Site Recovery. Rola „Współautor usługi Site Recovery” ma wszystkie uprawnienia wymagane do zarządzania operacjami usługi Site Recovery w magazynie usługi Recovery Services.


### <a name="verify-vm-outbound-access"></a>Sprawdzanie wychodzącego dostępu do maszyny wirtualnej

1. Upewnij się, że nie używasz uwierzytelniania serwera proxy do kontrolowania łączności sieciowej dla maszyn wirtualnych, które chcesz przenieść. 
2. Do celów tego samouczka założono, że maszyny wirtualne do przeniesienia mogą uzyskiwać dostęp do Internetu oraz że nie używasz serwera proxy zapory do kontrolowania dostępu wychodzącego. Jeśli tak jest, sprawdź wymagania [tutaj](azure-to-azure-tutorial-enable-replication.md#configure-outbound-network-connectivity).

### <a name="verify-vm-certificates"></a>Weryfikowanie certyfikatów maszyn wirtualnych

Sprawdź, czy na maszynach wirtualnych platformy Azure, które chcesz przenieść, są obecne wszystkie najnowsze certyfikaty główne. Jeśli brakuje najnowszych certyfikatów głównych, nie można zarejestrować maszyny wirtualnej w usłudze Site Recovery ze względu na ograniczenia związane z zabezpieczeniami.

- Aby zainstalować wszystkie zaufane certyfikaty główne na maszynach wirtualnych z systemem Windows, zainstaluj wszystkie najnowsze aktualizacje systemu Windows. W środowisku bez połączenia postępuj zgodnie ze standardową procedurą usługi Windows Update i procedurą aktualizacji certyfikatów, które są używane w danej organizacji.
- Aby zainstalować najnowsze wymagane certyfikaty główne i listę odwołania certyfikatów na maszynach wirtualnych z systemem Linux, postępuj zgodnie ze wskazówkami dystrybutora systemu Linux.



## <a name="create-a-vault"></a>Tworzenie magazynu

Magazyn można utworzyć w dowolnym regionie, z wyjątkiem regionu źródłowego.

1. Zaloguj się do witryny [Azure Portal](https://portal.azure.com) > **Recovery Services**.
2. Kliknij kolejno pozycje **Utwórz zasób** > **Narzędzia do zarządzania** > **Backup i Site Recovery**.
3. W polu **Nazwa** podaj przyjazną nazwę **ContosoVMVault**. Jeśli masz więcej niż jedną subskrypcję, wybierz jedną z nich.
4. Utwórz grupę zasobów **ContosoRG**.
5. Określ region platformy Azure. Aby sprawdzić obsługiwane regiony, zobacz sekcję dotyczącą dostępności geograficznej w temacie [Szczegóły cennika usługi Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).
6. Aby szybko uzyskać dostęp do magazynu z pulpitu nawigacyjnego, kliknij pozycję **Przypnij do pulpitu nawigacyjnego**, a następnie kliknij pozycję **Utwórz**.

   ![Nowy magazyn](./media/tutorial-migrate-azure-to-azure/azure-to-azure-vault.png)

Nowy magazyn zostanie dodany do sekcji **Pulpit nawigacyjny** w obszarze **Wszystkie zasoby** oraz pojawi się na stronie głównej **Magazyny usługi Recovery Services**.






## <a name="select-the-source"></a>Wybieranie źródła

1. W obszarze magazynów usługi Recovery Services kliknij kolejno pozycje **ConsotoVMVault** > **+ Replikuj**.
2. W obszarze **Źródło** wybierz pozycję **Azure**.
3. W obszarze **Lokalizacja źródłowa** wybierz źródłowy region świadczenia usługi Azure, w którym są uruchomione maszyny wirtualne.
4. Wybierz model wdrażania usługi Resource Manager. Następnie wybierz pozycję **Źródłowa grupa zasobów**.
5. Kliknij pozycję **OK**, aby zapisać ustawienia.


## <a name="enable-replication-for-azure-vms"></a>Włączanie replikacji maszyn wirtualnych platformy Azure

Usługa Site Recovery pobiera listę maszyn wirtualnych skojarzonych z subskrypcją i grupą zasobów.


1. W witrynie Azure Portal kliknij pozycję **Maszyny wirtualne**.
2. Wybierz maszynę wirtualną, którą chcesz przenieść. Następnie kliknij przycisk **OK**.
3. W obszarze **Ustawienia** kliknij pozycję **Odzyskiwanie po awarii**.
4. W obszarze **Konfigurowanie odzyskiwania po awarii** > **Region docelowy** wybierz region docelowy, w którym maszyna będzie replikowana.
5. Dla celów tego samouczka zaakceptuj inne ustawienia domyślne.
6. Kliknij pozycję **Włącz replikację**. Spowoduje to uruchomienie zadania włączającego replikację dla maszyny wirtualnej.

    ![włączanie replikacji](media/tutorial-migrate-azure-to-azure/settings.png)

 

## <a name="run-a-failover"></a>Uruchamianie trybu failover

1. W obszarze **Ustawienia** > **Replikowane elementy** kliknij maszynę, a następnie kliknij pozycję **Tryb failover**.
2. W obszarze **Tryb failover** wybierz pozycję **Najnowsze**. Ustawienie klucza szyfrowania nie ma znaczenia w przypadku tego scenariusza.
3. Wybierz pozycję **Zamknij maszynę przed rozpoczęciem pracy w trybie failover**. Usługa Site Recovery próbuje zamknąć źródłową maszynę wirtualną przed wyzwoleniem trybu failover. Przełączanie do trybu failover będzie kontynuowane, nawet jeśli zamknięcie nie powiedzie się. Na stronie **Zadania** można śledzić postęp trybu failover.
4. Sprawdź, czy maszyna wirtualna Azure jest wyświetlana na platformie Azure zgodnie z oczekiwaniami.
5. W obszarze **Replikowane elementy** kliknij prawym przyciskiem myszy maszynę wirtualną, a następnie kliknij pozycję **Zatwierdź**. Spowoduje to zakończenie procesu migracji.
6. Po zakończeniu zatwierdzania kliknij pozycję **Wyłącz replikację**.  Spowoduje to zatrzymanie replikacji maszyny wirtualnej.



## <a name="next-steps"></a>Następne kroki

W tym samouczku przeniesiono maszynę wirtualną platformy Azure do innego regionu świadczenia usługi Azure. Teraz możesz skonfigurować odzyskiwanie po awarii dla przeniesionej maszyny wirtualnej.

> [!div class="nextstepaction"]
> [Konfigurowanie odzyskiwania po awarii po migracji](azure-to-azure-quickstart.md)

