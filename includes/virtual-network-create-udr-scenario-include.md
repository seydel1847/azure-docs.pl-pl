---
title: Plik dyrektywy include
description: Plik dyrektywy include
services: virtual-network
author: genlin
ms.service: virtual-network
ms.topic: include
ms.date: 04/13/2018
ms.author: genli
ms.custom: include file
ms.openlocfilehash: b91ae155761f6357e286f4742d57b97cf96d909a
ms.sourcegitcommit: fa493b66552af11260db48d89e3ddfcdcb5e3152
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/23/2018
ms.locfileid: "31805166"
---
## <a name="scenario"></a>Scenariusz
Aby lepiej zilustrować tworzenie Udr, w niniejszym dokumencie użyto następujący scenariusz:

![OPIS ILUSTRACJI](./media/virtual-network-create-udr-scenario-include/figure1.png)

W tym scenariuszu utworzysz przez jeden dla *podsieci frontonu* i przez inny dla *podsieci wewnętrznej*w następujący sposób: 

* **Frontonu przez**. Frontonu przez jest stosowany do *frontonu* podsieci i może zawierać jedną trasę:    
  * **RouteToBackend**. Ta trasa wysyła cały ruch do podsieci zaplecza, aby **FW1** maszyny wirtualnej.
* **Wewnętrznej bazy danych przez**. PRZEZ zaplecza jest stosowany do *zaplecza* podsieci i może zawierać jedną trasę:    
  * **RouteToFrontend**. Ta trasa wysyła cały ruch do podsieci frontonu, aby **FW1** maszyny wirtualnej.

Kombinacja te trasy gwarantuje, że cały ruch kierowany z jednej podsieci do drugiej jest kierowany do **FW1** maszyny wirtualnej, która jest używana jako urządzenie wirtualne. Należy również włączyć funkcję przesyłania dalej dla adresu IP **FW1** maszynę Wirtualną, aby upewnić się, może odbierać ruch kierowany do innych maszyn wirtualnych.

