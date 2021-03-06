---
title: Wdrażanie topologii Apache Storm w usłudze Azure HDInsight i zarządzanie
description: Dowiedz się, jak wdrażanie, monitorowanie i zarządzanie topologii usługi Apache Storm na HDInsight z systemem Windows przy użyciu pulpitu nawigacyjnego Storm. Użyj narzędzi usługi Hadoop dla programu Visual Studio.
services: hdinsight
ms.service: hdinsight
author: hrasheed-msft
ms.reviewer: jasonh
ms.topic: conceptual
ms.date: 03/01/2017
ms.author: hrasheed
ROBOTS: NOINDEX
ms.openlocfilehash: 322c7164c0ecda550bf1bfe6a55075759bf95735
ms.sourcegitcommit: c94cf3840db42f099b4dc858cd0c77c4e3e4c436
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/19/2018
ms.locfileid: "53630520"
---
# <a name="deploy-and-manage-apache-storm-topologies-on-windows-based-hdinsight"></a>Wdrażanie i zarządzanie topologiami Apache Storm na HDInsight z systemem Windows

[Apache Storm](https://storm.apache.org/) pulpit nawigacyjny umożliwia łatwe wdrażanie i wykonywania topologii Apache Storm do usługi HDInsight klastra za pomocą przeglądarki sieci web. Umożliwia także pulpit nawigacyjny do monitorowania uruchomionych topologii i zarządzania. Jeśli używasz programu Visual Studio, narzędzia HDInsight dla programu Visual Studio zapewniają podobne funkcje w programie Visual Studio.

Pulpit nawigacyjny platformy Storm i funkcje systemu Storm w narzędziach HDInsight korzystają rozwiązań do zarządzania i interfejs API REST systemu Storm, który może służyć do tworzenia własnych monitorowania.

> [!IMPORTANT]  
> Kroki opisane w tym dokumencie wymagają platformy Storm w klastrze HDInsight, który używa systemu operacyjnego Windows. Linux jest jedynym systemem operacyjnym używanym w połączeniu z usługą HDInsight w wersji 3.4 lub nowszą. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).
>
> Aby uzyskać informacji na temat wdrażania i zarządzania nimi topologii systemu Storm przy użyciu klastra usługi HDInsight, który używa systemu Linux, zobacz [wdrażanie i zarządzanie topologiami Apache Storm na HDInsight opartych na systemie Linux](apache-storm-deploy-monitor-topology-linux.md)

## <a name="prerequisites"></a>Wymagania wstępne

* **Storm Apache na HDInsight** — zobacz [Rozpoczynanie pracy z usługą Apache Storm w HDInsight](apache-storm-tutorial-get-started-linux.md) Aby uzyskać instrukcje dotyczące tworzenia klastra.

* Aby uzyskać **pulpit nawigacyjny Storm**: Nowoczesna przeglądarka sieci Web, obsługująca język HTML5.

* Dla **programu Visual Studio** — zestaw Azure SDK 2.5.1 lub nowszej i narzędzi HDInsight dla programu Visual Studio. Zobacz [rozpoczęcie korzystania z narzędzi HDInsight Tools for Visual Studio](../hadoop/apache-hadoop-visual-studio-tools-get-started.md) Instalowanie i Konfigurowanie narzędzi HDInsight tools for Visual Studio.

    Jeden z następujących wersji programu Visual Studio:

  * Program Visual Studio 2012 z aktualizacją Update 4

  * Visual Studio 2013 z aktualizacją Update 4 lub Visual Studio 2013 Community

  * Program Visual Studio 2015 (w każdej wersji)

  * Program Visual Studio 2017 (w każdej wersji)

## <a name="storm-dashboard"></a>Pulpit nawigacyjny STORM

Pulpit nawigacyjny platformy Storm jest dostępne w klastrze Storm strony sieci web. Adres URL jest **https://&lt;nazwa_klastra >.azurehdinsight.net/**, gdzie **clustername** nazywa się w klastrze HDInsight Storm.

W górnej części pulpitu nawigacyjnego Storm, wybierz **przesyłanie topologii**. Postępuj zgodnie z instrukcjami na stronie uruchamiania przykładowych topologii lub przekazywanie i uruchomić topologię, który został utworzony.

![na stronie topologia przesyłania][storm-dashboard-submit]

### <a name="storm-ui"></a>Interfejs użytkownika platformy STORM

Wybierz z pulpitu nawigacyjnego Storm **interfejs użytkownika platformy Storm** łącza. Spowoduje to wyświetlenie informacji o klastrze, oprócz żadnych uruchomionych topologii.

![Interfejs użytkownika platformy storm][storm-dashboard-ui]

> [!NOTE]  
> W niektórych wersjach programu Internet Explorer może stwierdzić, interfejs użytkownika platformy Storm nie powoduje odświeżenia po raz pierwszy odwiedzeniu go. Na przykład może nie pokazywać nowe topologii przesłane lub mogą być wyświetlane topologii jako aktywny, gdy wcześniej zdezaktywowane. Firma Microsoft zapoznała się o tym problemie i pracuje nad rozwiązaniem.

#### <a name="main-page"></a>Strona główna

Główna strona interfejsu użytkownika platformy Storm udostępnia następujące informacje:

* **Podsumowanie klastra**: Podstawowe informacje o klaster Storm.

* **Podsumowanie topologii**: Listy uruchomionych topologii. Użyj linków w tej sekcji, aby wyświetlić więcej informacji na temat określonych topologii.

* **Nadzorca podsumowania**: Informacje na temat nadzorcy systemu Storm.

* **Konfiguracja nimbus**: Nimbus konfigurację klastra.

#### <a name="topology-summary"></a>Podsumowanie topologii

Link z wybraniu **podsumowanie topologii** sekcja wyświetla następujące informacje na temat topologii:

* **Podsumowanie topologii**: Podstawowe informacje na temat topologii.

* **Akcje topologii**: Akcje zarządzania, które można wykonywać w odniesieniu do topologii.

  * **Aktywuj**: Wznowienie przetwarzania dezaktywowanej topologii.

  * **Dezaktywuj**: Wstrzymanie uruchomionej topologii.

  * **Ponowne zrównoważenie**: To dostosować równoległość topologii. Po zmianie liczby węzłów w klastrze należy przeprowadzić ponowne równoważenie uruchomionych topologii. Dzięki temu topologię, aby dostosować równoległość topologii w celu kompensacji zwiększenia lub zmniejszenia liczby węzłów w klastrze.

      Aby uzyskać więcej informacji, zobacz [pojęcie równoległości w topologii Apache Storm](https://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).

  * **Kill**: Kończy topologii Storm po określonym czasie.

* **Topology stats**: Statystyka topologii. Użyj linków w **okna** kolumnę, aby ustawić przedział czasu dla pozostałych wpisów na stronie.

* **Spouts**: Elementy spout używane przez topologię. Użyj linków w tej sekcji, aby wyświetlić więcej informacji na temat określonych elementów spout.

* **Bolts**: Elementy bolt używane przez topologię. Użyj linków w tej sekcji, aby wyświetlić więcej informacji na temat określonych elementów bolt.

* **Konfiguracja topologii**: Konfiguracja wybrana topologia.

#### <a name="spout-and-bolt-summary"></a>Spout i Bolt — podsumowanie

Spout z wybraniu **Spouts** lub **Bolts** sekcje są wyświetlane następujące informacje dotyczące wybranej pozycji:

* **Podsumowanie składników**: Podstawowe informacje o spout lub bolt.

* **Spout/Bolt stats**: Statystyka spout lub bolt. Użyj linków w **okna** kolumnę, aby ustawić przedział czasu dla pozostałych wpisów na stronie.

* **Dane wejściowe statystyki** (tylko dla elementów bolt): Informacje na temat strumienie wejściowe, używane przez element bolt.

* **OUTPUT stats**: Informacje na temat strumienie emitowane przez to spout lub bolt.

* **Executors**: Informacje na temat wystąpień elementu spout lub bolt. Wybierz **portu** wpis dla określonych wykonawcy wyświetlić dziennik informacji diagnostycznych utworzone dla tego wystąpienia.

* **Błędy**: Wszelkie informacje o błędzie dla tego spout lub bolt.

## <a name="hdinsight-tools-for-visual-studio"></a>HDInsight Tools for Visual Studio

[Narzędzi HDInsight](https://azure.microsoft.com/resources/videos/hdinsight-tools-for-visual-studio/) może służyć do przesyłania C# lub hybrydowe topologie z klastrem Storm. Użyto przykładowej aplikacji. Aby uzyskać informacje dotyczące tworzenia własnych topologii za pomocą narzędzi HDInsight, zobacz [topologii opracowywanie języka C# za pomocą narzędzi HDInsight dla programu Visual Studio](apache-storm-develop-csharp-visual-studio-topology.md).

Wykonaj następujące kroki, aby wdrażanie przykładu w klastrze HDInsight Storm, a następnie Wyświetl i zarządzaj nimi topologii.

1. Jeśli nie już zainstalowano najnowszą wersję narzędzi HDInsight Tools for Visual Studio, zobacz [rozpoczęcie korzystania z narzędzi HDInsight Tools for Visual Studio](../hadoop/apache-hadoop-visual-studio-tools-get-started.md).

2. Otwórz program Visual Studio, wybierz **pliku** > **New** > **projektu**.

3. W **nowy projekt** okna dialogowego rozwiń **zainstalowane** > **szablony**, a następnie wybierz pozycję **HDInsight**. Z listy szablonów wybierz **przykładowe Storm**. W dolnej części okna dialogowego wpisz nazwę dla aplikacji.

    ![image](./media/apache-storm-deploy-monitor-topology/sample.png)

4. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt i wybierz **Prześlij do systemu Storm w HDInsight**.

   > [!NOTE]  
   > Po wyświetleniu monitu wprowadź poświadczenia logowania dla subskrypcji platformy Azure. Jeśli masz więcej niż jedną subskrypcję, zaloguj się do tego, który zawiera Storm w klastrze HDInsight.

5. Wybierz usługi Storm w klastrze HDInsight z **klastra Storm** listy rozwijanej, a następnie wybierz **przesyłania**. Można monitorować, czy przesyłanie zakończy się za pomocą **dane wyjściowe** okna.

6. Po pomyślnym przesłaniu topologii **topologii Storm** dla klastra powinna zostać wyświetlona. Wybierz topologię z listy, aby wyświetlić informacje o uruchomionej topologii.

    ![Monitorowanie programu Visual studio](./media/apache-storm-deploy-monitor-topology/vsmonitor.png)

   > [!NOTE]  
   > Można również wyświetlić **topologii Storm** z **Eksploratora serwera** , rozwijając **Azure** > **HDInsight**, a następnie Kliknij prawym przyciskiem myszy platformy Storm w klastrze HDInsight, a następnie wybierając **wyświetl topologie Storm**.

    Wybierz kształt elementy spout lub bolt, aby wyświetlić informacje o tych składników. Zostanie otwarte nowe okno, dla każdego wybranego elementu.

   > [!NOTE]  
   > Nazwa topologii jest nazwa klasy topologii (w tym przypadku `HelloWord`,) z sygnaturą czasową dołączane.

7. Z **podsumowanie topologii** widoku, wybierz opcję **Kill** zatrzymać topologię.

   > [!NOTE]  
   > Topologie STORM nadal uruchomione, dopóki nie pozostaną one zatrzymane lub klaster jest usuwany.


## <a name="rest-api"></a>Interfejs API REST

Interfejs użytkownika platformy Storm bazuje na usłudze interfejsu API REST, aby można było wykonywać podobne do zarządzania i monitorowania funkcjonalności za pomocą interfejsu API REST. Interfejs API REST umożliwia tworzenie niestandardowych narzędzi do zarządzania i monitorowania topologii Storm.

Aby uzyskać więcej informacji, zobacz [Apache Storm Interfejsu REST API](https://github.com/apache/storm/blob/0.9.3-branch/STORM-UI-REST-API.md). Następujące informacje są specyficzne dla przy użyciu platformy Apache Storm w HDInsight przy użyciu interfejsu API REST.

### <a name="base-uri"></a>Podstawowy identyfikator URI

Podstawowy identyfikator URI dla interfejsu API REST w klastrach HDInsight jest **https://&lt;nazwa_klastra >.azurehdinsight.net/stormui/api/v1/**, gdzie **clustername** nazywa się na HDInsight Storm klaster.

### <a name="authentication"></a>Authentication

Żądania interfejsu API REST muszą używać **uwierzytelnianie podstawowe**, dlatego użyto nazwy administratora klastra HDInsight i hasło.

> [!NOTE]  
> Ponieważ uwierzytelnianie podstawowe są wysyłane przy użyciu zwykłego tekstu, należy **zawsze** bezpieczna komunikacja przy użyciu klastra przy użyciu protokołu HTTPS.

### <a name="return-values"></a>Zwracane wartości

Można używać z w ramach klastra lub maszyn wirtualnych w tej samej sieci wirtualnej platformy Azure, co klaster może być tylko informacje zwrócone z interfejsu API REST. Na przykład w pełni kwalifikowana nazwa domeny (FQDN) dla [Apache ZooKeeper](https://zookeeper.apache.org/) serwery są nie są dostępne z Internetu.

## <a name="next-steps"></a>Następne kroki

Teraz, wyjaśniono, jak wdrożyć i monitorować topologie za pomocą pulpitu nawigacyjnego Storm, Dowiedz się, jak:

* [Opracowywanie topologii języka C# za pomocą narzędzi HDInsight dla programu Visual Studio](apache-storm-develop-csharp-visual-studio-topology.md)

* [Opracowywanie topologii opartych na języku Java, przy użyciu narzędzia Apache Maven](apache-storm-develop-java-topology.md)

Aby uzyskać listę więcej przykładowe topologie, zobacz [przykładowe topologie dla Storm Apache na HDInsight](apache-storm-example-topology.md).

[hdinsight-dashboard]: ./media/apache-storm-deploy-monitor-topology/dashboard-link.png
[storm-dashboard-submit]: ./media/apache-storm-deploy-monitor-topology/submit.png
[storm-dashboard-ui]: ./media/apache-storm-deploy-monitor-topology/storm-ui-summary.png
