---
author: erhopf
ms.service: cognitive-services
ms.topic: include
ms.date: 12/13/2018
ms.author: erhopf
ms.openlocfilehash: 79fbe2db1ec9758d1e15ba7d89363429415918c7
ms.sourcegitcommit: 549070d281bb2b5bf282bc7d46f6feab337ef248
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/21/2018
ms.locfileid: "53729479"
---
1. Uruchom program Visual Studio 2017.

1. Upewnij się, że jest dostępny pakiet roboczy **tworzenia platformy uniwersalnej systemu Windows**. Wybierz kolejno pozycje **Narzędzia** > **Pobierz narzędzia i funkcje** na pasku menu programu Visual Studio, aby otworzyć instalator programu Visual Studio. Jeśli ten pakiet roboczy jest już włączony, zamknij okno dialogowe.

    ![Zrzut ekranu Instalatora programu Visual Studio z wyróżnioną kartą Pakiety robocze](../articles/cognitive-services/Speech-Service/media/sdk/vs-enable-uwp-workload.png)

    W przeciwnym razie zaznacz pole obok pozycji **Tworzenie aplikacji na wiele platform dla platformy .NET** i wybierz opcję **Modyfikuj** w prawym dolnym rogu okna dialogowego. Instalowanie nowej funkcji chwilę potrwa.

1. Utwórz pustą aplikację uniwersalną dla systemu Windows w języku C#. Najpierw wybierz w menu pozycje **Plik** > **Nowy** > **Projekt**. W oknie dialogowym **Nowy projekt** w lewym okienku rozwiń pozycje **Zainstalowane** > **Visual C#** > **Aplikacje uniwersalne systemu Windows**. Następnie wybierz pozycję **Pusta aplikacja (platforma uniwersalna systemu Windows)**. Jako nazwę projektu podaj *helloworld*.

    ![Zrzut ekranu przedstawiający okno dialogowe Nowy projekt](../articles/cognitive-services/Speech-Service/media/sdk/qs-csharp-uwp-01-new-blank-app.png)

1. Zestaw Speech SDK wymaga, by aplikacja została utworzona dla systemu Windows 10 Fall Creators Update lub jego nowszej wersji. W wyświetlonym oknie **Nowy projekt platformy uniwersalnej systemu Windows** wybierz pozycję **Windows 10 Fall Creators Update (10.0; kompilacja 16299)** dla opcji **Wersja minimalna**. W polu **Wersja docelowa** wybierz tę lub dowolną nowszą wersję, a następnie kliknij przycisk **OK**.

    ![Zrzut ekranu przedstawiający okno Nowy projekt platformy uniwersalnej systemu Windows](../articles/cognitive-services/Speech-Service/media/sdk/qs-csharp-uwp-02-new-uwp-project.png)

1. Jeśli korzystasz z 64-bitowego systemu Windows, możesz przełączyć platformę kompilacji na `x64` za pomocą menu rozwijanego na pasku narzędzi programu Visual Studio. (64-bitowy system Windows może obsługiwać aplikacje 32-bitowe, więc jeśli wolisz, możesz pozostawić wartość `x86`.)

   ![Zrzut ekranu paska narzędzi programu Visual Studio z wyróżnioną opcją x64](../articles/cognitive-services/Speech-Service/media/sdk/qs-csharp-uwp-03-switch-to-x64.png)

   > [!NOTE]
   > Zestaw Speech SDK obsługuje wyłącznie procesory zgodne z technologią Intel. Architektura ARM nie jest obecnie obsługiwana.

1. Instalowanie i odwoływanie się do [zestawu Speech SDK pakietu NuGet](https://aka.ms/csspeech/nuget). W Eksploratorze rozwiązań kliknij rozwiązanie prawym przyciskiem myszy, a następnie wybierz pozycję **Zarządzaj pakietami NuGet dla rozwiązania**.

    ![Zrzut ekranu Eksploratora rozwiązań z wyróżnioną opcją Zarządzaj pakietami NuGet rozwiązania](../articles/cognitive-services/Speech-Service/media/sdk/qs-csharp-uwp-04-manage-nuget-packages.png)

1. W prawym górnym rogu wybierz w polu **Źródło pakietu** wartość **nuget.org**. Wyszukaj pakiet `Microsoft.CognitiveServices.Speech` i zainstaluj go w projekcie **helloworld**.

    ![Zrzut ekranu okna dialogowego Zarządzaj pakietami rozwiązania](../articles/cognitive-services/Speech-Service/media/sdk/qs-csharp-uwp-05-nuget-install-1.0.0.png "Instaluj pakiet NuGet")

1. Zaakceptuj wyświetloną licencję, aby rozpocząć instalowanie pakietu NuGet.

    ![Zrzut ekranu okna dialogowego Akceptacja licencji](../articles/cognitive-services/Speech-Service/media/sdk/qs-csharp-uwp-06-nuget-license.png "Akceptacja licencji")

1. W konsoli Menedżera pakietów zostaje wyświetlona linia z następującymi danymi wyjściowymi.

   ```text
   Successfully installed 'Microsoft.CognitiveServices.Speech 1.2.0' to helloworld
   ```

1. Ze względu na to, że aplikacja używa mikrofonu do danych wejściowych mowy, dodaj do projektu funkcję **Mikrofon**. W Eksploratorze rozwiązań kliknij dwukrotnie opcję **Package.appxmanifest**, aby edytować manifest aplikacji. Następnie przejdź na kartę **Capabilities** (Funkcje) i zaznacz pole obok funkcji **Mikrofon**, a następnie zapisz wprowadzone zmiany.

   ![Zrzut ekranu manifestu aplikacji programu Visual Studio z wyróżnionymi opcjami Capabilities (Funkcje) i Mikrofon](../articles/cognitive-services/Speech-Service/media/sdk/qs-csharp-uwp-07-capabilities.png)
