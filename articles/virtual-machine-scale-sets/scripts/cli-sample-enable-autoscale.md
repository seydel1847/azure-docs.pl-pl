---
title: Przykłady interfejsu wiersza polecenia platformy Azure — włączanie automatycznego skalowania opartego na hoście | Microsoft Docs
description: Przykłady interfejsu wiersza polecenia platformy Azure
services: virtual-machine-scale-sets
documentationcenter: ''
author: zr-msft
manager: jeconnoc
editor: ''
tags: azure-resource-manager
ms.assetid: ''
ms.service: virtual-machine-scale-sets
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/27/2018
ms.author: zarhoads
ms.custom: mvc
ms.openlocfilehash: 1172d9a3a2c36d41bc081454936ef8b570d99aba
ms.sourcegitcommit: 62759a225d8fe1872b60ab0441d1c7ac809f9102
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2018
ms.locfileid: "49465903"
---
# <a name="automatically-scale-a-virtual-machine-scale-set-with-the-azure-cli"></a>Automatyczne skalowanie zestawu skalowania maszyn wirtualnych przy użyciu interfejsu wiersza polecenia platformy Azure
Ten skrypt tworzy zestaw skalowania maszyn wirtualnych z systemem Ubuntu i wykorzystuje oparte na hoście metryki do automatycznego skalowania w miarę zmian obciążenia procesora CPU.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Przykładowy skrypt
[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine-scale-sets/auto-scale-host-metrics/auto-scale-host-metrics.sh "Automatically scale a virtual machine scale set")]

## <a name="clean-up-deployment"></a>Czyszczenie wdrożenia
Uruchom następujące polecenie, aby usunąć grupę zasobów, zestaw skalowania i wszystkie powiązane zasoby.

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Objaśnienia dla skryptu
Ten skrypt zawiera następujące polecenia służące do tworzenia grupy zasobów, zestawu skalowania maszyn wirtualnych i wszystkich powiązanych zasobów. Każde polecenie w tabeli stanowi link do dokumentacji polecenia.

| Polecenie | Uwagi |
|---|---|
| [az group create](/cli/azure/ad/group#az_ad_group_create) | Tworzy grupę zasobów, w której są przechowywane wszystkie zasoby. |
| [az vmss create](/cli/azure/vmss#az_vmss_create) | Tworzy zestaw skalowania maszyn wirtualnych i łączy go z siecią wirtualną, podsiecią i sieciową grupą zabezpieczeń. Zostanie też utworzony moduł równoważenia obciążenia w celu dystrybucji ruchu do wielu wystąpień maszyn wirtualnych. To polecenie określa również obraz maszyny wirtualnej do użycia oraz poświadczenia administracyjne.  |
| [az monitor autoscale-settings create](/cli/azure/monitor/autoscale-settings#az_monitor_autoscale_settings_create) | Tworzy i stosuje reguły automatycznego skalowania do zestawu skalowania maszyn wirtualnych. |
| [az group delete](/cli/azure/ad/group#delete) | Usuwa grupę zasobów wraz ze wszystkimi zagnieżdżonymi zasobami. |

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji na temat interfejsu wiersza polecenia platformy Azure, zobacz [dokumentację interfejsu wiersza polecenia platformy Azure](https://docs.microsoft.com/cli/azure/overview).

Dodatkowe przykłady skryptów interfejsu wiersza polecenia platformy Azure dotyczących zestawu skalowania maszyn wirtualnych można znaleźć w [dokumentacji zestawu skalowania maszyn wirtualnych platformy Azure](../cli-samples.md).