---
title: Wdrażanie Avere vFXT dla platformy Azure
description: Kroki, aby wdrożyć klaster vFXT Avere na platformie Azure
author: ekpgh
ms.service: avere-vfxt
ms.topic: conceptual
ms.date: 10/31/2018
ms.author: v-erkell
ms.openlocfilehash: 8e265f2bed480f7b40476e09ab8f442aedcc9dd4
ms.sourcegitcommit: 2469b30e00cbb25efd98e696b7dbf51253767a05
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/06/2018
ms.locfileid: "52999447"
---
# <a name="deploy-the-vfxt-cluster"></a>Wdrażanie klastra vFXT

Najprostszym sposobem utworzenia klastra vFXT na platformie Azure jest do użycia kontrolera klastra. Kontroler klastra jest maszyną Wirtualną, która zawiera wymagane skrypty, szablony i infrastrukturę oprogramowania do tworzenia i zarządzania klastrem vFXT.

Wdrażanie nowego klastra vFXT obejmuje następujące kroki:

1. [Tworzenie kontrolera klastra](#create-the-cluster-controller-vm).
1. Jeśli przy użyciu usługi Azure Blob storage [Tworzenie punktu końcowego magazynu](#create-a-storage-endpoint-if-using-azure-blob) w Twojej sieci wirtualnej.
1. [Połączyć się z kontrolerem klastra](#access-the-controller). Pozostałe kroki te są wykonywane z kontrolera klastra maszyny Wirtualnej. 
1. [Utwórz rolę dostępu](#create-the-cluster-node-access-role) dla węzłów klastra. Podano prototypu.
1. [Dostosowywanie skryptu tworzenia klastra](#edit-the-deployment-script) dla typu vFXT klastra, którą chcesz utworzyć.
1. [Wykonywanie skryptu tworzenia klastra](#run-the-script).

Aby uzyskać więcej informacji na temat kroków wdrażania klastra i planowania, przeczytaj [Planowanie systemu vFXT Avere](avere-vfxt-deploy-plan.md) i [Przegląd wdrażania](avere-vfxt-deploy-overview.md). 

Po wykonaniu instrukcji w tym dokumencie, będziesz mieć sieć wirtualną, podsieć, kontrolera i klaster vFXT, jak pokazano na poniższym diagramie:

![Diagram przedstawiający sieć wirtualna, zawierający opcjonalne blob storage i w podsieci zawierającej trzy pogrupowane maszyn wirtualnych z etykietą vFXT węzły/vFXT klastra i jeden kontroler etykietami klastra maszyny Wirtualnej](media/avere-vfxt-deployment.png)

Przed rozpoczęciem upewnij się, że zostały rozwiązane te wymagania wstępne:  

1. [Nowa subskrypcja](avere-vfxt-prereqs.md#create-a-new-subscription)
1. [Uprawnienia właściciela do subskrypcji](avere-vfxt-prereqs.md#configure-subscription-owner-permissions)
1. [Limit przydziału dla klastra vFXT](avere-vfxt-prereqs.md#quota-for-the-vfxt-cluster)

Opcjonalnie możesz utworzyć rolę węzła klastra [przed](avere-vfxt-pre-role.md) Tworzenie kontrolera klastra, ale jest prostsze zrobić to później.

## <a name="create-the-cluster-controller-vm"></a>Tworzenie maszyny Wirtualnej kontrolera klastra

Pierwszym krokiem jest do utworzenia maszyny wirtualnej, która spowoduje to utworzenie i skonfigurowanie vFXT węzłów klastra. 

Kontroler klastra jest Maszynę wirtualną systemu Linux za pomocą oprogramowania do tworzenia klastra vFXT Avere i skrypty wstępnie zainstalowane. Nie potrzebuje przetwarzania zasilania lub miejsce do magazynowania, dzięki czemu można wybrać opcje niedrogie. Ta maszyna wirtualna będzie służyć od czasu do czasu przez cały czas życia klastra vFXT.

Istnieją dwie metody, aby utworzyć kontroler klastra maszyny Wirtualnej. [Szablonu usługi Azure Resource Manager](#create-controller---arm-template) podano [poniżej](#create-controller---arm-template) Aby uprościć proces, ale można również utworzyć kontroler z [obrazu z witryny Azure Marketplace](#create-controller---azure-marketplace-image). 

Można utworzyć nową grupę zasobów w ramach tworzenia kontrolera.

> [!TIP]
>
> Zdecyduj, czy mają być Użyj publicznego adresu IP na kontrolerze klastra. Publiczny adres IP zapewnia łatwiejszy dostęp do klastra vFXT, ale tworzy mały zagrożenie bezpieczeństwa.
>
>  * Publiczny adres IP na kontrolerze klastra umożliwia przy użyciu go jako hosta szybkie łączenie z klastrem vFXT Avere z poza podsieci prywatnej.
>  * Jeśli nie skonfigurowano publiczny adres IP na kontrolerze, musisz podać innego hosta szybkie, połączenie sieci VPN lub usługi ExpressRoute do dostępu do klastra. Na przykład utworzyć kontroler sieci wirtualnej, który ma skonfigurowane połączenia sieci VPN.
>  * Jeśli utworzysz kontroler z publicznym adresem IP, należy chronić maszyny Wirtualnej kontrolera z sieciową grupą zabezpieczeń. Zezwalaj na dostęp tylko za pośrednictwem portu 22, aby zapewnić dostęp do Internetu.

### <a name="create-controller---resource-manager-template"></a>Tworzenie kontrolera — szablon usługi Resource Manager

Aby utworzyć węzeł klastra kontroler z poziomu portalu, kliknij poniższy przycisk "Wdróż na platformie Azure". Wdróż ten szablon umożliwia utworzenie maszyny Wirtualnej, która będzie tworzył i zarządzał Avere vFXT klastra.

[![przycisk, aby utworzyć kontroler](media/deploytoazure.png)](https://ms.portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FAvere%2Fmaster%2Fsrc%2Fvfxt%2Fazuredeploy.json)

Podaj następujące informacje.

W **BASIC** sekcji:  

* **Subskrypcja** klastra
* **Grupa zasobów** klastra 
* **Lokalizacja** 

W **ustawienia** sekcji:

* Czy należy utworzyć nową sieć wirtualną

  * Jeśli tworzysz nową sieć wirtualną, kontrolera klastra będzie można przypisać publiczny adres IP, aby przejść do niego. Sieciowa grupa zabezpieczeń również jest tworzony dla tej sieci wirtualnej, która ogranicza ruch przychodzący na tylko port 22.
  * Jeśli chcesz połączyć się z kontrolerem klastra za pomocą usługi ExpressRoute lub sieci VPN, należy ustawić tę wartość na `false` i określ istniejącej sieci wirtualnej w pozostałych polach. Kontroler klaster będzie używać tej sieci wirtualnej komunikacji sieciowej. 

* Grupa zasobów sieci wirtualnej, nazwę i nazwę podsieci — wpisz nazwy istniejących zasobów (w przypadku korzystania z istniejącej sieci wirtualnej) lub nowych nazw w przypadku tworzenia nowej sieci wirtualnej
* **Nazwa kontrolera** — Ustaw nazwę maszyny Wirtualnej kontrolera
* Nazwa użytkownika administratora kontrolera — wartość domyślna to `azureuser`
* Klucz SSH - Wklej klucz publiczny do skojarzenia z nazwą użytkownika administratora. Odczyt [sposób tworzenia i używania kluczy SSH](https://docs.microsoft.com/azure/virtual-machines/linux/ssh-from-windows) Jeśli potrzebujesz pomocy.

W obszarze **warunków i postanowień**: 

* Przeczytaj warunki użytkowania usługi i kliknij pole wyboru, aby je zaakceptować. 

  > [!NOTE] 
  > Jeśli nie jesteś właścicielem subskrypcji, mieć właściciela, zaakceptuj warunki dla przez następujące wstępnie wymagane kroki [zaakceptować warunki wcześniej oprogramowania](avere-vfxt-prereqs.md#accept-software-terms-in-advance). 


Kliknij przycisk **zakupu** po zakończeniu. Po pięciu lub sześciu minut Twój węzeł kontroler zostanie uruchomiona.

Odwiedź stronę danych wyjściowych, aby zebrać informacje kontrolera, które należy utworzyć klaster. Odczyt [informacje niezbędne do utworzenia klastra](#information-needed-to-create-the-cluster) Aby dowiedzieć się więcej.

### <a name="create-controller---azure-marketplace-image"></a>Tworzenie kontrolera - obrazu z witryny Azure Marketplace

Znajdź szablon kontrolera, wyszukując nazwę w portalu Azure Marketplace ``Avere``. Wybierz **vFXT Avere kontrolera Azure** szablonu.

Jeśli jeszcze tego nie zrobiono, należy zaakceptować warunki i włączyć dostęp programowy do obrazu z witryny Marketplace, klikając pozycję "chcesz wdrożyć programowo?" Link poniżej **Utwórz** przycisku.

![Zrzut ekranu przedstawiający link do dostęp programowy, w której znajduje się poniżej przycisku Utwórz](media/avere-vfxt-deploy-programmatically.png)

Kliknij przycisk **Włącz** przycisk i zapisać ustawienie.

![Zrzut ekranu przedstawiający myszy kliknij, aby włączyć dostęp programowy](media/avere-vfxt-enable-program.png)

Powrót na stronę główną programu **vFXT Avere kontrolera Azure** szablon i kliknij przycisk **Utwórz**. 

W pierwszym panelu wypełnić lub potwierdź następujące podstawowe opcje:

* **Subskrypcja**
* **Grupa zasobów** (wprowadź nową nazwę, jeśli chcesz utworzyć nową grupę).
* **Nazwa maszyny wirtualnej** — nazwa kontrolera
* **Region**
* **Opcje dostępności** — nadmiarowość nie jest wymagana
* **Obraz** -obrazu węzła Avere vFXT kontrolera
* **Rozmiar** — pozostaw wartość domyślną, lub wybierz inny typ niedrogie
* **Konto administratora** — Ustaw jak zalogować się do kontrolera klastra: 
  * Wybierz nazwę użytkownika/hasło lub klucz publiczny SSH (zalecane).
  
    > [!TIP] 
    > Klucz SSH jest bezpieczniejszy. Odczyt [sposób tworzenia i używania kluczy SSH](https://docs.microsoft.com/azure/virtual-machines/linux/ssh-from-windows) Jeśli potrzebujesz pomocy. 
  * Określ nazwę użytkownika 
  * Wklej klucz SSH lub wprowadź i Potwierdź hasło
* **Reguły portów wejściowych** — Jeśli to ustawienie przy użyciu publicznego adresu IP, otwarty port 22 (SSH)

Kliknij przycisk **dalej** można ustawić opcje dysku:

* **Typ dysku systemu operacyjnego** — wartość domyślną dysk twardy jest wystarczająca
* **Korzystać z dysków niezarządzanych** — nie jest konieczna
* **Dyski z danymi** — nie należy używać

Kliknij przycisk **dalej** dla opcji sieciowych:

* **Sieć wirtualna** — wybierz sieć wirtualną, kontrolera lub wprowadź nazwę, aby utworzyć nową sieć wirtualną. Jeśli nie chcesz używać publiczny adres IP kontrolera, należy wziąć pod uwagę lokalizowania go w sieci wirtualnej usługi ExpressRoute lub innej metody dostępu już skonfigurowane.
* **Podsieci** — Wybierz podsieć, w ramach sieci wirtualnej (opcjonalnie). Jeśli tworzysz nową sieć wirtualną, możesz utworzyć nową podsieć w tym samym czasie.
* **Publiczny adres IP** — Jeśli chcesz użyć publicznego adresu IP, możesz je określić w tym miejscu. 
* **Sieciowa grupa zabezpieczeń** -pozostaw ustawienie domyślne (**podstawowe**) 
* **Publiczne porty wejściowe** — Jeśli to ustawienie przy użyciu publicznego adresu IP, użyć tej kontrolki, aby zezwolić na dostęp z ruch SSH. 
* **Przyspieszoną sieć** jest niedostępna dla tej maszyny Wirtualnej.

Kliknij przycisk **dalej** można ustawić opcji zarządzania:

* **Diagnostyka rozruchu** — Zmień **wyłączone**
* **System operacyjny gościa diagnostyki** — pozostaw wyłączone
* **Konto magazynu diagnostyki** — opcjonalnie wybierz lub określ nowe konto, do przechowywania informacji diagnostycznych.
* **Tożsamość usługi zarządzanej** — tę opcję, aby zmienić **na**, co powoduje utworzenie jednostki usługi Azure AD dla kontrolera klastra.
* **Automatyczne zamykanie** -pozostawić wyłączone 

W tym momencie możesz kliknąć pozycję **przeglądu + Utwórz** Jeśli nie chcesz używać tagów wystąpienia. W przeciwnym razie kliknij przycisk **dalej** dwa razy, aby pominąć **config gościa** strony i przejść na stronę tagów. Po zakończeniu istnieje, kliknij **przeglądu + Utwórz**. 

Po zweryfikowaniu wybrane opcje, kliknij przycisk **Utwórz** przycisku.  

Tworzenie trwa pięciu lub sześciu minut.

## <a name="create-a-storage-endpoint-if-using-azure-blob"></a>Tworzenie punktu końcowego magazynu (w przypadku korzystania z obiektów Blob platformy Azure)

Jeśli używasz usługi Azure Blob storage do obsługi magazynu danych zaplecza, należy utworzyć punkt końcowy usługi magazynu w sieci wirtualnej. To [punktu końcowego usługi](https://docs.microsoft.com/azure/virtual-network/virtual-network-service-endpoints-overview) utrzymuje ruchu w usłudze Azure Blob lokalnego zamiast przesyłać go przez internet.

1. Z poziomu portalu, kliknij przycisk **sieci wirtualne** po lewej stronie.
1. Wybierz sieć wirtualną dla kontrolera. 
1. Kliknij przycisk **punkty końcowe usługi** po lewej stronie.
1. Kliknij przycisk **Dodaj** u góry.
1. Pozostaw usługę jako ``Microsoft.Storage`` i wybierz podsieć kontrolera.
1. Kliknij u dołu, **Dodaj**.

  ![Azure portal zrzut ekranu z adnotacjami, aby uzyskać instrukcje tworzenia punktu końcowego usługi](media/avere-vfxt-service-endpoint.png)

## <a name="information-needed-to-create-the-cluster"></a>Informacje wymagane do utworzenia klastra

Po utworzeniu kontroler klastra, upewnij się, że masz informacje potrzebne do następnych kroków. 

Informacje wymagane do połączenia z kontrolerem: 

* Nazwa użytkownika kontrolera i (hasła lub klucza SSH)
* Adres IP kontrolera lub innej metody, aby połączyć się z kontrolerem maszyny Wirtualnej

Informacje o wymaganych przez klaster: 

* Nazwa grupy zasobów
* Lokalizacja platformy Azure 
* Nazwa sieci wirtualnej
* Nazwa podsieci
* Nazwa roli węzła klastra — ta nazwa jest ustawiona po utworzeniu tej roli, opisano [poniżej](#create-the-cluster-node-access-role)
* Nazwa konta magazynu, w przypadku tworzenia kontenera obiektów Blob

Jeśli węzeł kontrolera jest tworzona przy użyciu szablonu usługi Resource Manager, możesz pobrać informacje z [wynik szablonu](#find-template-output). 

Jeśli używasz obrazu z witryny Azure Marketplace do tworzenia kontrolera podanych większość z tych elementów bezpośrednio. 

Znajdź wszystkie brakujące elementy, przechodząc do strony informacji maszyny Wirtualnej kontrolera. Na przykład kliknij pozycję **wszystkie zasoby** i nazwy kontrolera, a następnie kliknij nazwę kontrolera, aby wyświetlić jego szczegóły.

### <a name="find-template-output"></a>Znajdź wynik szablonu

Aby znaleźć te informacje z usługi Resource Manager wynik szablonu, wykonaj poniższą procedurę:

1. Przejdź do grupy zasobów dla kontrolera sieci klastra.

1. Po lewej stronie kliknij pozycję **wdrożeń**, a następnie **Microsoft.Template**.

   ![Portal stronie grupy zasobów z wdrożeniami wybrane po lewej i wyświetlanie Microsoft.Template w tabeli pod nazwą wdrożenia](media/avere-vfxt-deployment-template.png)

1. Po lewej stronie kliknij pozycję **dane wyjściowe**. Skopiuj wartości z każdego pola. 

   ![dane wyjściowe strony SSHSTRING RESOURCE_GROUP, lokalizacji, sieci, PODSIECI i SUBNET_ID wyświetlane w polach na prawo od etykiet](media/avere-vfxt-template-outputs.png)

## <a name="access-the-controller"></a>Dostęp do kontrolera

Aby wykonać pozostałe kroki wdrażania, musisz połączyć się z kontrolerem klastra.

1. Metody, aby połączyć się z kontrolerem sieci klastra zależy od konfiguracji.

   * Jeśli kontroler ma publiczny adres IP protokołu SSH do adresu IP kontrolera, jako nazwa użytkownika administratora należy ustawić (na przykład ``ssh azureuser@40.117.136.91``).
   * Jeśli kontrolera nie ma publicznego adresu IP, należy użyć sieci VPN lub [ExpressRoute](https://docs.microsoft.com/azure/expressroute/) połączenia z siecią wirtualną.

1. Po zalogowaniu się do kontrolera, uwierzytelnianie, uruchamiając `az login`. Skopiuj kod uwierzytelniania podany w powłoce, a następnie użyć przeglądarki internetowej, aby załadować [ https://microsoft.com/devicelogin ](https://microsoft.com/devicelogin) i Uwierzytelnij się przy użyciu systemu Microsoft. Zwróć się do powłoki o potwierdzenie.

   ![Dane wyjściowe wiersza polecenia dla polecenia "AZ login", wyświetlające kod browser link i uwierzytelniania](media/avere-vfxt-azlogin.png)

1. Dodaj swoją subskrypcję, uruchamiając następujące polecenie, przy użyciu swojego Identyfikatora subskrypcji:  ```az account set --subscription YOUR_SUBSCRIPTION_ID```

## <a name="create-the-cluster-node-access-role"></a>Tworzenie roli dostęp do węzła klastra

> [!NOTE] 
> * Jeśli nie jesteś właścicielem subskrypcji, a rola nie został już utworzony, mają właściciela subskrypcji, wykonaj następujące kroki, lub użyj procedury [tworzenie roli dostęp do środowiska uruchomieniowego klastra vFXT Avere bez kontrolera](avere-vfxt-pre-role.md).
> 
> * Użytkownicy wewnętrzni firmy Microsoft należy używać istniejącej roli o nazwie "Operator środowiska uruchomieniowego klastra Avere" zamiast próby, aby je utworzyć. 

[Kontrola dostępu oparta na rolach](https://docs.microsoft.com/azure/role-based-access-control/) (RBAC) umożliwia węzłów klastra vFXT autoryzacji do wykonania niezbędnych zadań.  

Jako część normalnego vFXT operacji klastra vFXT poszczególne węzły muszą wykonywać następujące czynności odczytu właściwości zasobów platformy Azure, zarządzania magazynem i kontrolować ustawienia interfejsu sieciowego w innych węzłach. 

1. Na kontrolerze, otwórz ``/avere-cluster.json`` plik w edytorze.

   ![Konsola pokazująca, że lista, polecenie, a następnie "vi /avere-cluster.json"](media/avere-vfxt-open-role.png)

1. Edytuj plik Uwzględnij identyfikator swojej subskrypcji i Usuń wiersz powyżej. Zapisz plik jako ``avere-cluster.json``.

   ![Konsoli Edytor tekstu, identyfikator subskrypcji i "Usuń ten wiersz" wybrane do usunięcia](media/avere-vfxt-edit-role.png)

1. Użyj tego polecenia, aby utworzyć rolę:  

   ```bash
   az role definition create --role-definition /avere-cluster.json
   ```

Nazwa roli zostanie przekazany do skryptu tworzenia klastra w następnym kroku. 

## <a name="create-nodes-and-configure-the-cluster"></a>Utwórz węzły i skonfiguruj klaster

Aby utworzyć klaster vFXT Avere, edytować jeden z przykładowych skryptach uwzględnione na kontrolerze i ma ją uruchomić. Przykładowe skrypty znajdują się w katalogu głównym (`/`) na kontrolerze klastra.

* Jeśli chcesz utworzyć kontener obiektów Blob jako system magazynu zaplecza Avere vFXT, użyj ``create-cloudbacked-cluster`` skryptu.

* Jeśli magazyn zostanie dodany później, należy użyć ``create-minimal-cluster`` skryptu.

> [!TIP]
> Skrypty prototypu do dodawania węzłów i niszczenie vFXT klastra są dołączone do dodatków `/` katalogu kontrolera klastra maszyny Wirtualnej.

### <a name="edit-the-deployment-script"></a>Edytuj skrypt wdrażania

Otwórz przykładowy skrypt w edytorze. Warto zapisać skrypt dostosowany pod inną nazwą, aby uniknąć zastąpienia oryginalnego przykładu.

Wprowadź wartości dla tych zmiennych skryptu.

* Nazwa grupy zasobów

  * Jeśli używasz składniki sieci i magazynu, które znajdują się w różnych grupach zasobów, usuń znaczniki komentarza zmienne i również dostarczyć tych nazw. 

```python
# Resource groups
# At a minimum specify the resource group.  If the network resources live in a
# different group, specify the network resource group.  Likewise for the storage
# account resource group.
RESOURCE_GROUP=
#NETWORK_RESOURCE_GROUP=
#STORAGE_RESOURCE_GROUP=
```

* Nazwa lokalizacji
* Nazwa sieci wirtualnej
* Nazwa podsieci
* Usługa Azure AD środowiska uruchomieniowego Nazwa roli — po wykonaniu w przykładzie w [tworzenie roli dostęp do węzła klastra](#create-the-cluster-node-access-role), użyj ``avere-cluster``. 
* Nazwa konta magazynu (w przypadku tworzenia nowego kontenera obiektów Blob)
* Nazwa klastra — w tej samej grupie zasobów nie może mieć dwa klastry vFXT o takiej samej nazwie. Nadaj każdy klaster unikatową nazwę dla najlepszym rozwiązaniem.
* Hasło administracyjne — wybrać bezpieczne hasło do monitorowania i administrowania klastrem. To hasło jest przypisane do użytkownika ``admin``. 
* Węzeł typu wystąpienia - zobacz [rozmiary węzłów vFXT](avere-vfxt-deploy-plan.md#vfxt-node-sizes) informacji
* Rozmiar pamięci podręcznej węzła — zobacz [rozmiary węzłów vFXT](avere-vfxt-deploy-plan.md#vfxt-node-sizes) informacji

Zapisz plik i zamknij.

### <a name="run-the-script"></a>Uruchamianie skryptu

Uruchom skrypt, wpisując nazwę pliku, który został utworzony. (Przykład: `./create-cloudbacked-cluster-west1`)  

> [!TIP]
> Należy rozważyć uruchomienie tego polecenia wewnątrz [terminalu multiplekser](http://linuxcommand.org/lc3_adv_termmux.php) takich jak `screen` lub `tmux` w przypadku, gdy połączenie zostanie utracone.  

Dane wyjściowe również jest rejestrowany wpis `~/vfxt.log`.

Po ukończeniu działania skryptu, skopiuj adres IP zarządzania, który jest niezbędny do administrowania klastrami.

![Dane wyjściowe wiersza polecenia skryptu wyświetlanie adres IP zarządzania blisko końca](media/avere-vfxt-mgmt-ip.png)

> [!IMPORTANT] 
> Jeśli utworzono nowy kontener obiektów Blob, może być zaszyfrowany przy użyciu domyślnego klucza, który nie został zapisany poza klastrem. Aby w kontenerze można przechowywać dane, należy albo Pobierz plik klucza odzyskiwania lub Utwórz klucz szyfrowania i zapisać swój plik odzyskiwania w trwałych lokalizacji. 
> 
> Jeśli używasz domyślnego klucza bez pobierania pliku odzyskiwania istnieje możliwość utraty dostępu do zaszyfrowanych danych w filtr podstawowych obiektów Blob, jeśli klaster vFXT zniszczone lub utraty.
>
> Jeśli skrypt zawiera `WARNING` wiadomości, takich jak te zaznaczona kółkiem na zrzucie ekranu poniżej, postępuj zgodnie z instrukcjami w [skonfigurować magazyn](avere-vfxt-add-storage.md) Pobierz plik klucza, lub Utwórz nowy klucz kontenera obiektów Blob. Użyj narzędzia konfiguracji klastra, Avere Panelu sterowania.

![Dane wyjściowe wiersza polecenia skryptu, wyświetlając komunikaty ostrzegawcze o utworzenie nowego klucza szyfrowania](media/avere-vfxt-key-warning.png)

## <a name="next-step"></a>Następny krok

Teraz, gdy klaster działa, i znasz jego adres IP zarządzania, możesz [nawiązać połączenie za pomocą narzędzia konfiguracji klastra](avere-vfxt-cluster-gui.md) Aby włączyć obsługę, Dodaj magazyn, jeśli potrzebne lub adresie domyślnego klucza szyfrowania na nowego magazynu obiektów Blob.
