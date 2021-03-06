---
title: Maszyna wirtualna aktualizacji i zarządzanie za pomocą usługi Azure Stack | Dokumentacja firmy Microsoft
description: Dowiedz się, jak używać rozwiązania Zarządzanie aktualizacjami, śledzenie zmian i spisu w usłudze Azure Automation do zarządzania Windows i maszyn wirtualnych systemu Linux, które są wdrożone w usłudze Azure Stack.
services: azure-stack
documentationcenter: ''
author: jeffgilb
manager: femila
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/15/2018
ms.author: jeffgilb
ms.reviewer: rtiberiu
ms.openlocfilehash: b86a9a0cff397148b0632b3108f58a1977b518e9
ms.sourcegitcommit: dede0c5cbb2bd975349b6286c48456cfd270d6e9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/16/2019
ms.locfileid: "54332510"
---
# <a name="azure-stack-vm-update-and-management"></a>Usługa Azure Stack VM update i zarządzanie
Następujące funkcje rozwiązania usługi Azure Automation służy do zarządzania Windows i maszyn wirtualnych systemu Linux, które są wdrażane przy użyciu usługi Azure Stack:

- **[Zarządzanie aktualizacjami](https://docs.microsoft.com/azure/automation/automation-update-management)**. Rozwiązanie Update Management możesz szybko ocenić stan dostępnych aktualizacji na wszystkich komputerach z agentami i zarządzanie procesem instalacji wymaganych aktualizacji dla tych maszyn wirtualnych systemu Linux i Windows.

- **[Śledzenie zmian](https://docs.microsoft.com/azure/automation/automation-change-tracking)**. Zmiany zainstalowanego oprogramowania, usług Windows, plików i rejestru Windows i demonów systemu Linux na monitorowanych serwerach są wysyłane do usługi Log Analytics w chmurze do przetwarzania. Logika jest stosowana do odebranych danych i usługi w chmurze rejestruje dane. Korzystając z informacji podanych na pulpicie nawigacyjnym śledzenia zmian, łatwo widać zmiany wprowadzone w ramach infrastruktury serwera.

- **[Spis](https://docs.microsoft.com/azure/automation/automation-vm-inventory)**. Spis śledzenia dla maszyny wirtualnej usługi Azure Stack zapewnia interfejs użytkownika oparty na przeglądarce do instalowania i konfigurowania zbierania spisu. 

> [!IMPORTANT]
> Te rozwiązania są takie same jak te używane do zarządzania maszynami wirtualnymi platformy Azure. Maszyny wirtualne platformy Azure Stack i Azure odbywa się w taki sam sposób, przy użyciu tego samego interfejsu, przy użyciu tych samych narzędzi. Maszyny wirtualne Azure Stack również kosztują taka sama jak maszyny wirtualne platformy Azure, korzystając z rozwiązania Update Management, śledzenia zmian i spisu rozwiązania z usługą Azure Stack.

## <a name="prerequisites"></a>Wymagania wstępne
Kilka wymagań wstępnych, muszą zostać spełnione przed rozpoczęciem korzystania z tych funkcji do aktualizacji i zarządzanie maszynami wirtualnymi platformy Azure Stack. Obejmują one kroki, które należy podjąć w witrynie Azure portal, jak i portalu administracyjnego usługi Azure Stack.

### <a name="in-the-azure-portal"></a>W witrynie Azure portal
Aby użyć spisu, śledzenia zmian i funkcje automatyzacji Azure Management aktualizacji maszyn wirtualnych platformy Azure Stack, należy najpierw włączyć te rozwiązania na platformie Azure.

> [!TIP]
> Jeśli masz już te funkcje włączone dla maszyn wirtualnych platformy Azure, używając istniejących poświadczeń LogAnalytics obszaru roboczego. Jeśli masz już LogAnalytics WorkspaceID i klucz podstawowy, którego chcesz używać, przejdź do sekcji [następnej sekcji](./vm-update-management.md#in-the-azure-stack-administration-portal). W przeciwnym razie jest nadal w tej sekcji, aby utworzyć nowy obszar roboczy LogAnalytics i konto usługi automation.

Pierwszym krokiem podczas włączania tych rozwiązań jest [Utwórz obszar roboczy LogAnalytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-quick-create-workspace) w subskrypcji platformy Azure. Obszar roboczy usługi Log Analytics to unikatowe środowisko usługi Log Analytics z własnym repozytorium danych, źródłami danych i rozwiązań. Po utworzeniu obszaru roboczego, należy pamiętać, identyfikator WorkspaceID i klucz. Aby wyświetlić te informacje, przejdź do bloku obszaru roboczego, kliknij **Zaawansowane ustawienia**i przejrzyj **identyfikator obszaru roboczego** i **klucz podstawowy** wartości. 

Następnie należy [Tworzenie konta usługi Automation](https://docs.microsoft.com/azure/automation/automation-create-standalone-account). Konto usługi Automation jest kontenerem dla zasobów usługi Azure Automation. Umożliwia ona rozdzielenie środowisk lub dokładniejsze uporządkowanie przepływów pracy automatyzacji i zasobów. Po utworzeniu konta usługi automation możesz należy włączyć spis, śledzenie zmian i aktualizacji funkcji zarządzania. Aby to zrobić, wykonaj następujące kroki, aby umożliwić każdej funkcji:

1. W witrynie Azure portal przejdź do konta usługi Automation, do którego chcesz używać.

2. Wybierz rozwiązanie, aby włączyć (albo **spisu**, **śledzenie zmian**, lub **rozwiązanie Update management**).

3. Użyj **wybierz obszar roboczy...**  listy rozwijanej, aby wybrać obszar roboczy analizy dzienników do użycia.

4. Sprawdź, czy wszystkie pozostałe informacje są poprawne, a następnie kliknij przycisk **Włącz** Aby włączyć rozwiązanie.

5. Powtórz kroki 2 – 4, aby włączyć wszystkie trzy rozwiązania. 

   [![](media/vm-update-management/1-sm.PNG "Włączanie funkcji konta usługi automation")](media/vm-update-management/1-lg.PNG#lightbox)

### <a name="in-the-azure-stack-administration-portal"></a>W portalu administracyjnym usługi Azure Stack
Po włączeniu rozwiązania usługi Azure Automation w witrynie Azure portal, następnie należy zalogować się do portalu administracyjnego usługi Azure Stack jako administrator w chmurze i Pobierz **aktualizacji baz danych Azure i zarządzanie konfiguracją** i  **Usługa Azure aktualizacji i zarządzania konfiguracją dla systemu Linux** elementów portalu marketplace usługi Azure Stack rozszerzenia. 

   ![Usługa Azure aktualizacji i konfiguracji zarządzania rozszerzenie elementu portalu marketplace](media/vm-update-management/2.PNG) 

## <a name="enable-update-management-for-azure-stack-virtual-machines"></a>Włączanie rozwiązania Update Management dla maszyn wirtualnych usługi Azure Stack
Wykonaj następujące kroki, aby włączyć zarządzanie aktualizacjami dla maszyn wirtualnych platformy Azure Stack.

1. Zaloguj się do portalu użytkowników usługi Azure Stack.

2. W aplikacji portal użytkowników usługi Azure Stack, przejdź do bloku rozszerzeń maszyn wirtualnych, dla których chcesz włączyć te rozwiązania, kliknij przycisk **+ Dodaj**, wybierz opcję **aktualizacji baz danych Azure i zarządzanie konfiguracją** rozszerzenie, a następnie kliknij przycisk **Utwórz**:

   [![](media/vm-update-management/3-sm.PNG "Blok rozszerzenia maszyny Wirtualnej")](media/vm-update-management/3-lg.PNG#lightbox)

3. Podaj utworzony wcześniej identyfikator obszaru roboczego i klucz podstawowy Połącz agenta z obszarem roboczym LogAnalytics, a następnie kliknij przycisk **OK** Aby wdrożyć rozszerzenie.

   [![](media/vm-update-management/4-sm.PNG "Podając identyfikator WorkspaceID i klucz")](media/vm-update-management/4-lg.PNG#lightbox) 

4. Zgodnie z opisem w [dokumentacja zarządzania aktualizacji usługi automation](https://docs.microsoft.com/azure/automation/automation-update-management), musisz włączyć rozwiązania do zarządzania aktualizacjami dla każdej maszyny Wirtualnej, którą chcesz zarządzać. Aby włączyć rozwiązanie dla wszystkich maszyn wirtualnych, które raporty do obszaru roboczego, wybierz pozycję **rozwiązanie Update management**, kliknij przycisk **zarządzać maszynami**, a następnie wybierz pozycję **Włącz na wszystkich dostępnych i przyszłych maszynach** opcji.

   [![](media/vm-update-management/5-sm.PNG "Podając identyfikator WorkspaceID i klucz")](media/vm-update-management/5-lg.PNG#lightbox) 

   > [!TIP]
   > Powtórz ten krok, aby włączyć każde z tych rozwiązań dla tego raportu do obszaru roboczego maszyny wirtualne stosu platformy Azure. 
  
Po włączeniu rozszerzenia aktualizacji baz danych Azure i zarządzanie konfiguracją skanowanie odbywa się dwa razy dziennie dla każdej zarządzanej maszyny Wirtualnej. Interfejs API jest wywoływana co 15 minut, aby wykonać zapytanie o czas ostatniej aktualizacji ustalić, czy stan się zmienił. Jeśli stan się zmienił, inicjowane jest skanowanie pod kątem zgodności.

Po przeskanowaniu maszyn wirtualnych pojawią się one w ramach konta usługi Azure Automation w rozwiązaniu do zarządzania aktualizacjami: 

   [![](media/vm-update-management/6-sm.PNG "Podając identyfikator WorkspaceID i klucz")](media/vm-update-management/6-lg.PNG#lightbox) 

> [!IMPORTANT]
> Może upłynąć od 30 minut do 6 godzin dla pulpitu nawigacyjnego wyświetlić zaktualizowane dane z zarządzanych komputerów.

Maszyny wirtualne Azure Stack mogą być teraz dołączane w zaplanowanych wdrożeń aktualizacji wraz z maszynami wirtualnymi platformy Azure.

## <a name="enable-update-management-using-a-resource-manager-template"></a>Włączanie rozwiązania Update Management przy użyciu szablonu usługi Resource Manager
Jeśli masz dużą liczbę maszyn wirtualnych platformy Azure Stack, możesz użyć [tego szablonu usługi Azure Resource Manager](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/MicrosoftMonitoringAgent-ext-win) łatwo wdrożyć rozwiązanie na maszynach wirtualnych. Szablon wdraża rozszerzenia Microsoft Monitoring Agent do istniejącej maszyny Wirtualnej usługi Azure Stack i dodaje go do istniejącego obszaru roboczego LogAnalytics platformy Azure.
 
## <a name="next-steps"></a>Kolejne kroki
[Optymalizacja wydajności programu SQL Server](azure-stack-sql-server-vm-considerations.md)
