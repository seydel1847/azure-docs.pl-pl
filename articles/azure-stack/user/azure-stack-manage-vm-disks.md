---
title: Zarządzaj dyskami maszyny Wirtualnej w usłudze Azure Stack | Dokumentacja firmy Microsoft
description: Aprowizuj dyski dla maszyn wirtualnych w usłudze Azure Stack.
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/03/2018
ms.author: mabrigg
ms.reviewer: jiahan
ms.openlocfilehash: 473fb95de5da4a14c81d0fa3a5aafa33302d9ab2
ms.sourcegitcommit: c61777f4aa47b91fb4df0c07614fdcf8ab6dcf32
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/14/2019
ms.locfileid: "54258683"
---
# <a name="provision-virtual-machine-disk-storage-in-azure-stack"></a>Aprowizuj Magazyn dyskowy maszyny wirtualnej w usłudze Azure Stack

*Dotyczy: Zintegrowane usługi Azure Stack, systemy i usługi Azure Stack Development Kit*

W tym artykule opisano sposób aprowizacji magazynu dyskowego maszyny wirtualnej za pomocą portalu usługi Azure Stack lub przy użyciu programu PowerShell.

## <a name="overview"></a>Przegląd

Począwszy od wersji 1808, usługa Azure Stack obsługuje korzystanie z dysków zarządzanych i niezarządzanych dysków na maszynach wirtualnych, zarówno jako systemu operacyjnego (OS) i dysk z danymi. Przed wersją 1808 obsługiwane są tylko dyski niezarządzane. 

**[Usługa Managed disks](https://docs.microsoft.com/azure/virtual-machines/windows/about-disks-and-vhds#managed-disks)**  upraszcza zarządzanie dyskami maszyn wirtualnych IaaS platformy Azure dzięki zarządzaniu kontami magazynu skojarzone z dyskami maszyn wirtualnych. Wystarczy określić rozmiar dysku należy i usługi Azure Stack, tworzy i zarządza dysku.

**[Niezarządzane dyski](https://docs.microsoft.com/azure/virtual-machines/windows/about-disks-and-vhds#unmanaged-disks)**, wymaga utworzenia [konta magazynu](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account) do przechowywania dysków. Dyski które tworzysz są określane jako dyski maszyny Wirtualnej i są przechowywane w kontenerach na koncie magazynu.

 

### <a name="best-practice-guidelines"></a>Najlepsze rozwiązania przyjęte

Aby zwiększyć wydajność i zmniejszyć ogólne koszty, zalecane jest umieszczenie każdego dysku maszyny Wirtualnej w kontenerze oddzielnym. Kontener mają być przechowywane z dysku systemu operacyjnego lub dysk danych, ale nie obu jednocześnie. (Jednak nie ma nic do uniemożliwić umieszczenie obu rodzajów dysku w tym samym kontenerze.)

Jeśli dodasz co najmniej jeden dysk danych do maszyny Wirtualnej, są używane dodatkowe kontenery jako miejsce do przechowywania tych dysków. Dysk systemu operacyjnego dla dodatkowych maszyn wirtualnych należy również w ich własnych kontenerów.

Podczas tworzenia wielu maszyn wirtualnych, można ponownie użyć tego samego konta magazynu dla każdej nowej maszyny wirtualnej. Kontenery, tworzonych powinny być unikatowe.

### <a name="adding-new-disks"></a>Dodawanie nowych dysków

W poniższej tabeli przedstawiono sposób dodawania dysków, korzystając z portalu i przy użyciu programu PowerShell.

| Metoda | Opcje
|-|-|
|[Portal użytkowników](#use-the-portal-to-add-additional-disks-to-a-vm)|— Dodawanie nowych dysków danych do istniejącej maszyny Wirtualnej. Nowe dyski są tworzone przez usługę Azure Stack. </br> </br>-Dodaj istniejący plik dysku (VHD) do wcześniej aprowizowane maszyny Wirtualnej. Aby to zrobić, należy przygotować VHD i następnie przekazać plik do usługi Azure Stack. |
|[Program PowerShell](#use-powershell-to-add-multiple-unmanaged-disks-to-a-vm) | — Tworzenie nowej maszyny Wirtualnej z dyskiem systemu operacyjnego, a w tym samym czasie należy dodać co najmniej jeden dysk danych do tej maszyny Wirtualnej. |

## <a name="use-the-portal-to-add-disks-to-a-vm"></a>Korzystanie z portalu, aby dodać dyski do maszyny Wirtualnej

Domyślnie podczas tworzenia maszyny Wirtualnej dla większości elementów portalu marketplace, za pomocą portalu tworzone tylko na dysku systemu operacyjnego.

Po utworzeniu maszyny Wirtualnej, można użyć portalu:
* Utwórz nowy dysk danych i dołączyć go do maszyny Wirtualnej.
* Przekaż istniejący dysk danych i dołączyć go do maszyny Wirtualnej.

Każdy dysk niezarządzany, jakie dodasz, należy umieścić w oddzielny kontener.

>[!NOTE]  
>Dyski tworzone i zarządzane przez platformę Azure są nazywane [usługi managed disks](https://docs.microsoft.com/azure/virtual-machines/windows/managed-disks-overview).

### <a name="use-the-portal-to-create-and-attach-a-new-data-disk"></a>Aby utworzyć i dołączyć nowy dysk danych, użyj portalu

1.  W portalu, wybierz **maszyn wirtualnych**.    
    ![Przykład: Pulpit nawigacyjny maszyny Wirtualnej](media/azure-stack-manage-vm-disks/vm-dashboard.png)

2.  Wybierz maszynę wirtualną, który wcześniej został aprowizowany.   
    ![Przykład: Wybierz maszynę Wirtualną na pulpicie nawigacyjnym](media/azure-stack-manage-vm-disks/select-a-vm.png)

3.  Dla maszyny wirtualnej wybierz **dysków** > **Dołącz nowy**.       
    ![Przykład: Dołączyć nowy dysk do maszyny wirtualnej](media/azure-stack-manage-vm-disks/Attach-disks.png)    

4.  W **Dołącz nowy dysk** okienku wybierz **lokalizacji**. Domyślnie lokalizacja jest ustawiana na ten sam kontener, który zawiera dysk systemu operacyjnego.      
    ![Przykład: Ustaw lokalizację dysku](media/azure-stack-manage-vm-disks/disk-location.png)

5.  Wybierz **konta magazynu** do użycia. Następnie wybierz pozycję **kontenera** gdzie chcesz umieścić dysk z danymi. Z **kontenery** strony, można utworzyć nowy kontener Jeśli chcesz. Lokalizacja nowego dysku można później zmienić na własnym kontenerze. Używając oddzielnego kontenera dla każdego dysku, możesz dystrybuować położenie dysku danych, który może zwiększyć wydajność. Wybierz **wybierz** zapisać je.     
    ![Przykład: Wybierz kontener](media/azure-stack-manage-vm-disks/select-container.png)

6.  W **Dołącz nowy dysk** strony, zaktualizuj **nazwa**, **typu**, **rozmiar**, i **hosta, buforowanie** ustawienia dysku. Następnie wybierz pozycję **OK** Aby zapisać nową konfigurację dysku dla maszyny Wirtualnej.  
    ![Przykład: Załącznik całego dysku](media/azure-stack-manage-vm-disks/complete-disk-attach.png)  

7.  Po usługi Azure Stack utworzy dysk i dołącza go do maszyny wirtualnej, nowy dysk ma na liście ustawień dysku maszyny wirtualnej w obszarze **dysków z danymi**.   
    ![Przykład: Wyświetl dysku](media/azure-stack-manage-vm-disks/view-data-disk.png)


### <a name="attach-an-existing-data-disk-to-a-vm"></a>Dołącz istniejący dysk danych do maszyny Wirtualnej

1.  [Przygotuj plik VHD](https://docs.microsoft.com/azure/virtual-machines/windows/classic/createupload-vhd) do użycia jako dysk z danymi dla maszyny Wirtualnej. Przekaż ten plik VHD do konta magazynu, który jest używany z maszyny Wirtualnej, która ma zostać dołączony plik VHD do.

  Zaplanuj użycie innego kontenera do przechowywania pliku VHD niż kontener, który zawiera dysk systemu operacyjnego.   
  ![Przykład: Przekazywanie pliku VHD](media/azure-stack-manage-vm-disks/upload-vhd.png)

2.  Po przekazaniu pliku VHD można przystąpić do Dołącz wirtualny dysk twardy do maszyny Wirtualnej. W menu po lewej stronie wybierz **maszyn wirtualnych**.  
 ![Przykład: Wybierz maszynę Wirtualną na pulpicie nawigacyjnym](media/azure-stack-manage-vm-disks/vm-dashboard.png)

3.  Wybierz maszynę wirtualną z listy.    
  ![Przykład: Wybierz maszynę Wirtualną na pulpicie nawigacyjnym](media/azure-stack-manage-vm-disks/select-a-vm.png)

4.  Na stronie dla maszyny wirtualnej wybierz **dysków** > **Dołącz istniejące**.   
  ![Przykład: Dołączanie istniejącego dysku](media/azure-stack-manage-vm-disks/attach-disks2.png)

5.  W **dołączyć istniejącego dysku** wybierz opcję **pliku wirtualnego dysku twardego**. **Kont magazynu** zostanie otwarta strona.    
  ![Przykład: Wybierz plik wirtualnego dysku twardego](media/azure-stack-manage-vm-disks/select-vhd.png)

6.  W obszarze **kont magazynu**, wybierz konto do użycia, a następnie wybierz kontener, który zawiera plik VHD został wcześniej przekazany. Wybierz plik VHD, a następnie wybierz **wybierz** zapisać je.    
  ![Przykład: Wybierz kontener](media/azure-stack-manage-vm-disks/select-container2.png)

7.  W obszarze **dołączyć istniejącego dysku**, wybrany plik znajduje się w obszarze **pliku wirtualnego dysku twardego**. Aktualizacja **hosta, buforowanie** ustawienia dysku, a następnie wybierz **OK** Aby zapisać nową konfigurację dysku dla maszyny Wirtualnej.    
  ![Przykład: Dołącz plik wirtualnego dysku twardego](media/azure-stack-manage-vm-disks/attach-vhd.png)

8.  Po usługi Azure Stack utworzy dysk i dołącza go do maszyny wirtualnej, nowy dysk ma na liście ustawień dysku maszyny wirtualnej w obszarze **dysków z danymi**.   
  ![Przykład: Dołączanie dysku ukończone](media/azure-stack-manage-vm-disks/complete-disk-attach.png)


## <a name="use-powershell-to-add-multiple-unmanaged-disks-to-a-vm"></a>Aby dodać wiele dysków niezarządzanych do maszyny Wirtualnej przy użyciu programu PowerShell
Można użyć programu PowerShell, aprowizowanie maszyny Wirtualnej i Dodaj nowy dysk danych, lub Dołącz istniejące wstępnie **VHD** pliku jako dysk z danymi.

**Add-azurermvmdatadisk i** polecenie cmdlet dodaje dysk danych do maszyny wirtualnej. Podczas tworzenia maszyny wirtualnej lub dysk danych można dodać istniejącej maszyny wirtualnej, można dodać dysku z danymi. Określ **VhdUri** parametru, aby dystrybuować dysków do różnych kontenerów.

### <a name="add-data-disks-to-a-new-virtual-machine"></a>Dodawanie dysków danych do nowej maszyny wirtualnej
W poniższych przykładach używane polecenia programu PowerShell, aby utworzyć Maszynę wirtualną za pomocą trzech dysków z danymi, każdej umieszczany w innego kontenera.

Pierwsze polecenie tworzy obiekt maszyny wirtualnej, a następnie przechowanie go w *$VirtualMachine* zmiennej. Polecenie przypisuje nazwę i rozmiar maszyny wirtualnej.
  ```powershell
  $VirtualMachine = New-AzureRmVMConfig -VMName "VirtualMachine" `
                                      -VMSize "Standard_A2"
  ```

Następne trzy polecenia przypisują ścieżki trzech dysków z danymi do *$DataDiskVhdUri01*, *$DataDiskVhdUri02*, i *$DataDiskVhdUri03* zmiennych. Zdefiniuj nazwę inną ścieżkę w adresie URL, aby dystrybuować dysków do różnych kontenerów.     
  ```powershell
  $DataDiskVhdUri01 = "https://contoso.blob.local.azurestack.external/test1/data1.vhd"
  ```

  ```powershell
  $DataDiskVhdUri02 = "https://contoso.blob.local.azurestack.external/test2/data2.vhd"
  ```

  ```powershell
  $DataDiskVhdUri03 = "https://contoso.blob.local.azurestack.external/test3/data3.vhd"
  ```

Ostatnie trzy polecenia Dodaj dyski z danymi na maszynę wirtualną przechowywaną w *$VirtualMachine*. Każde polecenie Określa nazwę, lokalizację i dodatkowe właściwości dysku. Identyfikator URI każdego dysku jest przechowywany w *$DataDiskVhdUri01*, *$DataDiskVhdUri02*, i *$DataDiskVhdUri03*.
  ```powershell
  $VirtualMachine = Add-AzureRmVMDataDisk -VM $VirtualMachine -Name 'DataDisk1' `
                  -Caching 'ReadOnly' -DiskSizeInGB 10 -Lun 0 `
                  -VhdUri $DataDiskVhdUri01 -CreateOption Empty
  ```

  ```powershell
  $VirtualMachine = Add-AzureRmVMDataDisk -VM $VirtualMachine -Name 'DataDisk2' `
                 -Caching 'ReadOnly' -DiskSizeInGB 11 -Lun 1 `
                 -VhdUri $DataDiskVhdUri02 -CreateOption Empty
  ```

  ```powershell
  $VirtualMachine = Add-AzureRmVMDataDisk -VM $VirtualMachine -Name 'DataDisk3' `
                  -Caching 'ReadOnly' -DiskSizeInGB 12 -Lun 2 `
                  -VhdUri $DataDiskVhdUri03 -CreateOption Empty
  ```

Użyj następujących poleceń programu PowerShell, aby dodać konfigurację dysku i sieci systemu operacyjnego do maszyny Wirtualnej, a następnie uruchom nową maszynę Wirtualną.
  ```powershell
  #set variables
  $rgName = "myResourceGroup"
  $location = "local"
  #Set OS Disk
  $osDiskUri = "https://contoso.blob.local.azurestack.external/vhds/osDisk.vhd"
  $osDiskName = "osDisk"

  $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $osDiskName -VhdUri $osDiskUri `
      -CreateOption FromImage -Windows

  # Create a subnet configuration
  $subnetName = "mySubNet"
  $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24

  # Create a vnet configuration
  $vnetName = "myVnetName"
  $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
      -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet

  # Create a public IP
  $ipName = "myIP"
  $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
      -AllocationMethod Dynamic

  # Create a network security group configuration
  $nsgName = "myNsg"
  $rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
      -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
      -SourceAddressPrefix Internet -SourcePortRange * `
      -DestinationAddressPrefix * -DestinationPortRange 3389
  $nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
      -Name $nsgName -SecurityRules $rdpRule

  # Create a NIC configuration
  $nicName = "myNicName"
  $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName `
  -Location $location -SubnetId $vnet.Subnets[0].Id -NetworkSecurityGroupId $nsg.Id -PublicIpAddressId $pip.Id

  #Create the new VM
  $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName VirtualMachine | `
      Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer -Offer WindowsServer `
      -Skus 2016-Datacenter -Version latest | Add-AzureRmVMNetworkInterface -Id $nic.Id
  New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $VirtualMachine
  ```



### <a name="add-data-disks-to-an-existing-virtual-machine"></a>Dodawanie dysków danych do istniejącej maszyny wirtualnej
W poniższych przykładach używane polecenia programu PowerShell, aby dodać dla trzech dysków danych do istniejącej maszyny Wirtualnej.
Pierwsze polecenie pobiera maszyny wirtualnej o nazwie VirtualMachine przy użyciu **Get-AzureRmVM** polecenia cmdlet. Polecenie przechowuje maszynę wirtualną w *$VirtualMachine* zmiennej.
  ```powershell
  $VirtualMachine = Get-AzureRmVM -ResourceGroupName "myResourceGroup" `
                                  -Name "VirtualMachine"
  ```
Następne trzy polecenia przypisują ścieżki trzech dysków z danymi do zmiennych $DataDiskVhdUri01 $DataDiskVhdUri02 i $DataDiskVhdUri03.  Nazwy innej ścieżki w vhduri wskazywać różnych kontenerów do umieszczania dysku.
  ```powershell
  $DataDiskVhdUri01 = "https://contoso.blob.local.azurestack.external/test1/data1.vhd"
  ```
  ```powershell
  $DataDiskVhdUri02 = "https://contoso.blob.local.azurestack.external/test2/data2.vhd"
  ```
  ```powershell
  $DataDiskVhdUri03 = "https://contoso.blob.local.azurestack.external/test3/data3.vhd"
  ```


  Następne trzy polecenia Dodaj dyski z danymi na maszynę wirtualną przechowywaną w *$VirtualMachine* zmiennej. Każde polecenie Określa nazwę, lokalizację i dodatkowe właściwości dysku. Identyfikator URI każdego dysku jest przechowywany w *$DataDiskVhdUri01*, *$DataDiskVhdUri02*, i *$DataDiskVhdUri03*.
  ```powershell
  Add-AzureRmVMDataDisk -VM $VirtualMachine -Name "disk1" `
                        -VhdUri $DataDiskVhdUri01 -LUN 0 `
                        -Caching ReadOnly -DiskSizeinGB 10 -CreateOption Empty
  ```
  ```powershell
  Add-AzureRmVMDataDisk -VM $VirtualMachine -Name "disk2" `
                        -VhdUri $DataDiskVhdUri02 -LUN 1 `
                        -Caching ReadOnly -DiskSizeinGB 11 -CreateOption Empty
  ```
  ```powershell
  Add-AzureRmVMDataDisk -VM $VirtualMachine -Name "disk3" `
                        -VhdUri $DataDiskVhdUri03 -LUN 2 `
                        -Caching ReadOnly -DiskSizeinGB 12 -CreateOption Empty
  ```


  Końcowe polecenie aktualizuje stan maszynę wirtualną przechowywaną w *$VirtualMachine* w -*ResourceGroupName*.
  ```powershell
  Update-AzureRmVM -ResourceGroupName "myResourceGroup" -VM $VirtualMachine
  ```
<!-- Pending scripts  

## Distribute the data disks of an existing VM
If you have a VM with more than one disk in the same container, the service operator of the Azure Stack deployment might ask you to redistribute the disks into individual containers.

To do so, use the scripts from the following location in GitHub. These scripts can be used to move the data disks to different containers.
-->

## <a name="next-steps"></a>Następne kroki
Aby dowiedzieć się więcej o maszynach wirtualnych usługi Azure Stack, zobacz [uwagi dotyczące maszyn wirtualnych w usłudze Azure Stack](https://docs.microsoft.com/azure/azure-stack/user/azure-stack-vm-considerations).
