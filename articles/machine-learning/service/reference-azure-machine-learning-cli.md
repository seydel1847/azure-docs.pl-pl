---
title: Rozszerzenie interfejsu wiersza polecenia do uczenia maszynowego
titleSuffix: Azure Machine Learning service
description: Dowiedz się więcej o rozszerzenie interfejsu wiersza polecenia usługi Azure Machine Learning dla wiersza polecenia platformy Azure. Wiersza polecenia platformy Azure jest narzędziem wiersza polecenia dla wielu platform, która umożliwia pracę z zasobami w chmurze platformy Azure. Rozszerzenie usługi Machine Learning umożliwia pracę z usługą Azure Machine Learning.
services: machine-learning
ms.service: machine-learning
ms.component: core
ms.topic: conceptual
ms.reviewer: jmartens
ms.author: jordane
author: jpe316
ms.date: 12/04/2018
ms.custom: seodec18
ms.openlocfilehash: bbe843f3481c6cd15f2c14386088cbb8d2d355d6
ms.sourcegitcommit: d61faf71620a6a55dda014a665155f2a5dcd3fa2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/04/2019
ms.locfileid: "54053129"
---
# <a name="use-the-cli-extension-for-azure-machine-learning-service"></a>Na użytek rozszerzenie interfejsu wiersza polecenia usługi Azure Machine Learning

Interfejsu wiersza polecenia usługi Azure Machine Learning to rozszerzenie [wiersza polecenia platformy Azure](https://docs.microsoft.com/cli/azure/?view=azure-cli-latest), interfejs wiersza polecenia dla wielu platform na platformie Azure. To rozszerzenie zawiera polecenia służące do pracy z usługą Azure Machine Learning z poziomu wiersza polecenia. Umożliwia tworzenia skryptów automatyzujących przepływy pracy uczenia maszynowego. Na przykład można utworzyć skrypty, które wykonują następujące czynności:

+ Uruchamianie eksperymentów w celu tworzenia modeli uczenia maszynowego

+ Zarejestruj modele uczenia maszynowego do użycia przez klientów

+ Pakowanie, wdrażanie i śledzenia w cyklu życia modeli usługi machine learning

Interfejs wiersza polecenia nie jest zamiennikiem dla zestawu SDK usługi Azure Machine Learning. To narzędzie służy do uzupełniające zoptymalizowane pod kątem obsługi wysoce sparametryzowanych zadań, takich jak:

* Tworzenie zasobów obliczeniowych

* przesyłanie eksperymentu sparametryzowane

* Rejestracja modelu

* Tworzenie obrazu

* Wdrażanie usługi

## <a name="prerequisites"></a>Wymagania wstępne


* Aby korzystać z interfejsu wiersza polecenia, musi mieć subskrypcję platformy Azure. Jeśli nie masz subskrypcji Azure, przed rozpoczęciem utwórz bezpłatne konto. Wypróbuj [bezpłatną lub płatną wersję usługi Azure Machine Learning](http://aka.ms/AMLFree) już dziś.

* [Wiersza polecenia platformy Azure](https://docs.microsoft.com/cli/azure/?view=azure-cli-latest).

## <a name="install-the-extension"></a>Instalowanie rozszerzenia

Aby zainstalować rozszerzenie interfejsu wiersza polecenia Machine Learning, użyj następującego polecenia:

```azurecli-interactive
az extension add -s https://azuremlsdktestpypi.blob.core.windows.net/wheels/sdk-release/Preview/E7501C02541B433786111FE8E140CAA1/azure_cli_ml-1.0.6-py2.py3-none-any.whl --pip-extra-index-urls  https://azuremlsdktestpypi.azureedge.net/sdk-release/Preview/E7501C02541B433786111FE8E140CAA1
```

Po wyświetleniu monitu wybierz `y` można zainstalować rozszerzenia.

Aby sprawdzić, czy rozszerzenie zostało zainstalowane, użyj następującego polecenia, aby wyświetlić listę określonych ML podpoleceń polecenia:

```azurecli-interactive
az ml -h
```

> [!TIP]
> Aby zaktualizować rozszerzenie, należy najpierw __Usuń__ , a następnie __zainstalować__ go. Spowoduje to zainstalowanie najnowszej wersji.

## <a name="remove-the-extension"></a>Usuń rozszerzenie

Aby usunąć rozszerzenie interfejsu wiersza polecenia, użyj następującego polecenia:

```azurecli-interactive
az extension remove -n azure-cli-ml
```

## <a name="resource-management"></a>Zarządzanie zasobami

Poniższe polecenia pokazują, jak zarządzać zasoby używane przez usługi Azure Machine Learning przy użyciu interfejsu wiersza polecenia.


+ Utwórz obszar roboczy usługi Azure Machine Learning:

    ```azurecli-interactive
    az ml workspace create -n myworkspace -g myresourcegroup
    ```

+ Ustaw domyślnego obszaru roboczego:

    ```azurecli-interactive
    az configure --defaults aml_workspace=myworkspace group=myresourcegroup
    ```

+ Tworzenie zarządzanego obliczeniowego elementu docelowego dla rozproszonego szkolenia:

    ```azurecli-interactive
    az ml computetarget create amlcompute -n mycompute --max_nodes 4 --size Standard_NC6
    ```

* Aktualizowanie zarządzanych obliczeniowego elementu docelowego:

    ```azurecli-interactive
    az ml computetarget update --name mycompute --workspace –-group --max_nodes 4 --min_nodes 2 --idle_time 300
    ```

* Dołącz obiekt docelowy niezarządzanych obliczeń szkolenia lub wdrożenia:

    ```azurecli-interactive
    az ml computetarget attach aks -n myaks -i myaksresourceid -g myrg -w myworkspace
    ```

## <a name="experiments"></a>Eksperymenty

Poniższe polecenia pokazują, jak pracować z eksperymentów przy użyciu interfejsu wiersza polecenia:

* Dołączanie projektu (Uruchom konfigurację) przed przesłaniem eksperymentu:

    ```azurecli-interactive
    az ml project attach --experiment-name myhistory
    ```

* Rozpocznij przebieg eksperymentu. Korzystając z tego polecenia, należy określić nazwę `.runconfig` pliku, który zawiera konfiguracji uruchamiania. Obliczeniowego elementu docelowego używa konfiguracji uruchamiania do utworzenia środowiska do szkolenia modelu. W tym przykładzie konfiguracji uruchamiania jest ładowany z `./aml_config/myrunconfig.runconfig` pliku.

    ```azurecli-interactive
    az ml run submit -c myrunconfig train.py
    ```

    Domyślne `.runconfig` plików o nazwie `docker.runconfig` i `local.runconfig` są tworzone po dołączeniu projekt za pomocą `az ml project attach` polecenia. Użytkownik może być konieczne zmodyfikowanie tych przed ich użyciem w celu nauczenia modelu. 

    Możesz również utworzyć programowo przy użyciu konfigurację uruchomieniową [RunConfiguration](https://docs.microsoft.com/python/api/azureml-core/azureml.core.runconfig.runconfiguration?view=azure-ml-py) klasy. Po utworzeniu można użyć `save()` metodę w celu utworzenia `.runconfig` pliku.

* Wyświetlanie listy przesłanych eksperymentów:

    ```azurecli-interactive
    az ml history list
    ```

## <a name="model-registration-image-creation--deployment"></a>Rejestracja modelu, tworzenie obrazu i wdrożenie

Poniższe polecenia pokazują, jak rejestrowanie uczonego modelu, a następnie wdrożyć go jako usługę produkcyjną:

+ Zarejestruj model przy użyciu usługi Azure Machine Learning:

  ```azurecli-interactive
  az ml model register -n mymodel -m sklearn_regression_model.pkl
  ```

+ Utwórz obraz, który zawiera Twoje modelu uczenia maszynowego i zależności: 

  ```azurecli-interactive
  az ml image create container -n myimage -r python -m mymodel:1 -f score.py -c myenv.yml
  ```

+ Wdrażanie obrazu obliczeniowego elementu docelowego:

  ```azurecli-interactive
  az ml service create aci -n myaciservice --image-id myimage:1
  ```
