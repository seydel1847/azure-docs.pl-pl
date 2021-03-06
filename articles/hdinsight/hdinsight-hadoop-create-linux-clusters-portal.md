---
title: Tworzenie klastrów usługi Apache Hadoop w przeglądarce sieci web — Azure HDInsight
description: Dowiedz się, jak utworzyć klastry Apache Hadoop, Apache HBase, Apache Storm lub Apache Spark w systemie Linux dla HDInsight przy użyciu przeglądarki sieci web i portalu Azure w wersji zapoznawczej.
services: hdinsight
author: hrasheed-msft
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 12/28/2018
ms.author: hrasheed
ms.openlocfilehash: ca8b398a796284e34ce4e0b577c335552ca75a98
ms.sourcegitcommit: 803e66de6de4a094c6ae9cde7b76f5f4b622a7bb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/02/2019
ms.locfileid: "53974271"
---
# <a name="create-linux-based-clusters-in-hdinsight-using-the-azure-portal"></a>Tworzenie klastrów opartych na systemie Linux w HDInsight przy użyciu witryny Azure portal
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

Azure portal to narzędzie do zarządzania opartego na sieci web dla usług i zasobów przechowywanych w chmurze Microsoft Azure. W tym artykule dowiesz się, jak tworzyć klastry HDInsight opartych na systemie Linux przy użyciu portalu.

## <a name="prerequisites"></a>Wymagania wstępne
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* **Subskrypcja platformy Azure**. Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **Nowoczesne przeglądarki**. Witryna Azure portal używa języka Javascript i HTML5 i mogą nie działać poprawnie w starszych przeglądarkach sieci web.

## <a name="create-clusters"></a>Tworzenie klastrów
Witryna Azure portal udostępnia większość właściwości klastra. Za pomocą szablonów usługi Azure Resource Manager, można ukryć wiele szczegółów. Aby uzyskać więcej informacji, zobacz [klastrów opartych na systemie Linux z tworzenia Apache Hadoop w HDInsight przy użyciu szablonów usługi Azure Resource Manager](hdinsight-hadoop-create-linux-clusters-arm-templates.md).

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]


1. Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).

1. Z menu po lewej stronie wybierz **+ Utwórz zasób**.

1.  W obszarze **portalu Azure Marketplace**, wybierz opcję **analizy**.

1.  W obszarze **polecane**, wybierz opcję **HDInsight**.
   
    ![Tworzenie nowego klastra w witrynie Azure portal](./media/hdinsight-hadoop-create-linux-clusters-portal/hdinsight-create-cluster.png "tworzenia nowego klastra w witrynie Azure portal")

1. Z **HDInsight** wybierz opcję **niestandardowe (rozmiar, ustawienia, aplikacje)**.

1. Wybierz **1 podstawy**, a następnie wprowadź następujące informacje:

    ![Tworzenie nowego klastra w witrynie Azure portal](./media/hdinsight-hadoop-create-linux-clusters-portal/hdinsight-create-cluster-basics.png "tworzenia nowego klastra w witrynie Azure portal")

    * Wprowadź **nazwa klastra**: Ta nazwa musi być unikatowa w skali globalnej.

    * Z **subskrypcji** listę rozwijaną, wybierz subskrypcję platformy Azure, która jest używana dla klastra.

    * Wybierz **typ klastra**, a następnie wybierz typ klastra (usługi Hadoop, Spark, itp.), którą chcesz utworzyć. **Systemu operacyjnego** będzie **Linux**. Następnie wybierz wersję typu klastra. Użyj wersji domyślnej, jeśli nie masz pewności co do wyboru. Więcej informacji można znaleźć w temacie [HDInsight cluster versions](hdinsight-component-versioning.md) (Wersje klastrów usługi HDInsight).
     
        > [!IMPORTANT]  
        > HDInsight mogą mieć różnych typów, które odnoszą się do obciążenia lub technologii, że klaster jest ona dostrojona dla klastrów. Nie istnieje obsługiwana metoda do tworzenia klastra, który łączy wiele typów, takich jak Storm i bazy danych HBase w jednym klastrze.
        
    * Aby uzyskać **nazwa użytkownika logowania klastra** i **hasło logowania klastra**, podaj nazwę użytkownika i hasło administratora.

    * Wprowadź **nazwa użytkownika SSH** i chcesz mieć hasło SSH w taki sam jak hasło administratora określone wcześniej, wybierz opcję **Użyj tego samego hasła podczas logowania do klastra** pole wyboru. Jeśli nie, wprowadź wartość **hasło** lub **klucza publicznego**, który będzie używany do uwierzytelniania użytkownika SSH. Zaleca się użycie klucza publicznego. Kliknij pozycję **Wybierz** u dołu, aby zapisać konfigurację poświadczeń.
   
        Aby uzyskać informacje, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

    * W obszarze **Grupa zasobów** określ, czy chcesz utworzyć nową grupę zasobów, czy użyć istniejącej.

    * Określ centrum danych **lokalizacji** gdzie został utworzony klaster.

    * Wybierz **dalej** aby przejść do następnej strony.

4. Z **zabezpieczenia 2 + sieć**, można Połącz klaster z siecią wirtualną, korzystając z podanej listy rozwijanej. Wybierz sieć wirtualną platformy Azure i podsieć, jeśli chcesz umieścić klastra w sieci wirtualnej. Aby uzyskać informacji na temat używania HDInsight z siecią wirtualną, łącznie z określonymi wymaganiami konfiguracji sieci wirtualnej, zobacz [HDInsight rozszerzanie możliwości za pomocą usługi Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md). Jeśli chcesz używać **pakiet Enterprise Security**, można również wykonać instrukcje w tym miejscu: [Konfigurowanie klastra HDInsight z pakietem Enterprise Security za pomocą usługi Azure Active Directory Domain Services](https://docs.microsoft.com/azure/hdinsight/domain-joined/apache-domain-joined-configure-using-azure-adds).

    Wybierz **dalej** aby przejść do następnej strony.


5. Z **magazynu 3**, określ, czy usługi Azure Storage (WASB) lub usługi Data Lake Storage jako magazynu domyślnego. Przyjrzyj się poniższej tabeli, aby uzyskać więcej informacji.

     ![Tworzenie nowego klastra w witrynie Azure portal](./media/hdinsight-hadoop-create-linux-clusters-portal/hdinsight-create-cluster-storage.png "tworzenia nowego klastra w witrynie Azure portal")

     | Magazyn                                      | Opis |
     |----------------------------------------------|-------------|
     | **Obiekty BLOB platformy Azure Storage jako magazynu domyślnego**   | <ul><li>Aby uzyskać **podstawowy typ magazynu**, wybierz opcję **usługi Azure Storage**. Po tym Aby uzyskać **metodę wyboru**, możesz wybrać **Moje subskrypcje** Jeśli chcesz określić konto magazynu, który jest częścią subskrypcji platformy Azure, a następnie wybierz konto magazynu. W przeciwnym razie kliknij przycisk **klucz dostępu** i podaj informacje dotyczące konta magazynu, który chcesz dokonać wyboru spoza Twojej subskrypcji platformy Azure.</li><li>Aby uzyskać **domyślny kontener**, użytkownik może zawsze pod ręką nazwę kontenera domyślnej, zaproponowana przez portal lub określ własne.</li><li>Jeśli używasz WASB jako magazynem domyślnym, możesz (opcjonalnie) kliknąć **dodatkowych kont magazynu** do określenia dodatkowych kont magazynu do skojarzenia z klastrem. Aby uzyskać **klucze magazynu Azure**, kliknij przycisk **Dodaj klucz magazynu**, i można podać konto magazynu z subskrypcji platformy Azure lub z innych subskrypcji (nie dostarczając klucz dostępu konta magazynu).</li><li>Jeśli używasz WASB jako magazynem domyślnym, możesz (opcjonalnie) kliknąć **dostępu do usługi Data Lake Storage** do określenia usługi Azure Data Lake Storage jako magazynu dodatkowego. Aby uzyskać więcej informacji, zobacz temat [Szybki start: Konfigurowanie klastrów w HDInsight](../storage/data-lake-storage/quickstart-create-connect-hdi-cluster.md).</li></ul> |
     | **Magazyn usługi Azure Data Lake jako magazynem domyślnym** | Dla **podstawowy typ magazynu**, wybierz opcję **usługi Azure Data Lake Storage Gen1** lub **usługi Azure Data Lake Storage Gen2** a następnie zapoznaj się z artykułem [Szybki Start: Konfigurowanie klastrów w HDInsight](../storage/data-lake-storage/quickstart-create-connect-hdi-cluster.md) instrukcje. |
     | **Zewnętrzne magazyny metadanych**                      | Opcjonalnie można określić bazę danych SQL można zapisać metadanych Hive i Oozie skojarzonego z klastrem. Aby uzyskać **wybierz bazę danych SQL dla usługi Hive** wybierz bazę danych SQL, a następnie podaj nazwę użytkownika/hasło dla bazy danych. Powtórz te czynności dla metadanych programu Oozie.<br><br>Niektóre zagadnienia podczas korzystania z bazy danych Azure SQL dla magazyny metadanych. <ul><li>Bazy danych Azure SQL, używanej do magazynu metadanych muszą zezwalać na łączność z innymi usługami platformy Azure, w tym usługi Azure HDInsight. Na pulpicie nawigacyjnym bazy danych Azure SQL po prawej stronie kliknij nazwę serwera. Jest to serwer, na którym uruchomiono wystąpienie usługi SQL database. Po użytkownik pracuje na widoku serwerów, kliknij przycisk **Konfiguruj**, a następnie dla **usług platformy Azure**, kliknij przycisk **tak**, a następnie kliknij przycisk **Zapisz**.</li><li>Podczas tworzenia metadanych, nie należy używać nazwy bazy danych, która zawiera łączników i łączniki, ponieważ może to spowodować niepowodzenie procesu tworzenia klastra.</li></ul> |

     > [!WARNING]  
     > Korzystanie z dodatkowego konta magazynu w innej lokalizacji niż klaster usługi HDInsight nie jest obsługiwane.

     Wybierz **dalej** aby przejść do następnej strony.


6. Z **4 aplikacji (opcjonalnie)**, wybierz żądane dowolnej aplikacji.  Te aplikacje mogą być opracowane przez firmę Microsoft, niezależnych dostawców oprogramowania (ISV) lub samodzielnie. Aby uzyskać więcej informacji, zobacz [aplikacji HDInsight zainstalować](hdinsight-apps-install-applications.md#install-applications-during-cluster-creation).

    Wybierz **dalej** aby przejść do następnej strony.


6. **Rozmiar klastra w 5** Wyświetla informacje o węzłach, które są używane dla tego klastra. Ustaw liczbę węzłów procesu roboczego, które są potrzebne dla klastra. Szacowany koszt klastra jest również wyświetlany.
   
    ![Warstwami cenowymi węzłów](./media/hdinsight-hadoop-create-linux-clusters-portal/hdinsight-create-cluster-nodes.png "Określ liczbę węzłów klastra")
   
   > [!IMPORTANT]  
   > Jeśli planowane jest na więcej niż 32 węzły procesu roboczego podczas tworzenia klastra lub przy użyciu skalowania klastra po utworzeniu, musisz wybrać rozmiar węzła głównego z co najmniej 8 rdzeniami i 14 GB pamięci RAM.
   > 
   > Aby uzyskać więcej informacji o rozmiarach węzła i powiązanych kosztach, zobacz [Cennik usługi HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).
   
    Wybierz **dalej** aby przejść do następnej strony.

8. Z **6 akcji skryptu**, można dostosować klaster, aby zainstalować składniki niestandardowe.  Użyj tej opcji, jeśli chcesz użyć niestandardowego skryptu do dostosowywania klastra, podczas tworzenia klastra. Aby uzyskać więcej informacji na temat akcji skryptu, zobacz [HDInsight Dostosowywanie klastrów za pomocą akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md).

   Wybierz **dalej** aby przejść do następnej strony.

9. Z **7 Podsumowanie**, sprawdź informacje, wprowadzony wcześniej, a następnie wybierz **Utwórz**.

     ![Warstwami cenowymi węzłów](./media/hdinsight-hadoop-create-linux-clusters-portal/hdinsight-create-cluster-summary.png "Określ liczbę węzłów klastra")
    
    > [!NOTE]  
    > Tworzenie klastra zajmuje trochę czasu, zwykle około 20 minut. Monitor **powiadomienia** do zapoznania się na proces inicjowania obsługi administracyjnej.

10. Po zakończeniu procesu tworzenia, wybierz **przejdź do zasobu** z **wdrażanie zakończyło się pomyślnie** powiadomień. W oknie klastra zawiera następujące informacje.
    
    ![Interfejs klastra](./media/hdinsight-hadoop-create-linux-clusters-portal/hdinsight-create-cluster-completed.png "właściwości klastra")
    
    Użyj następującego polecenia do zrozumienia ikony u góry.
    
    * **Omówienie** karta zawiera wszystkie niezbędne informacje dotyczące klastra, takie jak nazwa, należy do grupy zasobów, lokalizacji, systemu operacyjnego, adres URL dla pulpit nawigacyjny klastra itp.
    * **Pulpit nawigacyjny** kieruje użytkownika do portalu Ambari skojarzonego z klastrem.
    * **Bezpieczna powłoka**: Informacje potrzebne, aby uzyskać dostęp do klastra przy użyciu protokołu SSH.
    * **Skaluj klaster** pozwala zwiększyć liczbę węzłów procesu roboczego skojarzonego z klastrem.
      * **Usuń**: Usuwa klaster HDInsight.
    

## <a name="customize-clusters"></a>Dostosowywanie klastrów
* Zobacz [HDInsight Dostosowywanie klastrów za pomocą narzędzia Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md).
* Zobacz [HDInsight Dostosowywanie klastrów za pomocą akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md).

## <a name="delete-the-cluster"></a>Usuwanie klastra
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a>Rozwiązywanie problemów

W razie problemów podczas tworzenia klastrów usługi HDInsight zapoznaj się z [wymaganiami dotyczącymi kontroli dostępu](hdinsight-hadoop-create-linux-clusters-portal.md).

## <a name="next-steps"></a>Kolejne kroki
Teraz, że udało Ci się utworzyć klaster usługi HDInsight, należy użyć następującego, aby dowiedzieć się, jak pracować z klastrem:

### <a name="apache-hadoop-clusters"></a>Klastry platformy Apache Hadoop
* [Use Apache Hive z HDInsight](hadoop/hdinsight-use-hive.md)
* [UseApache z języka Pig z HDInsight](hadoop/hdinsight-use-pig.md)
* [Używanie technologii MapReduce z HDInsight](hadoop/hdinsight-use-mapreduce.md)

### <a name="apache-hbase-clusters"></a>Klastry Apache HBase
* [Rozpoczynanie pracy z usługą Apache HBase na HDInsight](hbase/apache-hbase-tutorial-get-started-linux.md)
* [Twórz aplikacje Java dla bazy danych Apache HBase na HDInsight](hbase/apache-hbase-build-java-maven-linux.md)

### <a name="apache-storm-clusters"></a>Klastrów Apache Storm
* [Opracowywanie topologii języka Java dla usługi Storm Apache na HDInsight](storm/apache-storm-develop-java-topology.md)
* [Używanie składników języka Python w Storm Apache na HDInsight](storm/apache-storm-develop-python-topology.md)
* [Wdrażanie i monitorowanie topologii za pomocą Storm Apache na HDInsight](storm/apache-storm-deploy-monitor-topology-linux.md)

### <a name="apache-spark-clusters"></a>Klastry platformy Apache Spark
* [Tworzenie autonomicznych aplikacji przy użyciu języka Scala](spark/apache-spark-create-standalone-application.md)
* [Zdalne uruchamianie zadań w klastrze Apache Spark przy użyciu programu Apache Livy](spark/apache-spark-livy-rest-interface.md)
* [Platforma Apache Spark przy użyciu Power BI: Interakcyjna analiza danych przy użyciu platformy Spark w HDInsight przy użyciu narzędzi do analizy Biznesowej](spark/apache-spark-use-bi-tools.md)
* [Platforma Apache Spark w usłudze Machine Learning: Korzystanie z platformy Spark w HDInsight do przewidywania wyników kontroli żywności](spark/apache-spark-machine-learning-mllib-ipython.md)

