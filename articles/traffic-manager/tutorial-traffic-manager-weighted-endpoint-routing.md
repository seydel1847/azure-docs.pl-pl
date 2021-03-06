---
title: Samouczek — kierowanie ruchu do punktów końcowych z wagami — usługa Azure Traffic Manager
description: W tym artykule zawierającym samouczek opisano sposób kierowania ruchu do punktów końcowych z wagami za pomocą usługi Traffic Manager.
services: traffic-manager
author: KumudD
Customer intent: As an IT Admin, I want to distribute traffic based on the weight assigned to a website endpoint so that I can control the user traffic to a given website.
ms.service: traffic-manager
ms.topic: tutorial
ms.date: 10/15/2018
ms.author: kumud
ms.openlocfilehash: f70f3804bb1c6f385081b56fe6139b1b680a95cf
ms.sourcegitcommit: d61faf71620a6a55dda014a665155f2a5dcd3fa2
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/04/2019
ms.locfileid: "54055017"
---
# <a name="tutorial-control-traffic-routing-with-weighted-endpoints-by-using-traffic-manager"></a>Samouczek: sterowanie routingiem ruchu za pomocą punktów końcowych z wagami przy użyciu usługi Traffic Manager 

W tym samouczku opisano, jak sterować routingiem ruchu użytkowników między punktami końcowymi metodą routingu ważonego za pomocą usługi Azure Traffic Manager. W przypadku tej metody routingu należy przypisać wagi do każdego punktu końcowego w konfiguracji profilu usługi Traffic Manager. Ruch użytkowników jest kierowany zgodnie z wagami przypisanymi do poszczególnych punktów końcowych. Waga jest liczbą całkowitą z zakresu od 1 do 1000. Im większa jest wartość wagi przypisana do punktu końcowego, tym wyższy jest priorytet.

Ten samouczek zawiera informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Tworzenie dwóch maszyn wirtualnych z podstawową witryną internetową w usługach IIS
> * Tworzenie dwóch testowych maszyn wirtualnych, aby zobaczyć usługę Traffic Manager w działaniu
> * Konfigurowanie nazwy DNS dla maszyn wirtualnych z uruchomionymi usługami IIS
> * Tworzenie profilu usługi Traffic Manager.
> * Dodawanie punktów końcowych maszyny wirtualnej do profilu usługi Traffic Manager
> * Sprawdź działanie usługi Traffic Manager.

Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).

## <a name="prerequisites"></a>Wymagania wstępne
Aby zobaczyć usługę Traffic Manager w działaniu, na potrzeby tego samouczka trzeba wdrożyć:
- dwa wystąpienia podstawowych witryn internetowych działających w różnych regionach świadczenia usługi Azure — Wschodnie stany USA i Europa Zachodnia,
- dwie testowe maszyny wirtualne do testowania usługi Traffic Manager — jedną maszynę wirtualną w regionie Wschodnie stany USA i drugą w regionie Europa Zachodnia. Testowe maszyny wirtualne są używane w celu zilustrowania sposobu kierowania ruchu użytkowników przez usługę Traffic Manager do witryny internetowej, która ma wyższą wagę przypisaną do punktu końcowego.

### <a name="sign-in-to-azure"></a>Logowanie do platformy Azure 

Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).

### <a name="create-websites"></a>Tworzenie witryn internetowych

W tej sekcji opisano tworzenie dwóch wystąpień witryny internetowej, które zapewniają dwa punkty końcowe usługi dla profilu usługi Traffic Manager w dwóch regionach platformy Azure. Aby utworzyć te dwie witryny internetowe, wykonaj następujące czynności:
1. Utwórz dwie maszyny wirtualne w celu uruchomienia podstawowej witryny internetowej — jedną w regionie Wschodnie stany USA, a drugą w regionie Europa Zachodnia.
2. Zainstaluj serwer usług IIS na każdej maszynie wirtualnej. Zaktualizuj domyślną stronę internetową, aby informowała o nazwie maszyny wirtualnej, z którą łączy się użytkownik podczas odwiedzania witryny internetowej.

#### <a name="create-vms-for-running-websites"></a>Tworzenie maszyn wirtualnych do uruchamiania witryn internetowych
W tej sekcji utworzysz dwie maszyny wirtualne (*myIISVMEastUS* i *myIISVMWEurope*) w regionach świadczenia usługi Azure Wschodnie stany USA i Europa Zachodnia.

1. W lewym górnym rogu witryny Azure Portal wybierz pozycję **Utwórz zasób** > **Środowisko obliczeniowe** > **Maszyna wirtualna z systemem Windows Server 2016**.
2. W bloku **Podstawowe** wprowadź lub wybierz następujące informacje: Zaakceptuj wartości domyślne pozostałych ustawień, a następnie wybierz pozycję **Utwórz**.

    |Ustawienie|Wartość|
    |---|---|
    |Name (Nazwa)|Wprowadź wartość **myIISVMEastUS**.|
    |Nazwa użytkownika| Wprowadź wybraną nazwę użytkownika.|
    |Hasło| Wprowadź wybrane hasło. Hasło musi mieć co najmniej 12 znaków i spełniać [zdefiniowane wymagania dotyczące złożoności](../virtual-machines/windows/faq.md?toc=%2fazure%2fvirtual-network%2ftoc.json#what-are-the-password-requirements-when-creating-a-vm).|
    |Grupa zasobów| Wybierz pozycję **Nowa**, a następnie wprowadź wartość **myResourceGroupTM1**.|
    |Lokalizacja| Wybierz pozycję **Wschodnie stany USA**.|
    |||
4. Wybierz rozmiar maszyny wirtualnej w obszarze **Wybierz rozmiar**.
5. Wybierz następujące wartości w obszarze **Ustawienia**, a następnie wybierz przycisk **OK**:
    
    |Ustawienie|Wartość|
    |---|---|
    |Sieć wirtualna| Wybierz pozycję **Sieć wirtualna**. W bloku **Tworzenie sieci wirtualnej** w polu **Nazwa** wprowadź wartość **myVNet1**. W polu **Podsieć** wprowadź wartość **mySubnet**.|
    |Sieciowa grupa zabezpieczeń|Wybierz pozycję **Podstawowa**. Z listy rozwijanej **Dodaj publiczne porty wejściowe** wybierz opcje **HTTP** i **RDP**. |
    |Diagnostyka rozruchu|Wybierz opcję **Wyłączone**.|
    |||
6. W obszarze **Utwórz** na stronie **Podsumowanie** wybierz pozycję **Utwórz**, aby rozpocząć wdrażanie maszyny wirtualnej.

7. Wykonaj ponownie kroki 1–6 z następującymi zmianami:

    |Ustawienie|Wartość|
    |---|---|
    |Grupa zasobów | Wybierz pozycję **Nowa**, a następnie wprowadź wartość **myResourceGroupTM2**.|
    |Lokalizacja|Wprowadź wartość **Europa Zachodnia**.|
    |Nazwa maszyny wirtualnej | Wprowadź wartość **myIISVMWEurope**.|
    |Sieć wirtualna | Wybierz pozycję **Sieć wirtualna**. W bloku **Tworzenie sieci wirtualnej** w polu **Nazwa** wprowadź wartość **myVNet2**. W polu **Podsieć** wprowadź wartość **mySubnet**.|
    |||
8. Proces tworzenia maszyny wirtualnej może potrwać kilka minut. Nie wykonuj pozostałych kroków, dopóki obie maszyny wirtualne nie zostaną utworzone.

![Tworzenie maszyny wirtualnej](./media/tutorial-traffic-manager-improve-website-response/createVM.png)

#### <a name="install-iis-and-customize-the-default-webpage"></a>Instalowanie usług IIS i dostosowywanie domyślnej strony internetowej

W tej sekcji zainstalujesz serwer usług IIS na dwóch maszynach wirtualnych — &mdash;myIISVMEastUS i myIISVMWEurope&mdash;, a następnie zaktualizujesz domyślną stronę internetową. Dostosowana strona internetowa wyświetla nazwę maszyny wirtualnej, z którą jest nawiązywane połączenie podczas odwiedzania witryny internetowej z przeglądarki internetowej.

1. Wybierz pozycję **Wszystkie zasoby** w menu po lewej stronie. Z listy zasobów wybierz pozycję **myIISVMEastUS** w grupie zasobów **myResourceGroupTM1**.
2. Na stronie **Przegląd** wybierz pozycję **Połącz**. W polu **Połącz z maszyną wirtualną** wybierz opcję **Pobierz plik RDP**. 
3. Otwórz pobrany plik RDP. Jeśli zostanie wyświetlony monit, wybierz pozycję **Połącz**. Wprowadź nazwę użytkownika i hasło, które zostały określone podczas tworzenia tej maszyny wirtualnej. Może być konieczne wybranie pozycji **Więcej opcji** > **Użyj innego konta**, aby określić poświadczenia wprowadzone podczas tworzenia maszyny wirtualnej. 
4. Kliknij przycisk **OK**.
5. Podczas procesu logowania może pojawić się ostrzeżenie o certyfikacie. Jeśli zostanie wyświetlone ostrzeżenie, wybierz pozycję **Tak** lub **Kontynuuj**, aby nawiązać połączenie.
6. Na pulpicie serwera przejdź do pozycji **Narzędzia administracyjne systemu Windows** > **Menedżer serwera**.
7. Otwórz program Windows PowerShell na maszynie wirtualnej VM1. Użyj poniższych poleceń, aby zainstalować serwer usług IIS i zaktualizować domyślny plik HTM.
    ```powershell-interactive
    # Install IIS
      Install-WindowsFeature -name Web-Server -IncludeManagementTools
    
    # Remove default .htm file
     remove-item  C:\inetpub\wwwroot\iisstart.htm
    
    #Add custom .htm file
     Add-Content -Path "C:\inetpub\wwwroot\iisstart.htm" -Value $("Hello World from " + $env:computername)
    ```

     ![Instalowanie usług IIS i dostosowywanie strony internetowej](./media/tutorial-traffic-manager-improve-website-response/deployiis.png)

8. Zamknij połączenie protokołu RDP z maszyną wirtualną **myIISVMEastUS**.
9. Powtórz kroki 1–8. Utwórz połączenie RDP z maszyną wirtualną **myIISVMWEurope** w grupie zasobów **myResourceGroupTM2**, aby zainstalować usługi IIS i dostosować domyślną stronę internetową.

#### <a name="configure-dns-names-for-the-vms-running-iis"></a>Konfigurowanie nazw DNS dla maszyn wirtualnych z uruchomionymi usługami IIS

Usługa Traffic Manager kieruje ruch użytkowników na podstawie nazwy DNS punktów końcowych usługi. W tej sekcji skonfigurujesz nazwy DNS dla serwerów usług IIS myIISVMEastUS i myIISVMWEurope.

1. Wybierz pozycję **Wszystkie zasoby** w menu po lewej stronie. Z listy zasobów wybierz pozycję **myIISVMEastUS** w grupie zasobów **myResourceGroupTM1**.
2. Na stronie **Przegląd**, w obszarze **Nazwa DNS**, wybierz opcję **Konfiguruj**.
3. Na stronie **Konfiguracja**, w obszarze etykieta nazwy DNS, dodaj unikatową nazwę. Następnie wybierz pozycję **Zapisz**.
4. Powtórz kroki 1–3 dla maszyny wirtualnej o nazwie **myIISVMWEurope** w grupie zasobów **myResourceGroupTM1**.

### <a name="create-a-test-vm"></a>Tworzenie testowej maszyny wirtualnej

W tej sekcji utworzysz maszynę wirtualną *mVMEastUS*. Ta maszyna wirtualna zostanie użyta do przetestowania sposobu, w jaki usługa Traffic Manager kieruje ruch do punktu końcowego witryny internetowej, który ma wyższą wartość wagi.

1. W lewym górnym rogu witryny Azure Portal wybierz pozycję **Utwórz zasób** > **Środowisko obliczeniowe** > **Maszyna wirtualna z systemem Windows Server 2016**.
2. W bloku **Podstawowe** wprowadź lub wybierz następujące informacje: Zaakceptuj wartości domyślne pozostałych ustawień, a następnie wybierz pozycję **Utwórz**:

    |Ustawienie|Wartość|
    |---|---|
    |Name (Nazwa)|Wprowadź wartość **myVMEastUS**.|
    |Nazwa użytkownika| Wprowadź wybraną nazwę użytkownika.|
    |Hasło| Wprowadź wybrane hasło. Hasło musi mieć co najmniej 12 znaków i spełniać [zdefiniowane wymagania dotyczące złożoności](../virtual-machines/windows/faq.md?toc=%2fazure%2fvirtual-network%2ftoc.json#what-are-the-password-requirements-when-creating-a-vm).|
    |Grupa zasobów| Wybierz pozycję **Użyj istniejącej**, a następnie wybierz grupę **myResourceGroupTM1**.|
    |||

4. Wybierz rozmiar maszyny wirtualnej w obszarze **Wybierz rozmiar**.
5. Wybierz następujące wartości w obszarze **Ustawienia**, a następnie wybierz przycisk **OK**:
    |Ustawienie|Wartość|
    |---|---|
    |Sieć wirtualna| Wybierz pozycję **Sieć wirtualna**. W bloku **Tworzenie sieci wirtualnej** w polu **Nazwa** wprowadź wartość **myVNet3**. W polu Podsieć wprowadź wartość **mySubnet**.|
    |Sieciowa grupa zabezpieczeń|Wybierz pozycję **Podstawowa**. Z listy rozwijanej **Dodaj publiczne porty wejściowe** wybierz opcje **HTTP** i **RDP**. |
    |Diagnostyka rozruchu|Wybierz opcję **Wyłączone**.|
    |||

6. W obszarze **Utwórz** na stronie **Podsumowanie** wybierz pozycję **Utwórz**, aby rozpocząć wdrażanie maszyny wirtualnej.
8. W ciągu kilku minut zostanie utworzona maszyna wirtualna. Nie wykonuj pozostałych kroków, dopóki maszyna wirtualna nie zostanie utworzona.

## <a name="create-a-traffic-manager-profile"></a>Tworzenie profilu usługi Traffic Manager
Utwórz profil usługi Traffic Manager, bazując na metodzie routingu **ważonego**.

1. W lewej górnej części ekranu wybierz pozycję **Utwórz zasób** > **Sieć** > **Profil usługi Traffic Manager** > **Utwórz**.
2. W bloku **Tworzenie profilu usługi Traffic Manager** wprowadź lub wybierz poniższe informacje. Zaakceptuj wartości domyślne pozostałych ustawień, a następnie wybierz pozycję **Utwórz**.

    | Ustawienie                 | Wartość                                              |
    | ---                     | ---                                                |
    | Name (Nazwa)                   | Wprowadź unikatową nazwę w obrębie strefy trafficmanager.net. Wynikiem jest nazwa DNS trafficmanager.net, która jest używana do uzyskiwania dostępu do profilu usługi Traffic Manager.                                   |
    | Metoda routingu          | Wybierz **ważoną** metodę routingu.                                       |
    | Subskrypcja            | Wybierz subskrypcję.                          |
    | Grupa zasobów          | Wybierz pozycję **Użyj istniejącej**, a następnie wybierz grupę **myResourceGroupTM1**. |
    |        |   |

    ![Tworzenie profilu usługi Traffic Manager](./media/tutorial-traffic-manager-weighted-endpoint-routing/create-traffic-manager-profile.png)

## <a name="add-traffic-manager-endpoints"></a>Dodawanie punktów końcowych usługi Traffic Manager

Dodaj dwie maszyny wirtualne, na których działają serwery IIS — myIISVMEastUS i myIISVMWEurope, aby skierować do nich ruch użytkowników.

1. Na pasku wyszukiwania portalu wyszukaj nazwę profilu usługi Traffic Manager, który został utworzony w poprzedniej sekcji. Wybierz profil w wyświetlanych wynikach.
2. W bloku **Profil usługi Traffic Manager** w sekcji **Ustawienia** wybierz pozycję **Punkty końcowe** > **Dodaj**.
3. Wprowadź lub wybierz poniższe informacje. Zaakceptuj wartości domyślne pozostałych ustawień, a następnie wybierz pozycję **OK**.

    | Ustawienie                 | Wartość                                              |
    | ---                     | ---                                                |
    | Typ                    | Wprowadź punkt końcowy platformy Azure.                                   |
    | Name (Nazwa)           | Wprowadź wartość **myEastUSEndpoint**.                                        |
    | Typ zasobu docelowego           | Wybierz pozycję **Publiczny adres IP**.                          |
    | Zasób docelowy          | Wybierz publiczny adres IP, aby wyświetlić listę zasobów z publicznymi adresami IP w ramach tej samej subskrypcji. W obszarze **Zasób** wybierz publiczny adres IP o nazwie **myIISVMEastUS-ip**. Jest to publiczny adres IP serwera usług IIS maszyny wirtualnej w regionie Wschodnie stany USA.|
    |  Waga      | Wprowadź wartość **100**.        |
    |        |           |

4. Powtórz kroki 2 i 3, aby dodać inny punkt końcowy o nazwie **myWestEuropeEndpoint** z publicznym adresem IP **myIISVMWEurope-ip**. Ten adres jest skojarzony z serwerem IIS na maszynie wirtualnej o nazwie myIISVMWEurope. W ustawieniu **Waga** wprowadź **25**. 
5.  Po zakończeniu dodawania obu punktów końcowych będą one wyświetlane w profilu usługi Traffic Manager, ze stanem monitorowania **Online**.

## <a name="test-the-traffic-manager-profile"></a>Testowanie profilu usługi Traffic Manager
Aby zobaczyć usługę Traffic Manager w działaniu, wykonaj następujące czynności:
1. Określ nazwę DNS profilu usługi Traffic Manager.
2. Sprawdź działanie usługi Traffic Manager.

### <a name="determine-dns-name-of-traffic-manager-profile"></a>Określanie nazwy DNS profilu usługi Traffic Manager
Dla uproszczenia w tym samouczku użyjesz nazwy DNS profilu usługi Traffic Manager do odwiedzania witryn internetowych. 

Nazwę DNS profilu usługi Traffic Manager można określić w następujący sposób:

1.  Na pasku wyszukiwania portalu wyszukaj nazwę profilu usługi Traffic Manager, który został utworzony w poprzedniej sekcji. W wyświetlonych wynikach wybierz profil usługi Traffic Manager.
1. Wybierz pozycję **Przegląd**.
2. Profil usługi Traffic Manager wyświetli swoją nazwę DNS. We wdrożeniach produkcyjnych można skonfigurować niestandardową nazwę domeny w celu wskazania nazwy domeny usługi Traffic Manager przy użyciu rekordu CNAME systemu DNS.

   ![Nazwa DNS usługi Traffic Manager](./media/tutorial-traffic-manager-improve-website-response/traffic-manager-dns-name.png)

### <a name="view-traffic-manager-in-action"></a>Wyświetlanie informacji o działaniu usługi Traffic Manager
W tej sekcji zobaczysz działanie usługi Traffic Manager. 

1. Wybierz pozycję **Wszystkie zasoby** w menu po lewej stronie. Z listy zasobów wybierz pozycję **myVMEastUS** w grupie zasobów **myResourceGroupTM1**.
2. Na stronie **Przegląd** wybierz pozycję **Połącz**. W polu **Połącz z maszyną wirtualną** wybierz opcję **Pobierz plik RDP**. 
3. Otwórz pobrany plik RDP. Jeśli zostanie wyświetlony monit, wybierz pozycję **Połącz**. Wprowadź nazwę użytkownika i hasło określone podczas tworzenia maszyny wirtualnej. Może być konieczne wybranie pozycji **Więcej opcji** > **Użyj innego konta**, aby określić poświadczenia wprowadzone podczas tworzenia maszyny wirtualnej. 
4. Kliknij przycisk **OK**.
5. Podczas procesu logowania może pojawić się ostrzeżenie o certyfikacie. Jeśli zostanie wyświetlone ostrzeżenie, wybierz pozycję **Tak** lub **Kontynuuj**, aby nawiązać połączenie. 
6. W przeglądarce internetowej na maszynie wirtualnej myVMEastUS wprowadź nazwę DNS profilu usługi Traffic Manager, aby wyświetlić witrynę internetową. Nastąpi przekierowanie do witryny internetowej hostowanej na serwerze usług IIS myIISVMEastUS, ponieważ ma on przypisaną wyższą wartość wagi (**100**). Serwer IIS myIISVMWEurope ma przypisaną niższą wartość wagi punktu końcowego — **25**.

   ![Testowanie profilu usługi Traffic Manager](./media/tutorial-traffic-manager-improve-website-response/eastus-traffic-manager-test.png)
   
## <a name="delete-the-traffic-manager-profile"></a>Usuwanie profilu usługi Traffic Manager
Jeżeli nie potrzebujesz już grup zasobów utworzonych w ramach tego samouczka, możesz je usunąć. Aby to zrobić, wybierz grupę zasobów (**ResourceGroupTM1** lub **ResourceGroupTM2**), a następnie wybierz pozycję **Usuń**.

## <a name="next-steps"></a>Następne kroki

> [!div class="nextstepaction"]
> [Kierowanie ruchu do określonych punktów końcowych na podstawie lokalizacji geograficznej użytkownika](traffic-manager-configure-geographic-routing-method.md)


