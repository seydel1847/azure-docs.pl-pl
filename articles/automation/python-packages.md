---
title: Zarządzanie pakietami języka Python 2 w usłudze Azure Automation
description: W tym artykule opisano sposób zarządzania pakietami języka Python 2 w usłudze Azure Automation.
services: automation
ms.service: automation
ms.subservice: process-automation
author: georgewallace
ms.author: gwallace
ms.date: 09/11/2018
ms.topic: conceptual
manager: carmonm
ms.openlocfilehash: de0998dffeac54db5311bbcde1c9499488b23556
ms.sourcegitcommit: 9999fe6e2400cf734f79e2edd6f96a8adf118d92
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/22/2019
ms.locfileid: "54434976"
---
# <a name="manage-python-2-packages-in-azure-automation"></a>Zarządzanie pakietami języka Python 2 w usłudze Azure Automation

Usługa Azure Automation umożliwia uruchamianie elementów runbook języka Python 2, na platformie Azure oraz w systemie Linux hybrydowych procesów roboczych Runbook. Aby ułatwić uproszczenia elementów runbook, umożliwia pakiety języka Python zaimportuj moduły, które są potrzebne. W tym artykule opisano sposób zarządzania i korzystanie z pakietów języka Python w usłudze Azure Automation.

## <a name="import-packages"></a>Importowanie pakietów

Na koncie usługi Automation wybierz **pakiety języka Python 2** w obszarze **zasoby udostępnione**. Kliknij przycisk **+ Dodaj pakiet języka Python 2**.

![Dodaj pakiet języka Python](media/python-packages/add-python-package.png)

Na **Dodaj pakiet programu Python 2** wybierz pakiet lokalny do przekazania. Pakiet może być `.whl` pliku lub `.tar.gz` pliku. Wybranie tej opcji, kliknij przycisk **OK** do przekazania pakietu.

![Dodaj pakiet języka Python](media/python-packages/upload-package.png)

Po zaimportowaniu pakietu jest wyświetlana na **pakiety języka Python 2** strony na Twoim koncie usługi Automation. Jeśli musisz usunąć pakiet, wybierz pakiet i wybierz polecenie **Usuń** na stronie pakiet.

![Lista pakietów](media/python-packages/package-list.png)

## <a name="use-a-package-in-a-runbook"></a>Użyj pakietu w elemencie runbook

Po zaimportowaniu pakietu można teraz używać go w elemencie runbook. W poniższym przykładzie użyto [ pakiet narzędzia usługi Azure Automation](https://github.com/azureautomation/azure_automation_utility). Ten pakiet umożliwia korzystanie z języka Python w usłudze Azure Automation. Aby użyć pakietu, postępuj zgodnie z instrukcjami w repozytorium GitHub i dodać go do elementu runbook za pomocą `from azure_automation_utility import get_automation_runas_credential` na przykład w celu importowania funkcji pobierania konto Uruchom jako.

```python
import azure.mgmt.resource
import automationassets
from azure_automation_utility import get_automation_runas_credential

# Authenticate to Azure using the Azure Automation RunAs service principal
runas_connection = automationassets.get_automation_connection("AzureRunAsConnection")
azure_credential = get_automation_runas_credential()

# Intialize the resource management client with the RunAs credential and subscription
resource_client = azure.mgmt.resource.ResourceManagementClient(
    azure_credential,
    str(runas_connection["SubscriptionId"]))

# Get list of resource groups and print them out
groups = resource_client.resource_groups.list()
for group in groups:
    print group.name
```

## <a name="develop-and-test-runbooks-offline"></a>Tworzenie i testowanie elementów runbook w trybie offline

Aby tworzyć i testować runbook języka Python 2 w trybie offline, należy użyć [języka python w usłudze Azure Automation emulowane zasoby](https://github.com/azureautomation/python_emulated_assets) modułu w witrynie GitHub. Ten moduł można odwoływać się do udostępnionych zasobów, takich jak poświadczenia, zmienne, połączenia i certyfikaty.

## <a name="next-steps"></a>Kolejne kroki

Aby rozpocząć pracę z elementami runbook języka Python 2, zobacz [Mój pierwszy element runbook Python 2](automation-first-runbook-textual-python2.md)
