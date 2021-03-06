---
title: Szybki start przy użyciu witryny Azure Portal
titleSuffix: Azure Machine Learning service
description: Rozpocznij pracę z usługą Azure Machine Learning. Użyj witryny Azure Portal, aby utworzyć obszar roboczy, który stanowi podstawowy blok w chmurze umożliwiający eksperymentowanie z modelami uczenia maszynowego, ich trenowanie oraz wdrażanie.
services: machine-learning
ms.service: machine-learning
ms.component: core
ms.topic: quickstart
ms.reviewer: sgilley
author: hning86
ms.author: haining
ms.date: 12/04/2018
ms.custom: seodec18
ms.openlocfilehash: 14c500d77cc0e67aaade5e6be490f599f39bfad5
ms.sourcegitcommit: 9f87a992c77bf8e3927486f8d7d1ca46aa13e849
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/28/2018
ms.locfileid: "53807724"
---
# <a name="quickstart-use-the-azure-portal-to-get-started-with-azure-machine-learning"></a>Szybki start: Rozpoczynanie pracy z usługą Azure Machine Learning w witrynie Azure Portal

W tym przewodniku Szybki start utworzysz obszar roboczy usługi Azure Machine Learning przy użyciu witryny Azure Portal. Ten obszar roboczy to podstawowy blok w chmurze umożliwiający eksperymentowanie z modelami uczenia maszynowego, ich uczenie oraz wdrażanie za pomocą usługi Machine Learning. Ten przewodnik Szybki start korzysta z zasobów w chmurze i nie wymaga żadnej instalacji. Aby zamiast tego skonfigurować własny serwer notesów Jupyter Notebook, zobacz [Szybki start: Rozpoczynanie pracy z usługą Azure Machine Learning w języku Python](quickstart-create-workspace-with-python.md).  
 
> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE2F9Ad]

W tym przewodniku Szybki start wykonasz następujące czynności:

* Tworzenie obszaru roboczego w subskrypcji platformy Azure.
* Wypróbowanie jego działania za pomocą języka Python w notesie platformy Azure i rejestrowanie wartości z wielu iteracji.
* Wyświetlanie zarejestrowanych wartości w obszarze roboczym.

Do obszaru roboczego zostaną automatycznie dodane następujące zasoby platformy Azure, gdy będą dostępne w regionie:

  - [Azure Container Registry](https://azure.microsoft.com/services/container-registry/)
  - [Azure Storage](https://azure.microsoft.com/services/storage/)
  - [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) 
  - [Usługa Azure Key Vault](https://azure.microsoft.com/services/key-vault/)

Utworzone zasoby mogą być używane jako wstępnie wymagane składniki w innych samouczkach usługi Machine Learning i artykułach z instrukcjami. Podobnie jak w przypadku innych usług platformy Azure korzystanie z pewnych zasobów skojarzonych z usługą Machine Learning jest ograniczone określonymi limitami. Przykładem jest rozmiar klastra obliczeniowego. Dowiedz się więcej o [limitach domyślnych i sposobach zwiększania limitów przydziału](how-to-manage-quotas.md).

Jeśli nie masz subskrypcji Azure, przed rozpoczęciem utwórz bezpłatne konto. Wypróbuj [bezpłatną lub płatną wersję usługi Azure Machine Learning](http://aka.ms/AMLFree) już dziś.


## <a name="create-a-workspace"></a>Tworzenie obszaru roboczego 

[!INCLUDE [aml-create-portal](../../../includes/aml-create-in-portal.md)]

Na stronie obszaru roboczego wybierz pozycję `Explore your Azure Machine Learning service Workspace`.

 ![Eksplorowanie obszaru roboczego](./media/quickstart-get-started/explore_aml.png)


## <a name="use-the-workspace"></a>Korzystanie z obszaru roboczego

Teraz zobaczysz, jak obszar roboczy ułatwia zarządzanie skryptami uczenia maszynowego. W tej sekcji wykonasz następujące kroki:

* Otwieranie notesu w usłudze Azure Notebooks.
* Uruchamianie kodu, który tworzy niektóre rejestrowane wartości.
* Wyświetlanie zarejestrowanych wartości w obszarze roboczym.

W tym przykładzie pokazano, jak obszar roboczy może pomóc w śledzeniu informacji wygenerowanych przez skrypt. 

### <a name="open-a-notebook"></a>Otwieranie notesu 

Usługa Azure Notebooks udostępnia bezpłatną platformę w chmurze do przechowywania notesów Jupyter, które są wstępnie skonfigurowane do obsługi wszystkich elementów potrzebnych, aby uruchomić usługę Machine Learning.  

Wybierz pozycję `Open Azure Notebooks`, aby wypróbować pierwszy eksperyment.

 ![Otwieranie usługi Azure Notebooks](./media/quickstart-get-started/explore_ws.png)

Organizacja może wymagać [zgody administratora](https://notebooks.azure.com/help/signing-up/work-or-school-account/admin-consent) przed zalogowaniem się.

Zaloguj się do notesów platformy Azure przy użyciu tego samego konta, którego używasz do logowania się do witryny Azure Portal.  Po zalogowaniu zostanie otwarta nowa karta z wyświetlonym monitem `Clone Library`. Wybierz pozycję `Clone`.


### <a name="run-the-notebook"></a>Uruchamianie notesu

Oprócz dwóch notesów zobaczysz jeszcze plik `config.json`. Ten plik konfiguracji zawiera informacje o utworzonym obszarze roboczym.  

Wybierz pozycję `01.run-experiment.ipynb`, aby otworzyć notes.

Uruchom komórki pojedynczo (Shift+Enter). Możesz też uruchomić cały notes, wybierając pozycje `Cells`  >  `Run All`. Gdy obok komórki jest wyświetlana gwiazdka __*__, oznacza to, że komórka jest uruchomiona. Po zakończeniu działania kodu tej komórki pojawi się liczba. 

Po zakończeniu uruchamiania wszystkich komórek w notesie możesz wyświetlić zarejestrowane wartości w swoim obszarze roboczym.

## <a name="view-logged-values"></a>Wyświetlanie zarejestrowanych wartości

Po uruchomieniu wszystkich komórek notesu wróć do strony portalu.  

Wybierz pozycję `View Experiments`.

![Wyświetlanie eksperymentów](./media/quickstart-get-started/view_exp.png)

Zamknij wyskakujące okienko `Reports`.

Wybierz pozycję `my-first-experiment`.

Przejrzyj informacje o wykonanym właśnie przebiegu. Przewiń stronę w dół do tabeli przebiegów. Wybierz link liczby przebiegów.

 ![Link historii przebiegów](./media/quickstart-get-started/report.png)

Zostaną wyświetlone wykresy utworzone automatycznie na podstawie zarejestrowanych wartości. Zawsze w przypadku zarejestrowania wielu wartości z tym samym parametrem nazwa wykres jest generowany automatycznie.

   ![Wyświetlanie historii](./media/quickstart-get-started/plots.png)

Kod obliczania przybliżonej liczby pi używa wartości losowych, dlatego wykresy będą przedstawiać różne wartości.  

## <a name="clean-up-resources"></a>Oczyszczanie zasobów 

[!INCLUDE [aml-delete-resource-group](../../../includes/aml-delete-resource-group.md)]

Możesz też zachować grupę zasobów i usunąć jeden obszar roboczy. Wyświetl właściwości obszaru roboczego i wybierz pozycję **Usuń**.

## <a name="next-steps"></a>Następne kroki

Utworzono zasoby umożliwiające eksperymentowanie i wdrażanie modeli. Uruchomiono też kod w notesie. Zbadano historię przebiegów dotyczącą tego kodu w obszarze roboczym w chmurze.

Aby poznać szczegółowo środowisko przepływu pracy, wykonaj czynności opisane w samouczku dotyczącym trenowania i wdrażania modelu w usłudze Machine Learning:  

> [!div class="nextstepaction"]
> [Samouczek: trenowanie modelu klasyfikacji obrazów](tutorial-train-models-with-aml.md)
