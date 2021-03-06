---
title: Używanie ról niestandardowych dla zasobów platformy Azure w usłudze PIM | Dokumentacja firmy Microsoft
description: Dowiedz się, jak używać ról niestandardowych dla zasobów platformy Azure w usłudze Azure AD Privileged Identity Management (PIM).
services: active-directory
documentationcenter: ''
author: rolyon
manager: mtillman
ms.service: active-directory
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.component: pim
ms.date: 03/30/2018
ms.author: rolyon
ms.openlocfilehash: b01e785ac85c71b2982561e8b5e118775750fc69
ms.sourcegitcommit: 63613e4c7edf1b1875a2974a29ab2a8ce5d90e3b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2018
ms.locfileid: "43189877"
---
# <a name="use-custom-roles-for-azure-resources-in-pim"></a>Używanie ról niestandardowych dla zasobów platformy Azure w usłudze PIM

Może być konieczne rygorystyczne Privileged Identity Management (PIM) dotyczą niektórych członków roli, zapewniając większą niezależność dla innych użytkowników. Rozważmy scenariusz, w którym organizacja zatrudnia kilka kojarzy umowy, aby pomóc w rozwoju aplikacji, która jest uruchamiana w subskrypcji platformy Azure.

Jako administrator zasobu ma pracownikom uprawnionych do dostępu bez konieczności zatwierdzania. Jednak wszystkie kojarzy kontraktu musi być zatwierdzony, gdy będą one żądać dostępu do zasobów organizacji.

Wykonaj kroki opisane w następnej sekcji, aby skonfigurować docelowych ustawień usługi PIM dla ról zasobów platformy Azure.

## <a name="create-the-custom-role"></a>Tworzenie roli niestandardowej

Aby utworzyć niestandardową rolę zasobu, wykonaj czynności opisane w [tworzenie ról niestandardowych dla kontroli dostępu](../role-based-access-control-custom-roles.md).

Podczas tworzenia roli niestandardowej obejmują nazwę opisową, dzięki czemu można łatwo zapamiętać wbudowaną rolę, która ma zduplikowane.

> [!NOTE]
> Upewnij się, że rola niestandardowa jest duplikatem rolę wbudowaną, którą chcesz zduplikować, i że jego zakres odpowiada wbudowana rola.

## <a name="apply-pim-settings"></a>Stosowanie ustawień usługi PIM

Po utworzeniu roli w swojej dzierżawie, w witrynie Azure portal przejdź do **Privileged Identity Management — zasoby platformy Azure** okienka. Wybierz zasób, który dotyczy roli.

!["Privileged Identity Management — zasoby platformy Azure" okienko](media/azure-pim-resource-rbac/aadpim_manage_azure_resource_some_there.png)

[Konfigurowanie ustawień roli usługi PIM](pim-resource-roles-configure-role-settings.md) , stosuje się do tych członków roli.

Na koniec [Przypisz role](pim-resource-roles-assign-roles.md) różne grupy elementów członkowskich, które ma pod kątem przy użyciu tych ustawień.

## <a name="next-steps"></a>Kolejne kroki

- [Konfigurowanie ustawień roli zasobów platformy Azure w usłudze PIM](pim-resource-roles-configure-role-settings.md)
- [Role niestandardowe na platformie Azure](../../role-based-access-control/custom-roles.md)
