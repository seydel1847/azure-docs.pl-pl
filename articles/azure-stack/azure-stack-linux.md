---
title: Dodawanie obrazów systemu Linux w usłudze Azure Stack
description: Dowiedz się, jak dodać obrazy systemu Linux w usłudze Azure Stack.
services: azure-stack
documentationcenter: ''
author: sethmanheim
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/16/2018
ms.author: sethm
ms.reviewer: unknown
ms.openlocfilehash: 98a1235532ec4cc225ac6a5117265e145b21034b
ms.sourcegitcommit: f4b78e2c9962d3139a910a4d222d02cda1474440
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/12/2019
ms.locfileid: "54245176"
---
# <a name="add-linux-images-to-azure-stack"></a>Dodawanie obrazów systemu Linux w usłudze Azure Stack

*Dotyczy: Zintegrowane usługi Azure Stack, systemy i usługi Azure Stack Development Kit*

Przez dodanie obrazów systemu Linux w witrynie Azure Marketplace stosu, można wdrożyć maszyny wirtualne systemu Linux (VM) w usłudze Azure Stack. Najprostszym sposobem dodania obrazu systemu Linux w usłudze Azure Stack jest za pośrednictwem witryny Marketplace zarządzania. Te obrazy zostały przetworzone i przetestowane pod kątem zgodności z usługą Azure Stack.

## <a name="marketplace-management"></a>Zarządzanie w portalu Marketplace

Aby pobrać obrazy systemu Linux w portalu Azure Marketplace, użyj procedur w programie [pobieranie elementów portalu marketplace z platformy Azure do usługi Azure Stack](azure-stack-download-azure-marketplace-item.md) artykułu. Wybierz obrazy systemu Linux, którzy chcą oferować użytkowników usługi Azure Stack. 

Należy pamiętać, że częste aktualizacje do tych obrazów, dlatego należy sprawdzić zarządzania portalu Marketplace, często w celu zapewnienia aktualności.

## <a name="prepare-your-own-image"></a>Przygotuj swój własny obraz

Wszędzie tam, gdzie to możliwe, należy pobrać obrazów dostępnych za pośrednictwem witryny Marketplace zarządzania, która została przygotowana i sprawdzane pod kątem usługi Azure Stack. 
 
Agent systemu Linux platformy Azure (zazwyczaj nazywany `WALinuxAgent` lub `walinuxagent`) jest wymagana, i nie wszystkie wersje agenta będzie działać w usłudze Azure Stack. Należy używać wersji 2.2.18 lub nowszej, jeśli tworzysz własny obraz. Należy pamiętać, że [pakietu cloud-init](https://cloud-init.io/) nie jest obsługiwana w usłudze Azure Stack w tej chwili.

Można przygotować własnego obrazu systemu Linux przy użyciu następujących instrukcji:

* [Dystrybucje systemu centOS](../virtual-machines/linux/create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Debian systemu Linux](../virtual-machines/linux/debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Red Hat Enterprise Linux](azure-stack-redhat-create-upload-vhd.md)
* [SLES & openSUSE](../virtual-machines/linux/suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Serwer Ubuntu](../virtual-machines/linux/create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

    
## <a name="add-your-image-to-the-marketplace"></a>Dodawanie obrazu do portalu marketplace
 
Postępuj zgodnie z [dodać obraz do portalu Marketplace](azure-stack-add-vm-image.md). Upewnij się, że `OSType` parametr ma wartość `Linux`.

Po dodaniu obrazu portalu Marketplace, tworzony jest element portalu Marketplace, a użytkownicy mogą wdrażać maszyny wirtualnej systemu Linux.

## <a name="next-steps"></a>Kolejne kroki

Zobacz następujące artykuły, aby uzyskać więcej informacji:

- [Pobieranie elementów portalu marketplace z platformy Azure do usługi Azure Stack](azure-stack-download-azure-marketplace-item.md)
- [Omówienie usługi Azure Stack w portalu Marketplace](azure-stack-marketplace.md)