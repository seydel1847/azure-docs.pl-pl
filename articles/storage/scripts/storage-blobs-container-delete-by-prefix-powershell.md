---
title: Przykładowy skrypt programu Azure PowerShell — usuwanie kontenerów na podstawie prefiksu | Microsoft Docs
description: Usuwanie kontenerów obiektów blob w usłudze Azure Storage na podstawie prefiksu nazwy kontenera.
services: storage
documentationcenter: na
author: tamram
manager: timlt
editor: tysonn
ms.assetid: ''
ms.custom: mvc
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: sample
ms.date: 06/13/2017
ms.author: tamram
ms.openlocfilehash: b98b42be170c37710435d1aad61707a4ed01851f
ms.sourcegitcommit: e7312c5653693041f3cbfda5d784f034a7a1a8f1
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/11/2019
ms.locfileid: "54214424"
---
# <a name="delete-containers-based-on-container-name-prefix"></a>Usuwanie kontenerów na podstawie prefiksu nazwy kontenera

Ten skrypt usuwa kontenery z usługi Azure Blob Storage na podstawie prefiksu nazwy kontenera.

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Przykładowy skrypt

[!code-powershell[main](../../../powershell_scripts/storage/delete-containers-by-prefix/delete-containers-by-prefix.ps1 "Delete containers by prefix")]

## <a name="clean-up-deployment"></a>Czyszczenie wdrożenia 

Uruchom następujące polecenie, aby usunąć grupę zasobów, pozostałe kontenery i wszystkie powiązane zasoby.

```powershell
Remove-AzResourceGroup -Name containerdeletetestrg
```

## <a name="script-explanation"></a>Objaśnienia dla skryptu

Ten skrypt zawiera następujące polecenia służące do usunięcia kontenerów na podstawie prefiksu nazwy kontenera. Każda pozycja w tabeli stanowi link do dokumentacji polecenia.

| Polecenie | Uwagi |
|---|---|
| [Get-AzStorageAccount](/powershell/module/az.storage/get-azstorageaccount) | Pobiera określone konto usługi Storage lub wszystkie konta usługi Storage w grupie zasobów lub subskrypcji. |
| [Get-AzStorageContainer](/powershell/module/az.storage/Get-AzStorageContainer) | Zwraca listę kontenerów magazynu skojarzonych z kontem magazynu. |
| [Remove-AzStorageContainer](/powershell/module/az.storage/Remove-AzStorageContainer) | Usuwa określony kontener magazynu. |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na temat modułu Azure PowerShell, zobacz [dokumentację programu Azure PowerShell](/powershell/azure/overview).

Więcej przykładowych skryptów programu PowerShell dla usługi Storage można znaleźć na stronie [PowerShell samples for Azure Blob storage (Przykładowe skrypty programu PowerShell dla usługi Azure Blob Storage)](../blobs/storage-samples-blobs-powershell.md).
