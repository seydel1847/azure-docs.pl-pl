---
title: Tworzenie obszaru deweloperskiego Kubernetes w chmurze przy użyciu platformy .NET Core i programu VS Code | Microsoft Docs
titleSuffix: Azure Dev Spaces
services: azure-dev-spaces
ms.service: azure-dev-spaces
ms.component: azds-kubernetes
author: zr-msft
ms.author: zarhoads
ms.date: 09/26/2018
ms.topic: tutorial
description: Szybkie tworzenie w środowisku Kubernetes za pomocą kontenerów i mikrousług na platformie Azure
keywords: Docker, Kubernetes, Azure, AKS, Azure Kubernetes Service, containers
ms.openlocfilehash: b5de5ccdf98d6d0a2952a694a253feaac9d6e07d
ms.sourcegitcommit: b254db346732b64678419db428fd9eb200f3c3c5
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2018
ms.locfileid: "53413629"
---
# <a name="get-started-on-azure-dev-spaces-with-net-core"></a>Rozpoczęcie pracy w usłudze Azure Dev Spaces za pomocą platformy .NET Core

Ten przewodnik zawiera informacje na temat wykonywania następujących czynności:

- Tworzenie środowiska Kubernetes na platformie Azure zoptymalizowanego pod kątem programowania — _przestrzeń deweloperów_.
- Iteracyjne tworzenie kodu w kontenerach przy użyciu programu VS Code i wiersza polecenia.
- Efektywne tworzenie i testowanie kodu w środowisku zespołu.

> [!Note]
> **Jeśli utkniesz** w dowolnym momencie, zobacz sekcję [Rozwiązywanie problemów](troubleshooting.md) lub prześlij komentarz na tej stronie.

Teraz możesz przystąpić do tworzenia obszaru deweloperskiego Kubernetes na platformie Azure.

## <a name="install-the-azure-cli"></a>Zainstaluj interfejs wiersza polecenia platformy Azure
Usługa Azure Dev Spaces wymaga minimalnej konfiguracji komputera lokalnego. Większość ustawień obszaru deweloperskiego jest przechowywana w chmurze i udostępniana innym użytkownikom. Na komputerze lokalnym może być uruchomiony system Windows, Mac lub Linux. W przypadku systemu Linux obsługiwane są następujące dystrybucje: Ubuntu (18.04, 16.04 i 14.04), Debian 8 i 9, RHEL 7, Fedora 26 +, CentOS 7, openSUSE 42.2 i SLES 12.

Zacznij od pobrania i uruchomienia [interfejsu wiersza polecenia platformy Azure](/cli/azure/install-azure-cli?view=azure-cli-latest). 

> [!IMPORTANT]
> Jeśli masz już zainstalowany interfejs wiersza polecenia platformy Azure, upewnij się, że używasz wersji 2.0.43 lub nowszej.

### <a name="sign-in-to-azure-cli"></a>Logowanie do interfejsu wiersza polecenia platformy Azure
Zaloguj się do platformy Azure. W oknie terminala wpisz następujące polecenie:

```cmd
az login
```

> [!Note]
> Jeśli nie masz subskrypcji platformy Azure, możesz utworzyć [bezpłatne konto](https://azure.microsoft.com/free).

#### <a name="if-you-have-multiple-azure-subscriptions"></a>Jeśli masz wiele subskrypcji platformy Azure...
Możesz wyświetlić swoje subskrypcje, uruchamiając polecenie: 

```cmd
az account list
```
Znajdź subskrypcję, która w danych wyjściowych JSON ma wartość `isDefault: true`.
Jeśli nie jest to subskrypcja, której chcesz użyć, możesz zmienić subskrypcję domyślną:

```cmd
az account set --subscription <subscription ID>
```

## <a name="create-a-kubernetes-cluster-enabled-for-azure-dev-spaces"></a>Tworzenie klastra Kubernetes obsługującego usługę Azure Dev Spaces

W wierszu polecenia utwórz grupę zasobów. Użyj jednego z aktualnie obsługiwanych regionów (EastUS, EastUS2, CentralUS, WestUS2, WestEurope, SoutheastAsia, CanadaCentral lub CanadaEast).

```cmd
az group create --name MyResourceGroup --location <region>
```

Utwórz klaster Kubernetes za pomocą następującego polecenia:

```cmd
az aks create -g MyResourceGroup -n MyAKS --location <region> --kubernetes-version 1.10.9 --enable-addons http_application_routing --generate-ssh-keys
```

Utworzenie klastra trwa kilka minut.

### <a name="configure-your-aks-cluster-to-use-azure-dev-spaces"></a>Konfigurowanie klastra usługi AKS do korzystania z usługi Azure Dev Spaces

Wpisz następujące polecenie interfejsu wiersza polecenia platformy Azure, podając grupę zasobów, która zawiera klaster usługi AKS, oraz nazwę klastra usługi AKS. Polecenie konfiguruje na klastrze obsługę usługi Azure Dev Spaces.

   ```cmd
   az aks use-dev-spaces -g MyResourceGroup -n MyAKS
   ```
   
> [!IMPORTANT]
> Proces konfiguracji usługi Azure Dev Spaces spowoduje usunięcie przestrzeni nazw `azds` w klastrze, jeśli taka istnieje.

## <a name="get-kubernetes-debugging-for-vs-code"></a>Uzyskiwanie debugowania rozwiązania Kubernetes dla programu VS Code
Rozbudowane funkcje, takie jak debugowanie rozwiązania Kubernetes, są dostępne dla deweloperów platformy .NET Core i środowiska Node.js korzystających z programu VS Code.

1. Jeśli nie masz programu [VS Code](https://code.visualstudio.com/Download), zainstaluj go.
1. Pobierz i zainstaluj [rozszerzenie usługi Azure Dev Spaces dla programu VS](https://marketplace.visualstudio.com/items?itemName=azuredevspaces.azds). Kliknij pozycję Zainstaluj najpierw na stronie rozszerzenia w witrynie Marketplace, a następnie w programie VS Code. 

## <a name="create-a-web-app-running-in-a-container"></a>Tworzenie aplikacji internetowej uruchomionej w kontenerze

W tej sekcji utworzysz aplikację internetową ASP.NET Core i uruchomisz ją w kontenerze w środowisku Kubernetes.

### <a name="create-an-aspnet-core-web-app"></a>Tworzenie aplikacji internetowej ASP.NET Core
Jeśli masz zainstalowaną platformę [.NET Core](https://www.microsoft.com/net), możesz szybko utworzyć aplikację internetową ASP.NET Core w folderze o nazwie `webfrontend`.
    
```cmd
dotnet new mvc --name webfrontend
```

Możesz też **pobrać przykładowy kod z serwisu GitHub**. Otwórz stronę https://github.com/Azure/dev-spaces i wybierz pozycję **Clone or Download** (Sklonuj lub pobierz). Repozytorium GitHub zostanie pobrane do środowiska lokalnego. Kod używany w tym przewodniku znajduje się w lokalizacji `samples/dotnetcore/getting-started/webfrontend`.

## <a name="preparing-code-for-docker-and-kubernetes-development"></a>Przygotowywanie kodu do opracowywania na platformie Docker i Kubernetes
W tej chwili masz podstawową aplikację internetową, która działa lokalnie. Teraz konteneryzujesz ją, tworząc zasoby, które definiują kontener aplikacji i sposób jego wdrażania na platformie Kubernetes. To zadanie łatwo wykonać za pomocą usługi Azure Dev Spaces: 

1. Uruchom program VS Code i otwórz folder `webfrontend`. (Możesz zignorować wszystkie domyślne monity o dodanie zasobów debugowania lub przywrócenie projektu).
1. Otwórz zintegrowany terminal w programie VS Code (przy użyciu menu **Widok > Zintegrowany terminal**).
1. Uruchom następujące polecenie (upewnij się, że bieżący folder to **webfrontend**):

    ```cmd
    azds prep --public
    ```

Polecenie `azds prep` interfejsu wiersza polecenia platformy Azure generuje zasoby platformy Docker i Kubernetes z ustawieniami domyślnymi:
* Plik `./Dockerfile` opisuje obraz kontenera aplikacji oraz sposób kompilowania kodu źródłowego i uruchamiania go w kontenerze.
* [Pakiet Helm](https://docs.helm.sh) w folderze `./charts/webfrontend` opisuje, jak wdrożyć kontener na platformie Kubernetes.

Na razie nie trzeba rozumieć pełnej zawartości tych plików. Warto jednak wspomnieć, że **te same zasoby konfiguracji jako kodu platformy Kubernetes i Docker mogą być używane od etapu opracowywania po etap produkcyjny, co zapewnia większą spójność w różnych środowiskach.**
 
Polecenie `prep` generuje również plik o nazwie `./azds.yaml`. Jest to plik konfiguracji usługi Azure Dev Spaces. Uzupełnia on artefakty platformy Docker i Kubernetes o dodatkową konfigurację zapewniającą środowisko programowania przyrostowego na platformie Azure.

## <a name="build-and-run-code-in-kubernetes"></a>Kompilowanie i uruchamianie kodu na platformie Kubernetes
Teraz uruchomimy nasz kod! W oknie terminalu uruchom to polecenie z **głównego folderu kodu**, WebFrontEnd:

```cmd
azds up
```

Śledź dane wyjściowe polecenia — wraz z postępem zauważysz kilka rzeczy:
- Kod źródłowy jest synchronizowany z przestrzenią deweloperów na platformie Azure.
- Obraz kontenera jest tworzony na platformie Azure, zgodnie z tym, co określają elementy zawartości aparatu Docker w folderze kodu.
- Tworzone są obiekty Kubernetes, które wykorzystują obraz kontenera, zgodnie z tym, co określa plan narzędzia Helm w folderze kodu.
- Wyświetlane są informacje o punktach końcowych kontenera. W tym przypadku spodziewamy się publicznego adresu URL HTTP.
- Zakładając, że powyższe etapy zakończą się powodzeniem, podczas uruchamiania kontenera powinny być widoczne dane wyjściowe `stdout` (i `stderr`).

> [!Note]
> Te kroki będą trwać dłużej podczas pierwszego uruchomienia polecenia `up`, ale kolejne uruchomienia powinny być szybsze.

### <a name="test-the-web-app"></a>Testowanie aplikacji internetowej
Przeskanuj dane wyjściowe konsoli w poszukiwaniu informacji o publicznym adresie URL, który został utworzony za pomocą polecenia `up`. Będzie on mieć postać: 

```
(pending registration) Service 'webfrontend' port 'http' will be available at <url>
Service 'webfrontend' port 80 (TCP) is available at http://localhost:<port>
```

Otwórz ten adres URL w oknie przeglądarki — aplikacja internetowa powinna zostać załadowana. Podczas wykonywania kontenera dane wyjściowe `stdout` i `stderr` są przesyłane strumieniowo do okna terminalu.

> [!Note]
> Przy pierwszym uruchomieniu przygotowanie publicznego serwera DNS może potrwać kilka minut. Jeśli publiczny adres URL nie zostanie rozpoznany, możesz użyć alternatywnego adresu URL http://localhost:<portnumber>, który jest wyświetlany w danych wyjściowych konsoli. Jeśli używasz adresu URL hosta lokalnego, może się wydawać, że kontener działa lokalnie, ale faktycznie jest on uruchamiany w usłudze AKS. Dla Twojej wygody i ułatwienia interakcji z usługą z komputera lokalnego usługa Azure Dev Spaces tworzy tymczasowy tunel SSH do kontenera uruchomionego na platformie Azure. Później, gdy rekord DNS będzie gotowy, możesz wrócić i wypróbować publiczny adres URL.

### <a name="update-a-content-file"></a>Aktualizowanie pliku zawartości
Usługa Azure Dev Spaces umożliwia nie tylko uruchamianie kodu w środowisku Kubernetes — pozwala też szybko i wielokrotnie wyświetlać efekt zmian wprowadzonych w kodzie w środowisku Kubernetes w chmurze.

1. Znajdź plik `./Views/Home/Index.cshtml` i zmień kod HTML. Na przykład zmień wiersz 70 z `<h2>Application uses</h2>` na `<h2>Hello k8s in Azure!</h2>`
1. Zapisz plik. Po chwili w oknie terminalu pojawi się komunikat informujący o tym, że plik w uruchomionym kontenerze został zaktualizowany.
1. Otwórz przeglądarkę i odśwież stronę. Na stronie powinien być widoczny zaktualizowany kod HTML.

Co się stało? Modyfikacje plików zawartości, takich jak HTML i CSS, nie wymagają ponownej kompilacji w aplikacji internetowej .NET Core. Z tego względu aktywne polecenie `azds up` automatycznie synchronizuje wszystkie zmodyfikowane pliki zawartości z uruchomionym kontenerem na platformie Azure, co umożliwia błyskawiczny podgląd zmian zawartości.

### <a name="update-a-code-file"></a>Aktualizowanie pliku kodu
Aktualizacja plików kodu wymaga nieco więcej pracy, ponieważ trzeba ponownie skompilować aplikację .NET Core i utworzyć zaktualizowane pliki binarne aplikacji.

1. W oknie terminalu naciśnij klawisze `Ctrl+C`, aby zatrzymać polecenie `azds up`.
1. Otwórz plik kodu o nazwie `Controllers/HomeController.cs` i zmień komunikat wyświetlany na stronie Informacje: `ViewData["Message"] = "Your application description page.";`
1. Zapisz plik.
1. Uruchom polecenie `azds up` w oknie terminalu. 

Spowoduje to ponowne skompilowanie obrazu kontenera i ponowne wdrożenie planu narzędzia Helm. Aby zobaczyć efekt zmian kodu w uruchomionej aplikacji, otwórz menu Informacje w aplikacji internetowej.


Oprócz tego dostępna jest jeszcze *szybsza metoda* opracowywania kodu. Omówimy ją w następnej sekcji. 

## <a name="debug-a-container-in-kubernetes"></a>Debugowanie kontenera w środowisku Kubernetes

W tej sekcji użyjesz programu VS Code do bezpośredniego debugowania naszego kontenera uruchomionego na platformie Azure. Ponadto dowiesz się, jak uzyskać szybszą pętlę edycji, uruchamiania i testowania.

![](media/common/edit-refresh-see.png)

> [!Note]
> **Jeśli utkniesz** w dowolnym momencie, zobacz sekcję [Rozwiązywanie problemów](troubleshooting.md) lub prześlij komentarz na tej stronie.

### <a name="initialize-debug-assets-with-the-vs-code-extension"></a>Inicjowanie zasobów debugowania za pomocą rozszerzenia programu VS Code
Najpierw musisz skonfigurować projekt kodu, aby program VS Code komunikował się z naszą przestrzenią deweloperów na platformie Azure. Rozszerzenie programu VS Code dla usługi Azure Dev Spaces udostępnia polecenie pomocnika w celu ustawienia konfiguracji debugowania. 

Otwórz okno **Paleta poleceń** (za pomocą menu **Widok | Paleta poleceń**) i przy użyciu autouzupełniania wpisz i wybierz to polecenie: `Azure Dev Spaces: Prepare configuration files for Azure Dev Spaces`. 

Spowoduje to dodanie konfiguracji debugowania dla usługi Azure Dev Spaces w obszarze folderu `.vscode`. Nie należy mylić tego polecenia z poleceniem `azds prep`, które umożliwia skonfigurowanie projektu na potrzeby wdrożenia.

![](media/common/command-palette.png)


### <a name="select-the-azds-debug-configuration"></a>Wybieranie konfiguracji debugowania w rozwiązaniu AZDS
1. Aby otworzyć widok debugowania, kliknij ikonę debugowania na **pasku działań** w bocznej części programu VS Code.
1. Wybierz pozycję **.NET Core Launch (AZDS)** (Uruchamianie programu .NET Core [AZDS]) jako aktywną konfigurację debugowania.

![](media/get-started-netcore/debug-configuration.png)

> [!Note]
> Jeśli na palecie poleceń nie widać żadnych poleceń usługi Azure Dev Spaces, upewnij się, że masz zainstalowane rozszerzenie VS Code dla usługi Azure Dev Spaces. Upewnij się, że obszar roboczy otwarty w programie VS Code odpowiada folderowi zawierającemu plik azds.yaml.


### <a name="debug-the-container-in-kubernetes"></a>Debugowanie kontenera w środowisku Kubernetes
Po naciśnięciu klawisza **F5** możesz debugować kod w środowisku Kubernetes.

Podobnie jak w przypadku polecenia `up` kod jest synchronizowany z obszarem deweloperskim, a kontener jest kompilowany i wdrażany w środowisku Kubernetes. Oczywiście tym razem debuger jest dołączany do zdalnego kontenera.

> [!Tip]
> Na pasku stanu programu VS Code będzie wyświetlany adres URL, który można kliknąć.

![](media/common/vscode-status-bar-url.png)

Ustaw punkt przerwania w pliku kodu po stronie serwera, na przykład w obrębie funkcji `Index()` w pliku źródłowym `Controllers/HomeController.cs`. Odświeżenie strony w przeglądarce powoduje aktywowanie punktu przerwania.

Masz pełny dostęp do informacji debugowania, takich jak stos wywołań, zmienne lokalne, informacje o wyjątkach itd., zupełnie jakby kod był wykonywany lokalnie.

### <a name="edit-code-and-refresh"></a>Edytowanie kodu i odświeżanie
Przy aktywnym debugerze wprowadź zmianę w kodzie. Na przykład zmodyfikuj komunikat na stronie Informacje w pliku `Controllers/HomeController.cs`. 

```csharp
public IActionResult About()
{
    ViewData["Message"] = "My custom message in the About page.";
    return View();
}
```

Zapisz plik i w okienku **Debug actions** (Akcje debugowania) kliknij przycisk **Refresh** (Odśwież). 

![](media/get-started-netcore/debug-action-refresh.png)

Zamiast ponownego kompilowania i wdrażania nowego obrazu kontenera przy każdej zmianie kodu, co często zajmuje dużo czasu, usługa Azure Dev Spaces przyrostowo ponownie kompiluje kod w istniejącym kontenerze, co przyspiesza działanie pętli edytowania/debugowania.

Odśwież aplikację internetową w przeglądarce, a następnie otwórz stronę Informacje. Twój komunikat powinien zostać wyświetlony w interfejsie użytkownika.

**Umiesz już korzystać z metody szybkiego wprowadzania zmian w kodzie i debugowania bezpośrednio w środowisku Kubernetes.** Następnie zobaczysz, jak utworzyć i wywołać drugi kontener.

## <a name="next-steps"></a>Następne kroki

> [!div class="nextstepaction"]
> [Więcej informacji na temat programowania zespołowego](team-development-netcore.md)
