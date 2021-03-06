---
title: Link konta platformy Azure, z Identyfikatorem partnera | Dokumentacja firmy Microsoft
description: Śledź interakcje z klientami platformy Azure, tworząc konto użytkownika, którego używasz do zarządzania zasobami przez klienta identyfikator partnera.
services: billing
author: dhirajgandhi
manager: dhgandhi
ms.author: cwatson
ms.date: 03/12/2018
ms.service: billing
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.openlocfilehash: eeb88627cbcc1736586defd403b19c19c9cdf56c
ms.sourcegitcommit: 7cd706612a2712e4dd11e8ca8d172e81d561e1db
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/18/2018
ms.locfileid: "53579247"
---
# <a name="link-a-partner-id-to-your-azure-accounts"></a>Połącz z Identyfikatorem partnera do kont systemu Azure

Jako partner możesz śledzić swoje oddziaływanie w powiadomieniach promujących zaangażowanie klientów. Możesz połączyć Twój identyfikator partnera kont, które są używane do zarządzania zasobami klienta.

Ta funkcja jest dostępna w publicznej wersji zapoznawczej.

## <a name="get-access-from-your-customer"></a>Uzyskiwanie dostępu do klienta

Aby połączyć się z Partnerem, klient musi udzielić Ci dostępu do swoich zasobów platformy Azure przy użyciu jednej z następujących opcji:

- **Użytkownik-Gość**: Klienta można dodał Cię jako użytkownika-gościa i przypisywania ról (RBAC) kontroli dostępu opartej na rolach. Aby uzyskać więcej informacji, zobacz [dodać użytkowników-gości z innego katalogu](https://docs.microsoft.com/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b).

- **Konto Directory**: Klienta można utworzyć konto użytkownika dla Ciebie w ich własnych katalogu i przyznawać żadnej roli RBAC.

- **Nazwa główna usługi**: Klienta można dodać aplikację lub skrypt z Twojej organizacji w jego katalogu i przyznawać żadnej roli RBAC. Tożsamość aplikacji lub skryptu jest określany jako nazwy głównej usługi.

## <a name="link-to-a-partner-id"></a>Łączenie z identyfikatorem partnera

Jeśli masz dostęp do zasobów przez klienta, użyć witryny Azure portal, programu PowerShell lub interfejsu wiersza polecenia platformy Azure, aby połączyć identyfikator sieci Microsoft Partner (identyfikator MPN) do Identyfikatora użytkownika lub nazwy głównej usługi. Połącz z Identyfikatorem partnera w każdej dzierżawy klienta.

### <a name="use-the-azure-portal-to-link-to-a-new-partner-id"></a>Użyj witryny Azure portal, aby połączyć nowy identyfikator partnera

1. Przejdź do [Połącz z Identyfikatorem partnera](https://portal.azure.com/#blade/Microsoft_Azure_Billing/managementpartnerblade) w witrynie Azure portal.

2. Zaloguj się do Portalu Azure.

3. Wprowadź identyfikator partnera firmy Microsoft Partner ten identyfikator jest [sieci Microsoft Partner Network](https://partner.microsoft.com/) identyfikator dla Twojej organizacji.

   ![Zrzut ekranu przedstawiający Link do Identyfikatora partnera](./media/billing-link-partner-id/link-partner-ID.PNG)

4. Aby połączyć Identyfikatora partnera do innego klienta, należy przełączyć katalog. W obszarze **Przełącz katalog**, wybierz swój katalog.

   ![Zrzut ekranu pokazujący Przełącz katalog](./media/billing-link-partner-id/directory-switcher.png)

### <a name="use-powershell-to-link-to-a-new-partner-id"></a>Aby połączyć nowy identyfikator partnera przy użyciu programu PowerShell

1. Zainstaluj [AzureRM.ManagementPartner](https://www.powershellgallery.com/packages/AzureRM.ManagementPartner) modułu programu PowerShell.

2. Zaloguj się do dzierżawy klienta przy użyciu konta użytkownika lub nazwy głównej usługi. Aby uzyskać więcej informacji, zobacz [Zaloguj się przy użyciu programu PowerShell](https://docs.microsoft.com/powershell/azure/authenticate-azureps?view=azurermps-5.2.0).
 
   ```azurepowershell-interactive
    C:\> Connect-AzureRmAccount -TenantId XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX 
   ```


3. Link do nowego identyfikatora partnera. Partner ten identyfikator jest [sieci Microsoft Partner Network](https://partner.microsoft.com/) identyfikator dla Twojej organizacji.

    ```azurepowershell-interactive
    C:\> new-AzureRmManagementPartner -PartnerId 12345 
    ```

#### <a name="get-the-linked-partner-id"></a>Pobierz identyfikator połączonej, partnera
```azurepowershell-interactive
C:\> get-AzureRmManagementPartner 
```

#### <a name="update-the-linked-partner-id"></a>Aktualizacja Identyfikatora połączonej, partnera
```azurepowershell-interactive
C:\> Update-AzureRmManagementPartner -PartnerId 12345 
```
#### <a name="delete-the-linked-partner-id"></a>Usuń identyfikator połączonej, partnera
```azurepowershell-interactive
C:\> remove-AzureRmManagementPartner -PartnerId 12345 
```

### <a name="use-the-azure-cli-to-link-to-a-new-partner-id"></a>Użyj wiersza polecenia platformy Azure, aby połączyć nowy identyfikator partnera
1. Zainstaluj rozszerzenie interfejsu wiersza polecenia platformy Azure.

    ```azurecli-interactive
    C:\ az extension add --name managementpartner
    ``` 

2. Zaloguj się do dzierżawy klienta przy użyciu konta użytkownika lub nazwy głównej usługi. Aby uzyskać więcej informacji, zobacz [Zaloguj się przy użyciu wiersza polecenia platformy Azure](https://docs.microsoft.com/cli/azure/authenticate-azure-cli?view=azure-cli-latest).

    ```azurecli-interactive
    C:\ az login --tenant <tenant>
    ``` 

3. Link do nowego identyfikatora partnera. Partner ten identyfikator jest [sieci Microsoft Partner Network](https://partner.microsoft.com/) identyfikator dla Twojej organizacji.

     ```azurecli-interactive
     C:\ az managementpartner create --partner-id 12345
      ```  

#### <a name="get-the-linked-partner-id"></a>Pobierz identyfikator połączonej, partnera
```azurecli-interactive
C:\ az managementpartner show
``` 

#### <a name="update-the-linked-partner-id"></a>Aktualizacja Identyfikatora połączonej, partnera
```azurecli-interactive
C:\ az managementpartner update --partner-id 12345
``` 

#### <a name="delete-the-linked-partner-id"></a>Usuń identyfikator połączonej, partnera
```azurecli-interactive
C:\ az managementpartner delete --partner-id 12345
``` 

## <a name="next-steps"></a>Kolejne kroki

Dołącz do dyskusji w [społeczności partnerów firmy Microsoft](https://aka.ms/PALdiscussion) odbierać aktualizacje lub wysłać opinię.

## <a name="frequently-asked-questions"></a>Często zadawane pytania

**Kto może połączyć Identyfikatora partnera?**

Każdy użytkownik z organizacji partnerskiej, użytkowników, którzy zarządzają zasobami platformy Azure klienta można połączyć Identyfikatora partnera na koncie.

**Identyfikator partnera można zmienić po prowadzi?**

Tak. Identyfikator partnera połączonego można można zmienić, dodać ani usunąć.

**Co zrobić, jeśli użytkownik ma konto w więcej niż jedną dzierżawę klienta?**

Łącze między identyfikator partnera, a kontem odbywa się dla każdej dzierżawy klienta. Połącz z Identyfikatorem partnera w każdej dzierżawy klienta.

**Innych partnerów lub klientów edytować lub usunąć łącze, aby identyfikator partnera?**

Łącze jest skojarzone na poziomie konta użytkownika. Tylko Edytuj lub Usuń łącze do identyfikatora partnera. Klienta i innymi partnerami, nie można zmienić link do identyfikatora partnera. 
