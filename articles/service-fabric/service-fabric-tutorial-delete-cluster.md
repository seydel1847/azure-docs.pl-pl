---
title: Usuwanie klastra usługi Service Fabric na platformie Azure | Microsoft Docs
description: W ramach tego samouczka dowiesz się, jak usunąć klaster usługi Service Fabric hostowany na platformie Azure razem ze wszystkimi zasobami. Istnieje możliwość usunięcia grupy zasobów zawierającej klaster lub selektywnego usuwania zasobów.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: ''
ms.assetid: ''
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: tutorial
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 09/26/2018
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 70c5fa5de627b69623b1cce6929615f4e99e2a05
ms.sourcegitcommit: b7e5bbbabc21df9fe93b4c18cc825920a0ab6fab
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/27/2018
ms.locfileid: "47410825"
---
# <a name="tutorial-remove-a-service-fabric-cluster-running-in-azure"></a>Samouczek: usuwanie klastra usługi Service Fabric uruchomionego na platformie Azure

Ten samouczek to czwarta część serii. Przedstawiono w nim sposób usuwania klastra usługi Service Fabric uruchomionego na platformie Azure. Aby całkowicie usunąć klaster usługi Service Fabric, musisz również usunąć wszystkie zasoby używane przez klaster. Dostępne są dwie opcje: usunięcie grupy zasobów, do której należy klaster (co powoduje usunięcie zasobu klastra i wszystkich innych zasobów w grupie zasobów) lub usunięcie konkretnie zasobu klastra i jego powiązanych zasobów (lecz nie innych zasobów w grupie zasobów).

Ten samouczek zawiera informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Usuwanie grupy zasobów i jej wszystkich zasobów
> * Selektywne usuwanie zasobów z grupy zasobów

Ta seria samouczków zawiera informacje na temat wykonywania następujących czynności:
> [!div class="checklist"]
> * Tworzenie bezpiecznego [klastra systemu Windows](service-fabric-tutorial-create-vnet-and-windows-cluster.md) lub [klastra systemu Linux](service-fabric-tutorial-create-vnet-and-linux-cluster.md) na platformie Azure przy użyciu szablonu
> * [Skalowanie klastra na zewnątrz lub do wewnątrz](service-fabric-tutorial-scale-cluster.md)
> * [Uaktualnianie środowiska uruchomieniowego klastra](service-fabric-tutorial-upgrade-cluster.md)
> * Usuwanie klastra

## <a name="prerequisites"></a>Wymagania wstępne

Przed rozpoczęciem tego samouczka:

* Jeśli nie masz subskrypcji platformy Azure, utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)
* Zainstaluj [moduł Azure PowerShell w wersji 4.1 lub nowszej](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) albo [interfejs wiersza polecenia platformy Azure](/cli/azure/install-azure-cli).
* Utwórz bezpieczny [klaster systemu Windows](service-fabric-tutorial-create-vnet-and-windows-cluster.md) lub [klaster systemu Linux](service-fabric-tutorial-create-vnet-and-linux-cluster.md) na platformie Azure.

## <a name="delete-the-resource-group-containing-the-service-fabric-cluster"></a>Usuwanie grupy zasobów zawierającej klaster usługi Service Fabric
Najprostszym sposobem na usunięcie klastra i wszystkich wykorzystywanych przez niego zasobów jest usunięcie grupy zasobów.

Zaloguj się do platformy Azure i wybierz identyfikator subskrypcji, za pomocą którego chcesz usunąć klaster.  Identyfikator subskrypcji można uzyskać po zalogowaniu się do [witryny Azure Portal](http://portal.azure.com). Usuń grupę zasobów i wszystkie zasoby klastra, korzystając z polecenia cmdlet [Remove-AzureRMResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) lub polecenia [az group delete](/cli/azure/group?view=azure-cli-latest#az_group_delete).

```powershell
Connect-AzureRmAccount
Set-AzureRmContext -SubscriptionId <guid>
$groupname = "sfclustertutorialgroup"
Remove-AzureRmResourceGroup -Name $groupname -Force
```

```azurecli
az login
az account set --subscription <guid>
ResourceGroupName="sfclustertutorialgroup"
az group delete --name $ResourceGroupName
```

## <a name="selectively-delete-the-cluster-resource-and-the-associated-resources"></a>Selektywne usuwanie zasobu klastra i skojarzonych zasobów
Jeśli grupa zasobów zawiera tylko zasoby powiązane z klastrem usługi Service Fabric do usunięcia, to łatwiej usunąć całą grupę zasobów. Jeśli chcesz selektywnie usunąć zasoby z grupy zasobów i zachować zasoby nieskojarzone z klastrem, wykonaj następujące kroki.

Wyświetl zasoby w grupie zasobów:

```powershell
Connect-AzureRmAccount
Set-AzureRmContext -SubscriptionId <guid>
$groupname = "sfclustertutorialgroup"
Get-AzureRmResource -ResourceGroupName $groupname | ft
```

```azurecli
az login
az account set --subscription <guid>
ResourceGroupName="sfclustertutorialgroup"
az resource list --resource-group $ResourceGroupName
```

Dla każdego z zasobów do usunięcia uruchom następujący skrypt:

```powershell
Remove-AzureRmResource -ResourceName "<name of the Resource>" -ResourceType "<Resource Type>" -ResourceGroupName $groupname -Force
```

```azurecli
az resource delete --name "<name of the Resource>" --resource-type "<Resource Type>" --resource-group $ResourceGroupName
```

Aby usunąć zasób klastra, uruchom następujący skrypt:

```powershell
Remove-AzureRmResource -ResourceName "<name of the Resource>" -ResourceType "Microsoft.ServiceFabric/clusters" -ResourceGroupName $groupname -Force
```

```azurecli
az resource delete --name "<name of the Resource>" --resource-type "Microsoft.ServiceFabric/clusters" --resource-group $ResourceGroupName
```

## <a name="next-steps"></a>Następne kroki

W niniejszym samouczku zawarto informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Usuwanie grupy zasobów i jej wszystkich zasobów
> * Selektywne usuwanie zasobów z grupy zasobów

Po ukończeniu tego samouczka spróbuj wykonać następujące czynności:
* Dowiedz się, jak przeprowadzić inspekcję klastra usługi Service Fabric i zarządzać nim przy użyciu programu [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).
* Dowiedz się, jak [zastosować poprawki systemu operacyjnego Windows](service-fabric-patch-orchestration-application.md) lub [zastosować poprawki systemu operacyjnego Linux](service-fabric-patch-orchestration-application-linux.md) w węzłach klastra.
* Dowiedz się, jak agregować i zbierać zdarzenia z [klastrów systemu Windows](service-fabric-diagnostics-event-aggregation-wad.md) lub [klastrów systemu Linux](service-fabric-diagnostics-event-aggregation-lad.md) oraz jak [skonfigurować usługę Log Analytics](service-fabric-diagnostics-oms-setup.md) pod kątem monitorowania zdarzeń klastra.