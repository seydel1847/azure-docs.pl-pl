---
title: Aby zmienić rozmiar maszyny Wirtualnej z systemem Windows na platformie Azure przy użyciu programu PowerShell | Dokumentacja firmy Microsoft
description: Zmień rozmiar maszyny wirtualnej Windows utworzone w modelu wdrażania usługi Resource Manager przy użyciu programu Azure Powershell.
services: virtual-machines-windows
documentationcenter: ''
author: cynthn
manager: jeconnoc
editor: ''
tags: azure-resource-manager
ms.assetid: 057ff274-6dad-415e-891c-58f8eea9ed78
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2018
ms.author: cynthn
ms.openlocfilehash: 6bd41115f586bf2969dacb772f097d84654f0306
ms.sourcegitcommit: cc4fdd6f0f12b44c244abc7f6bc4b181a2d05302
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/25/2018
ms.locfileid: "47092598"
---
# <a name="resize-a-windows-vm"></a>Zmień rozmiar Windows maszyny Wirtualnej

W tym artykule dowiesz się, jak przenieść Maszynę wirtualną do innego [rozmiar maszyny Wirtualnej](sizes.md) przy użyciu programu Azure Powershell.

Po utworzeniu maszyny wirtualnej (VM), możesz skalować maszynę Wirtualną w górę lub w dół, zmieniając rozmiar maszyny Wirtualnej. W niektórych przypadkach możesz najpierw cofnąć maszyny Wirtualnej. Może to nastąpić, jeśli nowy rozmiar jest niedostępny w klastrze sprzętu, który obecnie udostępnia maszyny Wirtualnej.

Jeśli maszyna wirtualna korzysta z usługi Premium Storage, upewnij się, że wybierasz **s** wersję rozmiar Aby uzyskać pomoc techniczną Premium Storage. Na przykład wybrać Standard_E4**s**_v3 zamiast maszyna wirtualna Standard_E4_v3.

## <a name="resize-a-windows-vm-not-in-an-availability-set"></a>Zmień rozmiar maszyny Wirtualnej z systemem Windows nie znajduje się w zestawie dostępności

Ustaw zmienne. Zastąp wartości, podając własne informacje.

```powershell
$resourceGroup = "myResourceGroup"
$vmName = "myVM"
```

Wyświetl listę rozmiarów maszyn wirtualnych, które są dostępne w klastrze sprzętu, w którym jest hostowana maszyna wirtualna. 
   
```powershell
Get-AzureRmVMSize -ResourceGroupName $resourceGroup -VMName $vmName 
```

Jeśli żądany rozmiar jest wymieniony, uruchom następujące polecenia, aby zmienić rozmiar maszyny Wirtualnej. Jeśli żądany rozmiar nie ma na liście, przejdź do kroku 3.
   
```powershell
$vm = Get-AzureRmVM -ResourceGroupName $resourceGroup -VMName $vmName
$vm.HardwareProfile.VmSize = "<newVMsize>"
Update-AzureRmVM -VM $vm -ResourceGroupName $resourceGroup
```

Jeśli żądany rozmiar nie ma na liście, uruchom następujące polecenia, aby cofnąć przydział maszyny Wirtualnej, zmień jego rozmiar i ponownie maszynę Wirtualną. Zastąp **<newVMsize>** z żądany rozmiar.
   
```powershell
Stop-AzureRmVM -ResourceGroupName $resourceGroup -Name $vmName -Force
$vm = Get-AzureRmVM -ResourceGroupName $resourceGroup -VMName $vmName
$vm.HardwareProfile.VmSize = "<newVMSize>"
Update-AzureRmVM -VM $vm -ResourceGroupName $resourceGroup
Start-AzureRmVM -ResourceGroupName $resourceGroup -Name $vmName
```

> [!WARNING]
> Cofanie przydziału maszyny Wirtualnej zwalnia dynamiczne adresy IP przypisane do maszyny Wirtualnej. Nie dotyczy systemu operacyjnego i dysków z danymi. 
> 
> 

## <a name="resize-a-windows-vm-in-an-availability-set"></a>Zmień rozmiar maszyny Wirtualnej z systemem Windows w zestawie dostępności

Jeśli nowy rozmiar maszyny Wirtualnej w zestawie dostępności nie jest dostępny w klastrze sprzętu obecnie obsługującego maszynę Wirtualną, następnie wszystkich maszyn wirtualnych w zestawie dostępności należy cofnąć przydział, aby zmienić rozmiar maszyny Wirtualnej. Możesz również może być konieczne zaktualizowanie rozmiaru innych maszyn wirtualnych w zestawie, po jednej maszyny Wirtualnej został zmieniony dostępności. Aby zmienić rozmiar maszyny Wirtualnej w zestawie dostępności, wykonaj następujące czynności.

```powershell
$resourceGroup = "myResourceGroup"
$vmName = "myVM"
```

Wyświetl listę rozmiarów maszyn wirtualnych, które są dostępne w klastrze sprzętu, w którym jest hostowana maszyna wirtualna. 
   
```powershell
Get-AzureRmVMSize -ResourceGroupName $resourceGroup -VMName $vmName 
```

Jeśli żądany rozmiar jest na liście, uruchom następujące polecenia, aby zmienić rozmiar maszyny Wirtualnej. Jeśli nie ma na liście, przejdź do następnej sekcji.
   
```powershell
$vm = Get-AzureRmVM -ResourceGroupName $resourceGroup -VMName $vmName 
$vm.HardwareProfile.VmSize = "<newVmSize>"
Update-AzureRmVM -VM $vm -ResourceGroupName $resourceGroup
```
    
Jeśli nie ma odpowiedni rozmiar, kontynuuj poniższe kroki, aby cofnąć wszystkie maszyny wirtualne w zestawie dostępności, zmienianie rozmiaru maszyn wirtualnych i uruchom je ponownie.

Zatrzymaj wszystkie maszyny wirtualne w zestawie dostępności.
   
```powershell
$as = Get-AzureRmAvailabilitySet -ResourceGroupName $resourceGroup
$vmIds = $as.VirtualMachinesReferences
foreach ($vmId in $vmIDs){
    $string = $vmID.Id.Split("/")
    $vmName = $string[8]
    Stop-AzureRmVM -ResourceGroupName $resourceGroup -Name $vmName -Force
    } 
```

Zmień rozmiar i ponowne uruchamianie maszyn wirtualnych w zestawie dostępności.
   
```powershell
$newSize = "<newVmSize>"
$as = Get-AzureRmAvailabilitySet -ResourceGroupName $resourceGroup
$vmIds = $as.VirtualMachinesReferences
  foreach ($vmId in $vmIDs){
    $string = $vmID.Id.Split("/")
    $vmName = $string[8]
    $vm = Get-AzureRmVM -ResourceGroupName $resourceGroup -Name $vmName
    $vm.HardwareProfile.VmSize = $newSize
    Update-AzureRmVM -ResourceGroupName $resourceGroup -VM $vm
    Start-AzureRmVM -ResourceGroupName $resourceGroup -Name $vmName
    }
```

## <a name="next-steps"></a>Kolejne kroki

Dla uzyskania dodatkowej skalowalności uruchomić wiele wystąpień maszyny Wirtualnej, a następnie skalować w poziomie. Aby uzyskać więcej informacji, zobacz [automatyczne skalowanie maszyn Windows w zestawie skalowania maszyn wirtualnych](../../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md).

