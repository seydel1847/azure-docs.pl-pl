---
title: Konfigurowanie zarządzanych tożsamości dla zasobów platformy Azure na maszynie wirtualnej zestawu skalowania przy użyciu szablonu
description: Instrukcje krok po kroku dotyczące konfigurowania zarządzanych tożsamości dla zasobów platformy Azure na zestaw skalowania maszyn wirtualnych zestawu, przy użyciu szablonu usługi Azure Resource Manager.
services: active-directory
documentationcenter: ''
author: daveba
manager: daveba
editor: ''
ms.service: active-directory
ms.component: msi
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/20/2018
ms.author: daveba
ms.openlocfilehash: 6498079950310e52fcb16172a34b9848e6a98e8b
ms.sourcegitcommit: 9999fe6e2400cf734f79e2edd6f96a8adf118d92
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/22/2019
ms.locfileid: "54429025"
---
# <a name="configure-managed-identities-for-azure-resources-on-a-azure-virtual-machine-scale-using-a-template"></a>Konfigurowanie zarządzanych tożsamości dla zasobów platformy Azure na skalę maszyny wirtualnej platformy Azure przy użyciu szablonu

[!INCLUDE [preview-notice](../../../includes/active-directory-msi-preview-notice.md)]

Zarządzanych tożsamości dla zasobów platformy Azure udostępnia usługi platformy Azure przy użyciu automatycznie zarządzanych tożsamości w usłudze Azure Active Directory. Można użyć tej tożsamości do uwierzytelniania na dowolne usługi obsługujące uwierzytelnianie usługi Azure AD bez poświadczeń w kodzie. 

W tym artykule dowiesz się, jak wykonywać następujące zarządzanych tożsamości dla operacji tworzenia zasobów platformy Azure w zestawie skalowania maszyn wirtualnych platformy Azure przy użyciu szablonu wdrożenia usługi Azure Resource Manager:
- Włączanie i wyłączanie przypisany systemowo tożsamość zarządzaną w zestawie skalowania maszyn wirtualnych platformy Azure
- Dodawanie i usuwanie tożsamości zarządzanej przypisanych przez użytkownika w zestawie skalowania maszyn wirtualnych platformy Azure

## <a name="prerequisites"></a>Wymagania wstępne

- Jeśli jesteś zaznajomiony z zarządzanych tożsamości dla zasobów platformy Azure, zapoznaj się z [sekcji Przegląd](overview.md). **Należy przejrzeć [różnicę między przypisana przez system i przypisanych przez użytkownika tożsamości zarządzanej](overview.md#how-does-it-work)**.
- Jeśli nie masz jeszcze konta platformy Azure, [utwórz bezpłatne konto](https://azure.microsoft.com/free/) przed kontynuowaniem.
- Do wykonywania operacji zarządzania, w tym artykule, Twoje konto musi następujące przypisania kontroli dostępu opartej na rolach platformy Azure:

    > [!NOTE]
    > Nie dodatkowych Azure przypisań ról katalogu usługi AD wymagane.

    - [Współautor maszyny wirtualnej](/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) do tworzenia zestawu skalowania maszyn wirtualnych i włączyć i usuwać systemowych i/lub przypisanych przez użytkownika z tożsamości zarządzanej z zestawu skalowania maszyn wirtualnych.
    - [Współautor tożsamości zarządzanych](/azure/role-based-access-control/built-in-roles#managed-identity-contributor) tożsamości zarządzanej roli do utworzenia przypisanych przez użytkownika.
    - [Operator tożsamości zarządzanych](/azure/role-based-access-control/built-in-roles#managed-identity-operator) roli przypisywania i usuwania, użytkownik przypisany tożsamości zarządzanej, od i do zestawu skalowania maszyn wirtualnych.

## <a name="azure-resource-manager-templates"></a>Szablony usługi Azure Resource Manager

Podobnie jak w witrynie Azure portal i skryptów, [usługi Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) Szablony zapewniają możliwość wdrażania nowych lub zmodyfikowanych zasobów zdefiniowany przez grupę zasobów platformy Azure. Jest dostępnych kilka opcji edycję szablonu i wdrażania, zarówno lokalnych, jak i oparte na portalu, w tym:

   - Za pomocą [niestandardowego szablonu w portalu Azure Marketplace](../../azure-resource-manager/resource-group-template-deploy-portal.md#deploy-resources-from-custom-template), co pozwala na Utwórz szablon od podstaw albo oparte na typowych istniejących lub [szablon szybkiego startu](https://azure.microsoft.com/documentation/templates/).
   - Wyprowadzanie z istniejącej grupy zasobów przez wyeksportowanie szablonu z poziomu [oryginalnego wdrożenia](../../azure-resource-manager/resource-manager-export-template.md#view-template-from-deployment-history), lub z [bieżący stan wdrożenia](../../azure-resource-manager/resource-manager-export-template.md#export-the-template-from-resource-group).
   - Za pomocą lokalnego [edytora JSON (np. programu VS Code)](../../azure-resource-manager/resource-manager-create-first-template.md), a następnie przekazywanie i wdrażanie przy użyciu programu PowerShell lub interfejsu wiersza polecenia.
   - Za pomocą programu Visual Studio [projekt grupy zasobów platformy Azure](../../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) Aby utworzyć i wdrożyć szablon.  

Niezależnie od wybranej opcji składni szablonu jest taka sama podczas początkowego wdrażania i ponownego wdrażania. Włączanie zarządzanych tożsamości dla zasobów platformy Azure w nowej lub istniejącej maszyny Wirtualnej z systemem odbywa się w taki sam sposób. Ponadto domyślnie usługi Azure Resource Manager jest [aktualizacji przyrostowej](../../azure-resource-manager/deployment-modes.md) do wdrożeń.

## <a name="system-assigned-managed-identity"></a>Przypisana przez system tożsamości zarządzanej

W tej sekcji można będzie włączyć i wyłączyć przypisany systemowo tożsamości zarządzanej przy użyciu szablonu usługi Azure Resource Manager.

### <a name="enable-system-assigned-managed-identity-during-creation-the-creation-of-a-virtual-machines-scale-set-or-a-existing-virtual-machine-scale-set"></a>Włącz przypisany systemowo tożsamości zarządzanej podczas tworzenia do tworzenia zestawu skalowania maszyn wirtualnych i istniejącego zestawu skalowania maszyn wirtualnych

1. Czy możesz się zarejestrować na platformę Azure lokalnie lub w witrynie Azure portal, należy użyć konta skojarzonego z subskrypcją platformy Azure, który zawiera zestaw skalowania maszyn wirtualnych.
   
2. Aby włączyć tożsamość zarządzaną przypisana przez system, należy załadować szablon do edytora, odszukaj `Microsoft.Compute/virtualMachinesScaleSets` zasobów zainteresowania w ramach zasobów sekcji i Dodaj `identity` właściwości w tym samym poziomie co `"type": "Microsoft.Compute/virtualMachinesScaleSets"` właściwości. Należy użyć następującej składni:

   ```JSON
   "identity": { 
       "type": "SystemAssigned"
   }
   ```

3. (Opcjonalnie) Dodawanie zarządzanych tożsamości dla rozszerzenia zasobów platformy Azure jako zestawu skalowania maszyn wirtualnych `extensionsProfile` elementu. Ten krok jest opcjonalny, zgodnie z tożsamości usługi Azure wystąpienie metadanych usługi (IMDS), można użyć do pobierania tokenów, jak również.  Należy użyć następującej składni:

   >[!NOTE] 
   > W poniższym przykładzie założono, rozszerzenie zestawu skalowania maszyn wirtualnych z systemem Windows (`ManagedIdentityExtensionForWindows`) jest wdrażany. Można również skonfigurować dla systemu Linux przy użyciu `ManagedIdentityExtensionForLinux` katalog wirtualny wskazywał na `"name"` i `"type"` elementów.
   >

   ```json
   "extensionProfile": {
        "extensions": [
            {
                "name": "ManagedIdentityWindowsExtension",
                "properties": {
                    "publisher": "Microsoft.ManagedIdentity",
                    "type": "ManagedIdentityExtensionForWindows",
                    "typeHandlerVersion": "1.0",
                    "autoUpgradeMinorVersion": true,
                    "settings": {
                        "port": 50342
                    },
                    "protectedSettings": {}
                }
            }
   ```

4. Gdy wszystko będzie gotowe, w poniższych sekcjach należy dodawać do sekcji zasobów szablonu i powinien wyglądać w następujący sposób:

   ```json
    "resources": [
        {
            //other resource provider properties...
            "apiVersion": "2018-06-01",
            "type": "Microsoft.Compute/virtualMachineScaleSets",
            "name": "[variables('vmssName')]",
            "location": "[resourceGroup().location]",
            "identity": {
                "type": "SystemAssigned",
            },
           "properties": {
                //other resource provider properties...
                "virtualMachineProfile": {
                    //other virtual machine profile properties...
                    "extensionProfile": {
                        "extensions": [
                            {
                                "name": "ManagedIdentityWindowsExtension",
                                "properties": {
                                  "publisher": "Microsoft.ManagedIdentity",
                                  "type": "ManagedIdentityExtensionForWindows",
                                  "typeHandlerVersion": "1.0",
                                  "autoUpgradeMinorVersion": true,
                                  "settings": {
                                      "port": 50342
                                  }
                                }
                            } 
                        ]
                    }
                }
            }
        }
    ]
   ``` 

### <a name="disable-a-system-assigned-managed-identity-from-an-azure-virtual-machine-scale-set"></a>Wyłącz przypisany systemowo tożsamości zarządzanej z zestawu skalowania maszyn wirtualnych platformy Azure

Jeśli masz zestaw skalowania maszyn wirtualnych, który nie wymaga tożsamości zarządzanej przypisana przez system:

1. Czy możesz się zarejestrować na platformę Azure lokalnie lub w witrynie Azure portal, należy użyć konta skojarzonego z subskrypcją platformy Azure, który zawiera zestaw skalowania maszyn wirtualnych.

2. Ładowanie szablonu do [edytora](#azure-resource-manager-templates) i Znajdź `Microsoft.Compute/virtualMachineScaleSets` zasobów zainteresowania w ramach `resources` sekcji. Jeśli masz maszynę Wirtualną, która ma tylko przypisana przez system tożsamości zarządzanej, można ją wyłączyć, zmieniając typ tożsamości do `None`.

   **Microsoft.Compute/virtualMachineScaleSets interfejsu API w wersji 2018-06-01**

   Jeśli Twoja wersja interfejsu API jest `2018-06-01` i maszyna wirtualna ma systemowych i tożsamości przypisanych przez użytkownika zarządzanego, Usuń `SystemAssigned` z typu tożsamości i zachować `UserAssigned` wraz z wartościami słownika userAssignedIdentities.

   **Microsoft.Compute/virtualMachineScaleSets interfejsu API w wersji 2018-06-01**

   Jeśli Twoja wersja interfejsu API jest `2017-12-01` i zestawu skalowania maszyn wirtualnych ma systemowych i tożsamości przypisanych przez użytkownika zarządzanego, Usuń `SystemAssigned` z typu tożsamości i zachować `UserAssigned` wraz z `identityIds` tablicę użytkownik przypisany zarządzane tożsamości. 
   
    

   Poniższy przykład pokazuje, jak usunąć przypisany systemowo tożsamość zarządzaną z maszyny wirtualnej zestawu skalowania z tożsamości zarządzanej nie przypisanych przez użytkownika:
   
   ```json
   {
       "name": "[variables('vmssName')]",
       "apiVersion": "2018-06-01",
       "location": "[parameters(Location')]",
       "identity": {
           "type": "None"
        }

   }
   ```

## <a name="user-assigned-managed-identity"></a>Przypisane przez użytkownika z tożsamości zarządzanej

W tej sekcji należy przypisać przypisanych przez użytkownika tożsamości zarządzanej maszyny wirtualnej zestawu skalowania przy użyciu szablonu usługi Azure Resource Manager.

> [!Note]
> Aby utworzyć przypisanych przez użytkownika tożsamości zarządzanej przy użyciu szablonu usługi Azure Resource Manager, zobacz [tworzenie zarządzanych tożsamości przypisanych przez użytkownika](how-to-manage-ua-identity-arm.md#create-a-user-assigned-managed-identity).

### <a name="assign-a-user-assigned-managed-identity-to-a-virutal-machine-scale-set"></a>Przypisz tożsamości zarządzanej użytkownik przypisany do zestawu skalowania maszyny wirtualnej

1. W obszarze `resources` elementu, Dodaj następujący wpis do przypisywania tożsamości zarządzanej użytkownik przypisany do zestawu skalowania maszyn wirtualnych.  Koniecznie Zastąp `<USERASSIGNEDIDENTITY>` o nazwie użytkownik przypisany zarządzanych tożsamości został utworzony.
   
   **Microsoft.Compute/virtualMachineScaleSets interfejsu API w wersji 2018-06-01**

   Jeśli Twoja wersja interfejsu API jest `2018-06-01`, zarządzanych tożsamości przypisanych przez użytkownika są przechowywane w `userAssignedIdentities` format słownika i `<USERASSIGNEDIDENTITYNAME>` wartość musi być przechowywany w zmiennej zdefiniowanej w `variables` części szablonu.

   ```json
   {
       "name": "[variables('vmssName')]",
       "apiVersion": "2018-06-01",
       "location": "[parameters(Location')]",
       "identity": {
           "type": "userAssigned",
           "userAssignedIdentities": {
               "[resourceID('Microsoft.ManagedIdentity/userAssignedIdentities/',variables('<USERASSIGNEDIDENTITYNAME>'))]": {}
           }
       }
    
   }
   ```   

   **Microsoft.Compute/virtualMachineScaleSets interfejsu API w wersji 2017-12-01**
    
   Jeśli Twoje `apiVersion` jest `2017-12-01` lub starszej, zarządzanych tożsamości przypisanych przez użytkownika są przechowywane w `identityIds` tablicy i `<USERASSIGNEDIDENTITYNAME>` wartość musi być przechowywany w zmiennej zdefiniowanej w sekcji zmiennych szablonu.

   ```json
   {
       "name": "[variables('vmssName')]",
       "apiVersion": "2017-03-30",
       "location": "[parameters(Location')]",
       "identity": {
           "type": "userAssigned",
           "identityIds": [
               "[resourceID('Micrososft.ManagedIdentity/userAssignedIdentities/',variables('<USERASSIGNEDIDENTITY>'))]"
           ]
       }

   }
   ``` 

2. (Opcjonalnie) Dodaj następujący wpis w obszarze `extensionProfile` element, aby przypisać zarządzanych tożsamości dla rozszerzenia zasobów platformy Azure do Twojego zestawu skalowania maszyn wirtualnych. Ten krok jest opcjonalny, zgodnie z punktu końcowego tożsamości Azure wystąpienie metadanych usługi (IMDS), można użyć do pobierania tokenów, jak również. Należy użyć następującej składni:
   
    ```JSON
       "extensionProfile": {
            "extensions": [
                {
                    "name": "ManagedIdentityWindowsExtension",
                    "properties": {
                        "publisher": "Microsoft.ManagedIdentity",
                        "type": "ManagedIdentityExtensionForWindows",
                        "typeHandlerVersion": "1.0",
                        "autoUpgradeMinorVersion": true,
                        "settings": {
                            "port": 50342
                        },
                        "protectedSettings": {}
                    }
                }
    ```

3. Gdy wszystko będzie gotowe, szablon powinien wyglądać podobnie do poniższej:
   
   **Microsoft.Compute/virtualMachineScaleSets interfejsu API w wersji 2018-06-01**   

   ```json
   "resources": [
        {
            //other resource provider properties...
            "apiVersion": "2018-06-01",
            "type": "Microsoft.Compute/virtualMachineScaleSets",
            "name": "[variables('vmssName')]",
            "location": "[resourceGroup().location]",
            "identity": {
                "type": "UserAssigned",
                "userAssignedIdentities": {
                    "[resourceID('Microsoft.ManagedIdentity/userAssignedIdentities/',variables('<USERASSIGNEDIDENTITYNAME>'))]": {}
                }
            },
           "properties": {
                //other virtual machine properties...
                "virtualMachineProfile": {
                    //other virtual machine profile properties...
                    "extensionProfile": {
                        "extensions": [
                            {
                                "name": "ManagedIdentityWindowsExtension",
                                "properties": {
                                  "publisher": "Microsoft.ManagedIdentity",
                                  "type": "ManagedIdentityExtensionForWindows",
                                  "typeHandlerVersion": "1.0",
                                  "autoUpgradeMinorVersion": true,
                                  "settings": {
                                      "port": 50342
                                  }
                                }
                            } 
                        ]
                    }
                }
            }
        }
    ]
   ```

   **Microsoft.Compute/virtualMachines interfejsu API w wersji 2017-12-01**

   ```json
   "resources": [
        {
            //other resource provider properties...
            "apiVersion": "2017-12-01",
            "type": "Microsoft.Compute/virtualMachineScaleSets",
            "name": "[variables('vmssName')]",
            "location": "[resourceGroup().location]",
            "identity": {
                "type": "UserAssigned",
                "identityIds": [
                    "[resourceID('Microsoft.ManagedIdentity/userAssignedIdentities/',variables('<USERASSIGNEDIDENTITYNAME>'))]"
                ]
            },
           "properties": {
                //other virtual machine properties...
                "virtualMachineProfile": {
                    //other virtual machine profile properties...
                    "extensionProfile": {
                        "extensions": [
                            {
                                "name": "ManagedIdentityWindowsExtension",
                                "properties": {
                                  "publisher": "Microsoft.ManagedIdentity",
                                  "type": "ManagedIdentityExtensionForWindows",
                                  "typeHandlerVersion": "1.0",
                                  "autoUpgradeMinorVersion": true,
                                  "settings": {
                                      "port": 50342
                                  }
                                }
                            } 
                        ]
                    }
                }
            }
        }
    ]
   ```
### <a name="remove-user-assigned-managed-identity-from-an-azure-virtual-machine-scale-set"></a>Usuń tożsamość zarządzaną przypisanych przez użytkownika z zestawu skalowania maszyn wirtualnych platformy Azure

Jeśli masz zestaw skalowania maszyn wirtualnych, który nie wymaga tożsamości zarządzanej przypisanych przez użytkownika:

1. Czy możesz się zarejestrować na platformę Azure lokalnie lub w witrynie Azure portal, należy użyć konta skojarzonego z subskrypcją platformy Azure, który zawiera zestaw skalowania maszyn wirtualnych.

2. Ładowanie szablonu do [edytora](#azure-resource-manager-templates) i Znajdź `Microsoft.Compute/virtualMachineScaleSets` zasobów zainteresowania w ramach `resources` sekcji. Jeśli masz zestaw skalowania maszyn wirtualnych, który zawiera tylko przypisanych przez użytkownika z tożsamości zarządzanej, można ją wyłączyć, zmieniając typ tożsamości do `None`.

   Poniższy przykład pokazuje, jak usunąć wszystkich przypisanych do użytkowników zarządzanych tożsamości z maszyny Wirtualnej za pomocą tożsamości zarządzanych nie przypisanych systemu:

   ```json
   {
       "name": "[variables('vmssName')]",
       "apiVersion": "2018-06-01",
       "location": "[parameters(Location')]",
       "identity": {
           "type": "None"
        }
   }
   ```
   
   **Microsoft.Compute/virtualMachineScaleSets interfejsu API w wersji 2018-06-01**
    
   Aby usunąć pojedynczy tożsamość zarządzaną przypisanych przez użytkownika z zestawu skalowania maszyn wirtualnych, usuń go z `userAssignedIdentities` słownika.

   Jeśli masz tożsamości przypisanych przez system, przechowuj je w w `type` wartości w obszarze `identity` wartość.

   **Microsoft.Compute/virtualMachineScaleSets interfejsu API w wersji 2017-12-01**

   Aby usunąć pojedynczy tożsamość zarządzaną przypisanych przez użytkownika z zestawu skalowania maszyn wirtualnych, usuń go z `identityIds` tablicy.

   Jeśli masz przypisaną przez system tożsamości zarządzanej, przechowuj je w w `type` wartości w obszarze `identity` wartość.
   
## <a name="next-steps"></a>Kolejne kroki

- [Zarządzane tożsamości dla zasobów platformy Azure — omówienie](overview.md).

