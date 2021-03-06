---
title: 'Usługa Azure Backup: Magazyny usługi Recovery Services za pomocą interfejsu API REST'
description: Zarządzanie kopiami zapasowymi i przywracanie operacji przy użyciu interfejsu API REST usługi Azure VM Backup
services: backup
author: pvrk
manager: shivamg
keywords: INTERFEJS API REST; Kopia zapasowa maszyny Wirtualnej platformy Azure; Przywracanie maszyny Wirtualnej platformy Azure;
ms.service: backup
ms.topic: conceptual
ms.date: 08/21/2018
ms.author: pullabhk
ms.assetid: e54750b4-4518-4262-8f23-ca2f0c7c0439
ms.openlocfilehash: 7d1a4e6b1093344d1217e8577a56f34cd3c1f52c
ms.sourcegitcommit: 02ce0fc22a71796f08a9aa20c76e2fa40eb2f10a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/08/2018
ms.locfileid: "51289701"
---
# <a name="create-azure-recovery-services-vault-using-rest-api"></a>Tworzenie usługi Azure magazyn usługi Recovery Services za pomocą interfejsu API REST

Kroki umożliwiające utworzenie Azure magazyn usługi Recovery Services za pomocą interfejsu API REST są opisane w [Utwórz magazyn usługi interfejsu API REST](https://docs.microsoft.com/rest/api/recoveryservices/vaults/createorupdate) dokumentacji. Daj nam należy używać tego dokumentu jako odwołanie, aby utworzyć magazyn o nazwie "testVault" w "Zachodnie stany USA".

Aby utworzyć lub zaktualizować magazyn usługi Azure Recovery Services, należy użyć następującego *umieścić* operacji.

```http
PUT https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.RecoveryServices/vaults/{vaultName}?api-version=2016-06-01
```

## <a name="create-a-request"></a>Utwórz żądanie

Aby utworzyć *umieścić* żądania `{subscription-id}` parametr jest wymagany. Jeśli masz wiele subskrypcji, zobacz [Praca z wieloma subskrypcjami](/cli/azure/manage-azure-subscriptions-azure-cli?view=azure-cli-latest#working-with-multiple-subscriptions). Należy zdefiniować `{resourceGroupName}` i `{vaultName}` dla zasobów, wraz z `api-version` parametru. W tym artykule wykorzystano `api-version=2016-06-01`.

Wymagane są następujące nagłówki:

| Nagłówek żądania   | Opis |
|------------------|-----------------|
| *Typ zawartości:*  | Wymagany. Ustaw `application/json`. |
| *Autoryzacja:* | Wymagany. Ustawić prawidłową `Bearer` [token dostępu](https://docs.microsoft.com/rest/api/azure/#authorization-code-grant-interactive-clients). |

Aby uzyskać więcej informacji o tym, jak utworzyć żądanie, zobacz [składniki żądania/odpowiedzi interfejsu API REST](/rest/api/azure/#components-of-a-rest-api-requestresponse).

## <a name="create-the-request-body"></a>Tworzenie treści żądania

Następujące typowe definicje są używane do tworzenia treści żądania:

|Name (Nazwa)  |Wymagane  |Typ  |Opis  |
|---------|---------|---------|---------|
|Element eTag     |         |   Ciąg      |  Opcjonalny element eTag.       |
|location     |  true       |Ciąg         |   Lokalizacja zasobu      |
|properties     |         | [VaultProperties](https://docs.microsoft.com/rest/api/recoveryservices/vaults/createorupdate#vaultproperties)        |  Właściwości magazynu       |
|jednostka SKU     |         |  [Jednostka SKU](https://docs.microsoft.com/rest/api/recoveryservices/vaults/createorupdate#sku)       |    Określa unikatowy identyfikator systemowy dla poszczególnych zasobów platformy Azure     |
|tags     |         | Obiekt        |     Tagi zasobów    |

Należy zauważyć, że magazyn nazwy i nazwy grupy zasobów znajdują się w identyfikatorze URI PUT. Treść żądania określa lokalizację.

## <a name="example-request-body"></a>Przykład treść żądania

Treść poniższy przykład umożliwia utworzenie magazynu w "Zachodnie stany USA". Określ lokalizację. Jednostka SKU jest zawsze "Standardowy".

```json
{
  "properties": {},
  "sku": {
    "name": "Standard"
  },
  "location": "West US"
}
```

## <a name="responses"></a>Odpowiedzi

Istnieją dwa pomyślne odpowiedzi dla operacji, które można utworzyć lub zaktualizować magazynu usługi Recovery Services:

|Name (Nazwa)  |Typ  |Opis  |
|---------|---------|---------|
|200 OK     |   [Magazyn](https://docs.microsoft.com/rest/api/recoveryservices/vaults/createorupdate#vault)      | OK        |
|201 utworzono     | [Magazyn](https://docs.microsoft.com/rest/api/recoveryservices/vaults/createorupdate#vault)        |   Utworzone      |

Aby uzyskać więcej informacji na temat odpowiedzi interfejsu API REST, zobacz [przetworzyć komunikatu odpowiedzi](/rest/api/azure/#process-the-response-message).

### <a name="example-response"></a>Przykładowa odpowiedź

Skrócone *201 utworzono* odpowiedzi z poprzedniego żądania przykład podstawowy pokazuje *identyfikator* przypisano i *provisioningState* jest *zakończone powodzeniem* :

```json
{
  "location": "westus",
  "name": "testVault",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "id": "/subscriptions/77777777-b0c6-47a2-b37c-d8e65a629c18/resourceGroups/Default-RecoveryServices-ResourceGroup/providers/Microsoft.RecoveryServices/vaults/testVault",
  "type": "Microsoft.RecoveryServices/vaults",
  "sku": {
    "name": "Standard"
  }
}
```

## <a name="next-steps"></a>Kolejne kroki

[Tworzenie kopii zapasowej zasady tworzenia kopii zapasowej maszyny Wirtualnej platformy Azure, w tym magazynie](backup-azure-arm-userestapi-createorupdatepolicy.md).

Aby uzyskać więcej informacji na temat interfejsów API REST platformy Azure zobacz następujące dokumenty:

- [Interfejs API REST platformy Azure w zakresie dostawcy usługi Recovery Services](/rest/api/recoveryservices/)
- [Wprowadzenie do interfejsu API REST platformy Azure](/rest/api/azure/)
