---
title: Uruchamianie notesu usługi Databricks za pomocą działania notesu usługi Databricks w usłudze Azure Data Factory
description: Dowiedz się, jak można użyć działania notesu usługi Databricks w usłudze Azure Data Factory w celu uruchomienia notesu usługi Databricks w klastrze zadań usługi Databricks.
services: data-factory
documentationcenter: ''
author: nabhishek
manager: craigg
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.topic: tutorial
ms.date: 03/12/2018
ms.author: abnarain
ms.reviewer: douglasl
ms.openlocfilehash: 7035035823e00fb0c12de3f4eeae11d8b3e1d54d
ms.sourcegitcommit: 25936232821e1e5a88843136044eb71e28911928
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/04/2019
ms.locfileid: "54016927"
---
# <a name="run-a-databricks-notebook-with-the-databricks-notebook-activity-in-azure-data-factory"></a>Uruchamianie notesu usługi Databricks za pomocą działania notesu usługi Databricks w usłudze Azure Data Factory

W tym samouczku w witrynie Azure Portal utworzysz potok usługi Azure Data Factory, który wykona notes usługi Databricks w klastrze zadań usługi Databricks. Podczas wykonywania parametry usługi Azure Data Factory będą również przekazywane do notesu usługi Databricks.

Ten samouczek obejmuje następujące procedury:

  - Tworzenie fabryki danych.

  - Tworzenie potoku, który używa działania notesu usługi Databricks.

  - Wyzwalanie uruchomienia potoku.

  - Monitorowanie uruchomienia potoku.

Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz  [bezpłatne konto](https://azure.microsoft.com/free/) .

Poniższy klip wideo zawiera jedenastominutowe wprowadzenie i demonstrację tej funkcji:

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/ingest-prepare-and-transform-using-azure-databricks-and-data-factory/player]

## <a name="prerequisites"></a>Wymagania wstępne

  - **Obszar roboczy usługi Azure Databricks**. [Utwórz obszar roboczy usługi Databricks](https://docs.microsoft.com/azure/azure-databricks/quickstart-create-databricks-workspace-portal) lub użyj istniejącego. Najpierw utworzysz notes Python w obszarze roboczym usługi Azure Databricks. Następnie wykonasz notes i przekażesz do niego parametry przy użyciu usługi Azure Data Factory.

## <a name="create-a-data-factory"></a>Tworzenie fabryki danych

1.  Uruchom przeglądarkę internetową  **Microsoft Edge**  lub  **Google Chrome** . Obecnie interfejs użytkownika usługi Data Factory jest obsługiwany tylko przez przeglądarki internetowe Microsoft Edge i Google Chrome.

1.  Wybierz pozycję  **Utwórz zasób**  w menu po lewej stronie, a następnie kolejno pozycje  **Analiza** i  **Data Factory**.

    ![Tworzenie nowej fabryki danych](media/transform-data-using-databricks-notebook/new-azure-data-factory-menu.png)

1.  W okienku  **Nowa fabryka danych**  wpisz  **ADFTutorialDataFactory**  w polu  **Nazwa**.

    Nazwa fabryki danych Azure musi być  *globalnie unikatowa*. Jeśli zostanie wyświetlony poniższy błąd, zmień nazwę fabryki danych. Na przykład użyj nazwy  **\<twoje_imię\>ADFTutorialDataFactory**. Reguły nazewnictwa artefaktów usługi Data Factory zawiera artykuł  [Data Factory — Naming Rules (Data Factory — reguły nazewnictwa)](https://docs.microsoft.com/azure/data-factory/naming-rules) .

    ![Udostępnianie nazwy nowej fabryki danych](media/transform-data-using-databricks-notebook/new-azure-data-factory.png)

1.  W obszarze  **Subskrypcja** wybierz subskrypcję platformy Azure, w której chcesz utworzyć fabrykę danych.

1.  W obszarze  **Grupa zasobów** wykonaj jedną z następujących czynności:
    
    - Wybierz pozycję  **Użyj istniejącej**, a następnie wybierz istniejącą grupę zasobów z listy rozwijanej.
    
    - Wybierz pozycję  **Utwórz nową**, a następnie wprowadź nazwę grupy zasobów.

    W niektórych krokach w tym samouczku szybkiego startu zakłada się, że nazwa grupy zasobów to  **ADFTutorialResourceGroup** . Informacje na temat grup zasobów znajdują się w artykule  [Using resource groups to manage your Azure resources (Używanie grup zasobów do zarządzania zasobami platformy Azure)](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).

1.  W obszarze  **Wersja** wybierz pozycję  **V2**.

1.  W obszarze  **Lokalizacja** wybierz lokalizację fabryki danych.

    Aby uzyskać listę regionów platformy Azure, w których obecnie jest dostępna usługa Data Factory, wybierz dane regiony na poniższej stronie, a następnie rozwiń węzeł **Analiza**, aby zlokalizować pozycję **Data Factory**: [Dostępność produktów według regionów](https://azure.microsoft.com/global-infrastructure/services/). Magazyny danych (na przykład Azure Storage lub Azure SQL Database) i jednostki obliczeniowe (takie jak HDInsight) używane przez usługę Data Factory mogą znajdować się w innych regionach.
1.  Wybierz pozycję  **Utwórz**.


1.  Po zakończeniu tworzenia zostanie wyświetlona strona  **Fabryka danych** . Wybierz kafelek  **Tworzenie i monitorowanie** , aby na osobnej karcie uruchomić aplikację interfejsu użytkownika usługi Data Factory.

    ![Uruchamianie aplikacji interfejsu użytkownika usługi Data Factory](media/transform-data-using-databricks-notebook/databricks-notebook-activity-image4.png)

## <a name="create-linked-services"></a>Tworzenie połączonych usług

W tej sekcji utworzysz połączoną usługę Databricks. Ta połączona usługa zawiera informacje o połączeniu z klastrem usługi Databricks:

### <a name="create-an-azure-databricks-linked-service"></a>Tworzenie połączonej usługi Azure Databricks

1.  Na stronie  **Wprowadzenie**  przejdź do karty  **Edycja**  na lewym panelu.

    ![Edytowanie nowej połączonej usługi](media/transform-data-using-databricks-notebook/get-started-page.png)

1.  Wybierz pozycję  **Połączenia**  w dolnej części okna, a następnie wybierz pozycję  **+ Nowy**.
    
    ![Tworzenie nowego połączenia](media/transform-data-using-databricks-notebook/databricks-notebook-activity-image6.png)

1.  W oknie  **Nowa połączona usługa**  wybierz pozycje  **Compute** \> **Azure Databricks**, a następnie pozycję  **Kontynuuj**.
    
    ![Określanie połączonej usługi Databricks](media/transform-data-using-databricks-notebook/databricks-notebook-activity-image7.png)

1.  W oknie  **Nowa połączona usługa**  wykonaj następujące kroki:
    
    1.  W polu **Nazwa** podaj ciąg ***AzureDatabricks\_LinkedService***.
    
    1.  Wybierz odpowiedni **obszar roboczy usługi Databricks**, w którym uruchomisz notes.

    1.  W pozycji **Wybierz klaster** wybierz opcję **Nowy klaster zadań**.
    
    1.  Dane w polu **Domena/region** powinny zostać wypełnione automatycznie.

    1.  W obszarze **Token dostępu** wygeneruj token na podstawie miejsca pracy usługi Azure Databricks. Procedurę można znaleźć [tutaj](https://docs.databricks.com/api/latest/authentication.html#generate-token).

    1.  W polu **Wersja klastra** wybierz opcję **4.0** (z oprogramowaniem Apache Spark 2.3.0 i Scala 2.11).

    1.  Na potrzeby tego samouczka w polu **Typ węzła klastra** wybierz opcję **Standard\_D3\_v2** w kategorii **Ogólnego przeznaczenia (HDD)**. 
    
    1.  W polu **Procesy robocze** podaj wartość **2**.
    
    1.  Wybierz pozycję **Zakończ**.

        ![Kończenie tworzenia połączonej usługi](media/transform-data-using-databricks-notebook/new-databricks-linkedservice.png)

## <a name="create-a-pipeline"></a>Tworzenie potoku

1.  Wybierz przycisk  **+**  (znak plus), a następnie wybierz pozycję  **Potok**  w menu.

    ![Przyciski do tworzenia nowego potoku](media/transform-data-using-databricks-notebook/databricks-notebook-activity-image9.png)

1.  Utwórz **parametr** do użycia w **potoku**. Później przekażesz ten parametr do działania notesu usługi Databricks. W pustym potoku kliknij kartę **Parametry**, a następnie wybierz pozycję **Nowy** i wpisz nazwę „**nazwa**”.

    ![Tworzenie nowego parametru](media/transform-data-using-databricks-notebook/databricks-notebook-activity-image10.png)

    ![Tworzenie parametru nazwa](media/transform-data-using-databricks-notebook/databricks-notebook-activity-image11.png)

1.  W przyborniku  **Działania**  rozwiń węzeł  **Databricks**. Przeciągnij działanie  **Notes**  z przybornika  **Działania**  na powierzchnię projektanta potoku.

    ![Przeciąganie notesu na powierzchnię projektanta](media/transform-data-using-databricks-notebook/new-adf-pipeline.png)

1.  We właściwościach okna działania **Notes**  usługi  **Databricks** u dołu wykonaj następujące kroki:

    a. Przejdź na kartę  **Azure Databricks** .

    b. Wybierz usługę  **AzureDatabricks\_LinkedService**  (utworzoną w ramach poprzedniej procedury).

    d. Przejdź do karty **Ustawienia**.

    d. Użyj polecenia Przeglądaj, aby wybrać wartość dla pozycji **Ścieżka notesu** usługi Databricks. W tym miejscu utworzymy notes i określimy ścieżkę. Ścieżkę notesu można uzyskać, wykonując kilka następnych kroków.

       1. Uruchom obszar roboczy usługi Azure Databricks.

       1. Utwórz **nowy folder** w miejscu pracy i nadaj mu nazwę **adftutorial**.

          ![Tworzenie nowego folderu](media/transform-data-using-databricks-notebook/databricks-notebook-activity-image13.png)

       1. W folderze **adftutorial** [utwórz nowy notes](https://docs.databricks.com/user-guide/notebooks/index.html#creating-a-notebook) (Python) i nadaj mu nazwę **mynotebook****.** Kliknij przycisk **Utwórz**.

          ![Tworzenie nowego notesu](media/transform-data-using-databricks-notebook/databricks-notebook-activity-image14.png)

          ![Ustawianie właściwości nowego notesu](media/transform-data-using-databricks-notebook/databricks-notebook-activity-image15.png)

       1. W nowo utworzonym notesie „mynotebook” dodaj następujący kod:

           ```
           # Creating widgets for leveraging parameters, and printing the parameters

           dbutils.widgets.text("input", "","")
           dbutils.widgets.get("input")
           y = getArgument("input")
           print "Param -\'input':"
           print y
           ```

           ![Tworzenie widżetów parametrów](media/transform-data-using-databricks-notebook/databricks-notebook-activity-image16.png)

       1. W tym przypadku **Ścieżka notesu** to **/adftutorial/mynotebook**.

1.  Przełącz się z powrotem do **narzędzia tworzenia interfejsu użytkownika usługi Data Factory**. Przejdź do karty **Ustawienia** w obszarze **Działanie notesu Notes1**. 
    
    a.  **Dodaj parametr** do działania notesu. Użyj tego samego parametru, który został dodany wcześniej do **potoku**.

       ![Dodawanie parametru](media/transform-data-using-databricks-notebook/new-adf-parameters.png)

    b.  Nadaj parametrowi nazwę **wejście** i podaj wartości w postaci wyrażenia **@pipeline().parameters.name**.

1.  Aby zweryfikować potok, wybierz przycisk  **Weryfikuj**  na pasku narzędzi. Wybierz przycisk  **\>\>**  (strzałka w prawo), aby zamknąć okno weryfikacji.

    ![Weryfikowanie potoku](media/transform-data-using-databricks-notebook/databricks-notebook-activity-image18.png)

1.  Wybierz pozycję  **Opublikuj wszystkie**. Interfejs użytkownika usługi Data Factory publikuje jednostki (połączone usług i potok) do usługi Azure Data Factory.

    ![Publikowanie nowych jednostek fabryki danych](media/transform-data-using-databricks-notebook/databricks-notebook-activity-image19.png)

## <a name="trigger-a-pipeline-run"></a>Wyzwalanie uruchomienia potoku

Wybierz pozycję  **Wyzwól**  na pasku narzędzi, a następnie wybierz pozycję  **Wyzwól teraz**.

![Wybieranie polecenia Wyzwól teraz](media/transform-data-using-databricks-notebook/databricks-notebook-activity-image20.png)

W oknie dialogowym **Uruchamianie potoku** zostanie wyświetlona prośba o podanie parametru **nazwa**. Jako parametru użyj w tym miejscu wartości **/path/filename**. Kliknij przycisk **Zakończ**.

![Podawanie wartości parametru nazwa](media/transform-data-using-databricks-notebook/databricks-notebook-activity-image21.png)

## <a name="monitor-the-pipeline-run"></a>Monitorowanie działania potoku

1.  Przejdź na kartę  **Monitorowanie** . Sprawdź, czy widzisz uruchomienie potoku. Utworzenie klastra zadań usługi Databricks, w którym jest wykonywany notes, trwa około 5–8 minut.

    ![Monitorowanie potoku](media/transform-data-using-databricks-notebook/databricks-notebook-activity-image22.png)

1.  Okresowo wybieraj pozycję  **Odśwież** , aby sprawdzić stan uruchomienia potoku.

1.  Aby wyświetlić uruchomienia działań skojarzone z uruchomieniem potoku, wybierz pozycję  **Wyświetl uruchomienia działań** w kolumnie  **Akcje** .

    ![Wyświetlanie uruchomień działań](media/transform-data-using-databricks-notebook/databricks-notebook-activity-image23.png)

Aby wrócić do widoku uruchomień potoków, możesz wybrać link  **Potoki**  u góry.

## <a name="verify-the-output"></a>Sprawdzanie danych wyjściowych

Po zalogowaniu się do **obszaru roboczego usługi Azure Databricks** możesz przejść na kartę **Klastry**, gdzie jest wyświetlany stan **zadania**. Dostępne wartości to *Oczekiwanie na wykonanie, Uruchomione i Zakończone*.

![Wyświetlanie klastra zadań i zadania](media/transform-data-using-databricks-notebook/databricks-notebook-activity-image24.png)

Aby uzyskać więcej szczegółów, możesz kliknąć **nazwę zadania**. Po pomyślnym uruchomieniu można sprawdzić poprawność przekazanych parametrów i dane wyjściowe notesu Python.

![Wyświetlanie szczegółów uruchomienia i danych wyjściowych](media/transform-data-using-databricks-notebook/databricks-output.png)

## <a name="next-steps"></a>Następne kroki

Potok w tym przykładzie wyzwala działanie notesu usługi Databricks i przekazuje do niego parametr. W tym samouczku omówiono:

  - Tworzenie fabryki danych.

  - Tworzenie potoku, który używa działania notesu usługi Databricks.

  - Wyzwalanie uruchomienia potoku.

  - Monitorowanie uruchomienia potoku.
