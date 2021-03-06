---
title: Instalowanie opublikowanej aplikacji — H2O Sparkling Water — Azure HDInsight
description: Instalowanie i używanie aplikacji platformy Hadoop innych firm H2O Sparkling Water.
services: hdinsight
author: ashishthaps
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 01/10/2018
ms.author: ashish
ms.openlocfilehash: 4be346163fd54c0c5f962d15bc2433c7fab49e0b
ms.sourcegitcommit: e68df5b9c04b11c8f24d616f4e687fe4e773253c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/20/2018
ms.locfileid: "53650947"
---
# <a name="install-published-application---h2o-sparkling-water"></a>Instalowanie opublikowanej aplikacji — H2O Sparkling Water

W tym artykule opisano sposób instalowania i uruchamiania [H20 Sparkling Water](https://www.h2o.ai/) opublikowane [Apache Hadoop](https://hadoop.apache.org/) aplikacji w usłudze Azure HDInsight. Omówienie platformy aplikacji HDInsight i listę z dostępnych niezależnym dostawcą oprogramowania (ISV) opublikowanych aplikacji, zobacz [instalowanie aplikacji platformy Hadoop innych firm](hdinsight-apps-install-applications.md). Aby uzyskać instrukcje instalowania własnej aplikacji, zobacz [Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md) (Instalowanie niestandardowych aplikacji usługi HDInsight).

## <a name="about-h2o-sparkling-water"></a>Temat H2O Sparkling Water

H2O Sparkling Water to open source platforma edukacyjna pełni rozproszonych maszyny w pamięci z skalowalność liniowa. H2O Sparkling Water umożliwia łączenie algorytmów H2O z możliwościami uczenia maszynowego szybkich, skalowalnych [platformy Apache Spark](https://spark.apache.org/). Dzięki temu Sparkling użytkowników może zapewnić obliczeń z [Scala](https://www.scala-lang.org/), R i Python przy użyciu interfejsu H2O przepływu użytkownika.

H2O Sparkling Water umożliwia:

* **Łatwe w użyciu interfejsem sieci Web i znanych interfejsów** — ustawienie zapasowej i Rozpocznij pracę, szybko przy użyciu obu H2O intuicyjne opartego na sieci web przepływu graficznego interfejsu użytkownika lub środowisk, takich jak R, Python, Java, Scala, JSON i interfejsów API H2O programowania.
* **Niezależnie od danych Obsługa wszystkich popularnych typów bazy danych i pliku** — łatwe Eksplorowanie i modelowanie danych Big Data z w ramach programu Microsoft Excel, programu R Studio, Tableau i. Łączenie z danymi ze źródeł danych systemu plików HDFS, S3, SQL i NoSQL.
* **Wysoce skalowalny (munging) z danych Big Data i analiza** — H2O duże sprzężenia można wykonywać 7 x szybciej niż operacje data.table R i liniowe skalowanie na 10 miliardów x 10 miliardów wierszy sprzężenia.
* **Ocenianie danych w czasie rzeczywistym** — szybko wdrażać modele do produkcji przy użyciu zwykłego old Java obiektów (obiektu typu POJO), zoptymalizowane pod kątem modelu obiektów języka Java (MOJO), lub interfejsu API REST H2O.

### <a name="resource-links"></a>Linki zasobów

* [H2O.ai Engineering Roadmap](http://jira.h2o.ai/)
* [Strona główna H2O.AI](https://www.h2o.ai/)
* [Dokumentacja H2O.AI](http://docs.h2o.ai/)
* [Obsługa H2O.AI](https://support.h2o.ai/)
* [H2O.AI "Open Source" w bazie kodu](https://github.com/h2oai/)

## <a name="prerequisites"></a>Wymagania wstępne

Aby zainstalować tę aplikację w nowym klastrze HDInsight lub istniejącego klastra, musisz mieć następującą konfigurację:

* Warstwy klastrów: Standardowa lub Premium
* Typ klastra: platforma Spark
* Wersje klastrów: 3.5 i 3.6

## <a name="install-the-h2o-sparkling-water-published-application"></a>Instalowanie H2O Sparkling Water opublikowanej aplikacji

Aby uzyskać instrukcje krok po kroku dotyczące instalowania tego i innych dostępnych aplikacji niezależnych dostawców oprogramowania, przeczytaj [instalowanie aplikacji usługi Apache Hadoop innych firm](hdinsight-apps-install-applications.md).

## <a name="launch-h2o-sparkling-water"></a>Uruchom H2O Sparkling Water

1. Po zakończeniu instalacji, można uruchomić przy użyciu H2O Sparkling Water (h2o sparklingwater) z klastrem w witrynie Azure portal, otwierając [notesów programu Jupyter](https://jupyter.org/) (`https://<ClusterName>.azurehdinsight.net/jupyter`). Można także uzyskać się do aplikacji Jupyter, wybierając **pulpit nawigacyjny klastra** usługi klastra w okienku portalu, a następnie wybierając pozycję **notesu programu Jupyter**. Monit o podanie poświadczeń. Wprowadź poświadczenia usługi Hadoop klastra zgodnie z instrukcjami na utworzenie klastra.

2. W programie Jupyter zostanie wyświetlony trzy foldery: H2O-PySparkling — przykłady, przykłady PySpark i Scala przykłady. Wybierz **H2O-PySparkling — przykłady** folderu.

    ![Program Jupyter Notebooks macierzystego](./media/hdinsight-apps-install-h2o/jupyter-home.png)

3. Pierwszym krokiem podczas tworzenia nowego notesu jest skonfigurowanie środowiska platformy Spark. Te informacje znajdują się w **Sentiment_analysis_with_Sparkling_Water** przykład. Podczas konfigurowania środowiska platformy Spark, należy użyć poprawny plik jar i określ adres IP podany w danych wyjściowych pierwszej komórki.

    ![Program Jupyter Notebooks macierzystego](./media/hdinsight-apps-install-h2o/spark-config.png)

4. Uruchomienie klastra H2O.

    ![Uruchomienie klastra](./media/hdinsight-apps-install-h2o/start-cluster.png)

5. Po skonfigurowaniu i uruchomieniu klastra H2O Otwórz przepływ H2O, przechodząc do **`https://<ClusterName>-h2o.apps.azurehdinsight.net:443`**.

    > [!NOTE]  
    > Jeśli nie można otworzyć przepływu H2O, spróbuj wyczyszczenie pamięci podręcznej przeglądarki. Jeśli jednak nie można przejść do niego, prawdopodobnie nie masz wystarczającej liczby zasobów w klastrze. Spróbuj zwiększyć liczbę węzłów procesu roboczego w obszarze **Skaluj klaster** opcji w okienku klastra.

    ![Przepływ H2O pulpitu nawigacyjnego](./media/hdinsight-apps-install-h2o/h2o-flow.png)

6. Wybierz **Million_Songs.flow** przykładu z menu po prawej stronie. Gdy zostanie wyświetlony monit z ostrzeżeniem, kliknij przycisk **notesu obciążenia**. Tej wersji demonstracyjnej jest przeznaczony do działania w ciągu kilku minut przy użyciu rzeczywistych danych. Celem jest przewidzieć z danych, czy utwór został wydany przed lub po 2004 przy użyciu klasyfikacji binarnej.

    ![Wybierz Million_Songs.flow](./media/hdinsight-apps-install-h2o/million-songs.png)

7. Znajdź zawierający ścieżkę **milsongs-zgodny ze specyfikacją train.csv.gz**i Zastąp całą ścieżkę z **https://h2o-public-test-data.s3.amazonaws.com/bigdata/laptop/milsongs/milsongs-cls-train.csv.gz**.

8. Znajdź zawierający ścieżkę **milsongs-zgodny ze specyfikacją test.csv.gz** i zastąp go wartością **https://h2o-public-test-data.s3.amazonaws.com/bigdata/laptop/milsongs/milsongs-cls-test.csv.gz**.

9. Aby wykonać wszystkie instrukcje w komórkach Notes, wybierz **Uruchom wszystkie** przycisk na pasku narzędzi.

    ![Uruchom wszystko](./media/hdinsight-apps-install-h2o/run-all.png)

10. Po kilku minutach powinny być widoczne dane wyjściowe podobne do następujących.

    ![Dane wyjściowe](./media/hdinsight-apps-install-h2o/output.png)

Gotowe. Zostały zaprzęgnięte sztucznej inteligencji na platformie Spark w ciągu kilku minut. Teraz możesz eksplorować więcej przykładów w H2O przepływu, które pokazują różne typy algorytmów uczenia maszynowego.

## <a name="next-steps"></a>Kolejne kroki

* [Dokumentacja H2O](http://docs.h2o.ai/h2o/latest-stable/h2o-docs/index.html)
* [Instalowanie niestandardowych aplikacji HDInsight](hdinsight-apps-install-custom-applications.md): Dowiedz się, jak wdrożyć cofnięto publikowanie aplikacji HDInsight HDInsight.
* [Publikowanie aplikacji HDInsight](hdinsight-apps-publish-applications.md): Dowiedz się, jak opublikować niestandardowe aplikacje HDInsight w portalu Azure Marketplace.
* [MSDN: Instalowanie aplikacji usługi HDInsight](https://msdn.microsoft.com/library/mt706515.aspx): Dowiedz się, jak zdefiniować aplikacje HDInsight.
* [Dostosowywanie klastrów HDInsight opartych na systemie Linux za pomocą akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md): Dowiedz się, jak instalować dodatkowe aplikacje za pomocą akcji skryptu.
* [Używanie pustych węzłów brzegowych w HDInsight](hdinsight-apps-use-edge-node.md): Dowiedz się, jak używać pustego węzła krawędzi do uzyskiwania dostępu do klastrów HDInsight, a także do testowania i obsługi aplikacji HDInsight.
