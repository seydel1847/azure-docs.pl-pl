---
title: Programowe tworzenie subskrypcji Azure Enterprise | Dokumentacja firmy Microsoft
description: Dowiedz się, jak programowo utworzyć dodatkowych subskrypcji Azure Enterprise lub Enterprise projektowania/testowania.
services: azure-resource-manager
author: adpick
manager: adpick
editor: ''
ms.assetid: ''
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/05/2018
ms.author: adpick
ms.openlocfilehash: 90823eded03f298dd912735fb0170fd8002328f3
ms.sourcegitcommit: c29d7ef9065f960c3079660b139dd6a8348576ce
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/12/2018
ms.locfileid: "44715894"
---
# <a name="programmatically-create-azure-enterprise-subscriptions-preview"></a>Programowe tworzenie subskrypcji Azure Enterprise (wersja zapoznawcza)

Jako klient korzystający z platformy Azure na [Enterprise Agreement (EA)](https://azure.microsoft.com/pricing/enterprise-agreement/), można utworzyć subskrypcji umowy EA i testowania (MS-AZR - 0148 P) i EA (MS-AZR - 0017 P) programowo. W tym artykule dowiesz się, jak utworzyć subskrypcje programistycznie przy użyciu usługi Azure Resource Manager.

Po utworzeniu subskrypcji platformy Azure z tego interfejsu API, że subskrypcja podlega warunkom umowy, na podstawie której zakupiono usługi Microsoft Azure od firmy Microsoft lub autoryzowanym sprzedawcą. Aby dowiedzieć się więcej, zobacz [Microsoft Azure — informacje prawne](https://azure.microsoft.com/support/legal/).

## <a name="prerequisites"></a>Wymagania wstępne

Konieczne jest posiadanie roli współautora lub właściciela chcesz tworzyć subskrypcje w ramach konta rejestracji. Istnieją dwa sposoby uzyskania tych ról:

* Administrator rejestracji może [upewnij się, że właściciel konta](https://ea.azure.com/helpdocs/addNewAccount) (logowania wymagane) co sprawia, że możesz właściciel konta rejestracji. Postępuj zgodnie z instrukcjami w wiadomości e-mail z zaproszeniem otrzymywanych ręcznie utworzyć początkową subskrypcję. Potwierdzenie własności konta, a następnie utwórz ręcznie subskrypcji EA początkowej przed przejściem do następnego kroku. Wystarczy dodać konto do rejestracji jest niewystarczające.

* Właściciel istniejącego konta rejestracji można [przyznać dostęp](grant-access-to-create-subscription.md). Podobnie, jeśli chcesz użyć nazwy głównej usługi można utworzyć subskrypcji umowy EA, musisz najpierw [udzielić tego obiektu głównego usługi możliwość tworzenia subskrypcji](grant-access-to-create-subscription.md).

## <a name="find-accounts-you-have-access-to"></a>Wyszukiwania kont, do których masz dostęp do

Po dodaniu rejestracji umowy EA platformy Azure jako właściciel konta, platforma Azure używa relacji rejestracji konta, aby określić, gdzie są naliczane opłaty za subskrypcję. Wszystkie subskrypcje utworzone w ramach konta są rozliczane w kierunku rejestracji umowy EA, który znajduje się konto. Tworzenie subskrypcji, należy przekazać wartości dotyczące konta rejestracji i podmiotami zabezpieczeń użytkownika, być właścicielem subskrypcji. 

Aby uruchomić następujące polecenia, użytkownik musi być zalogowany do właściciela konta *katalogu macierzystego*, który jest katalogiem, który subskrypcje są tworzone w domyślnym.

# <a name="resttabrest"></a>[REST](#tab/rest)

Żądanie wyświetlenia listy wszystkich kont rejestracji:

```json
GET https://management.azure.com/providers/Microsoft.Billing/enrollmentAccounts?api-version=2018-03-01-preview
```

Usługa Azure współpracuje z listą wszystkich kont rejestracji, do których masz dostęp do:

```json
{
  "value": [
    {
      "id": "/providers/Microsoft.Billing/enrollmentAccounts/747ddfe5-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "name": "747ddfe5-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "type": "Microsoft.Billing/enrollmentAccounts",
      "properties": {
        "principalName": "SignUpEngineering@contoso.com"
      }
    },
    {
      "id": "/providers/Microsoft.Billing/enrollmentAccounts/4cd2fcf6-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "name": "4cd2fcf6-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "type": "Microsoft.Billing/enrollmentAccounts",
      "properties": {
        "principalName": "BillingPlatformTeam@contoso.com"
      }
    }
  ]
}
```

# <a name="powershelltabazure-powershell"></a>[Program PowerShell](#tab/azure-powershell)

Użyj [polecenia Get-AzureRmEnrollmentAccount](/powershell/module/azurerm.billing/get-azurermenrollmentaccount) Aby wyświetlić listę wszystkich kont rejestracji masz dostęp do.

```azurepowershell-interactive
Get-AzureRmEnrollmentAccount
```

Azure odpowiada za pomocą listy identyfikatorów obiektów i ich adresy e-mail kont.

```azurepowershell
ObjectId                               | PrincipalName
747ddfe5-xxxx-xxxx-xxxx-xxxxxxxxxxxx   | SignUpEngineering@contoso.com
4cd2fcf6-xxxx-xxxx-xxxx-xxxxxxxxxxxx   | BillingPlatformTeam@contoso.com
```

# <a name="azure-clitabazure-cli"></a>[Interfejs wiersza polecenia platformy Azure](#tab/azure-cli)

Użyj [az rozliczania konta rejestracji listy](https://aka.ms/EASubCreationPublicPreviewCLI) polecenie, aby wyświetlić listę wszystkich kont rejestracji, masz dostęp do.

```azurecli-interactive 
az billing enrollment-account list
```

Azure odpowiada za pomocą listy identyfikatorów obiektów i ich adresy e-mail kont.

```json
{
  "value": [
    {
      "id": "/providers/Microsoft.Billing/enrollmentAccounts/747ddfe5-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "name": "747ddfe5-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "type": "Microsoft.Billing/enrollmentAccounts",
      "properties": {
        "principalName": "SignUpEngineering@contoso.com"
      }
    },
    {
      "id": "/providers/Microsoft.Billing/enrollmentAccounts/747ddfe5-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "name": "4cd2fcf6-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "type": "Microsoft.Billing/enrollmentAccounts",
      "properties": {
        "principalName": "BillingPlatformTeam@contoso.com"
      }
    }
  ]
}
```

---

Użyj `principalName` właściwość do identyfikacji konta, naliczane w ramach subskrypcji. Użyj `id` jako `enrollmentAccount` wartości, których używasz do utworzenia subskrypcji w następnym kroku.

## <a name="create-subscriptions-under-a-specific-enrollment-account"></a>Utwórz subskrypcje w ramach konta określonego rejestracji 

Poniższy przykład tworzy żądanie, aby utworzyć subskrypcję o nazwie *subskrypcji zespołu deweloperów* i oferty subskrypcji *MS-AZR - 0017P* (regularnych EA). Konta rejestracji jest `747ddfe5-xxxx-xxxx-xxxx-xxxxxxxxxxxx` (identyfikator GUID jest wartość symbolu zastępczego, ta wartość), czyli konta rejestracji dla SignUpEngineering@contoso.com. Również opcjonalnie dodaje dwóch użytkowników jako właścicieli RBAC dla subskrypcji.

# <a name="resttabrest"></a>[REST](#tab/rest)

Użyj `id` z `enrollmentAccount` ścieżka żądania, aby utworzyć subskrypcję.

```json
POST https://management.azure.com/providers/Microsoft.Billing/enrollmentAccounts/747ddfe5-xxxx-xxxx-xxxx-xxxxxxxxxxxx/providers/Microsoft.Subscription/createSubscription?api-version=2018-03-01-preview

{
  "displayName": "Dev Team Subscription",
  "offerType": "MS-AZR-0017P",
  "owners": [
    {
      "objectId": "<userObjectId>"
    },
    {
      "objectId": "<servicePrincipalObjectId>"
    }
  ]
}
```

| Nazwa elementu  | Wymagane | Typ   | Opis                                                                                               |
|---------------|----------|--------|-----------------------------------------------------------------------------------------------------------|
| `displayName` | Nie      | Ciąg | Nazwa wyświetlana subskrypcji. Jeśli nie zostanie określony, jest ustawiona na nazwę tej oferty, takimi jak "Microsoft Azure Enterprise."                                 |
| `offerType`   | Yes      | Ciąg | Oferta subskrypcji. Istnieją dwie opcje w przypadku umowy EA [MS-AZR - 0017P](https://azure.microsoft.com/pricing/enterprise-agreement/) (użycia w środowisku produkcyjnym) i [MS-AZR - 0148P](https://azure.microsoft.com/offers/ms-azr-0148p/) (Tworzenie i testowanie, musi być [włączone w witrynie EA portal](https://ea.azure.com/helpdocs/DevOrTestOffer)).                |
| `owners`      | Nie       | Ciąg | Identyfikator obiektu każdemu użytkownikowi, który chcesz dodać jako właściciela RBAC w ramach subskrypcji, podczas jego tworzenia.  |

W odpowiedzi możesz wrócić `subscriptionOperation` obiektu monitorowania. Po zakończeniu tworzenia subskrypcji `subscriptionOperation` zwróci obiekt `subscriptionLink` obiektu, który ma identyfikator subskrypcji.

# <a name="powershelltabazure-powershell"></a>[Program PowerShell](#tab/azure-powershell)

Aby użyć tego modułu (wersja zapoznawcza), zainstaluj go, uruchamiając `Install-Module AzureRM.Subscription -AllowPrerelease` pierwszy. Aby upewnić się, że `-AllowPrerelease` dzieła, zainstalować najnowszą wersję modułu PowerShellGet z [uzyskiwanie modułu PowerShellGet](/powershell/gallery/installing-psget).

Użyj [New-AzureRmSubscription](/powershell/module/azurerm.subscription) wraz z `enrollmentAccount` obiekt o identyfikatorze jako `EnrollmentAccountObjectId` parametru, aby utworzyć nową subskrypcję. 

```azurepowershell-interactive
New-AzureRmSubscription -OfferType MS-AZR-0017P -Name "Dev Team Subscription" -EnrollmentAccountObjectId 747ddfe5-xxxx-xxxx-xxxx-xxxxxxxxxxxx -OwnerObjectId <userObjectId>,<servicePrincipalObjectId>
```

| Nazwa elementu  | Wymagane | Typ   | Opis                                                                                               |
|---------------|----------|--------|-----------------------------------------------------------------------------------------------------------|
| `Name` | Nie      | Ciąg | Nazwa wyświetlana subskrypcji. Jeśli nie zostanie określony, jest ustawiona na nazwę tej oferty, takimi jak "Microsoft Azure Enterprise."                                 |
| `OfferType`   | Yes      | Ciąg | Oferta subskrypcji. Istnieją dwie opcje w przypadku umowy EA [MS-AZR - 0017P](https://azure.microsoft.com/pricing/enterprise-agreement/) (użycia w środowisku produkcyjnym) i [MS-AZR - 0148P](https://azure.microsoft.com/offers/ms-azr-0148p/) (Tworzenie i testowanie, musi być [włączone w witrynie EA portal](https://ea.azure.com/helpdocs/DevOrTestOffer)).                |
| `EnrollmentAccountObjectId`      | Yes       | Ciąg | Identyfikator obiektu konta rejestracji, że subskrypcja jest utworzone w ramach i rozliczane. Ta wartość jest identyfikatorem GUID, który można pobrać z `Get-AzureRmEnrollmentAccount`. |
| `OwnerObjectId`      | Nie       | Ciąg | Identyfikator obiektu każdemu użytkownikowi, który chcesz dodać jako właściciela RBAC w ramach subskrypcji, podczas jego tworzenia.  |
| `OwnerSignInName`    | Nie       | Ciąg | Adres e-mail każdemu użytkownikowi, który chcesz dodać jako właściciela RBAC w ramach subskrypcji, podczas jego tworzenia. Można użyć tego parametru zamiast `OwnerObjectId`.|
| `OwnerApplicationId` | Nie       | Ciąg | Identyfikator aplikacji nazwy głównej usługi, który chcesz dodać jako właściciela RBAC w ramach subskrypcji, podczas jego tworzenia. Można użyć tego parametru zamiast `OwnerObjectId`. Korzystając z tego parametru, jednostka usługi musi mieć [dostęp do odczytu do katalogu](/powershell/azure/active-directory/signing-in-service-principal?view=azureadps-2.0#give-the-service-principal-reader-access-to-the-current-tenant-get-azureaddirectoryrole).| 

Aby wyświetlić pełną listę wszystkich parametrów, zobacz [New-AzureRmSubscription](/powershell/module/azurerm.subscription.preview).

# <a name="azure-clitabazure-cli"></a>[Interfejs wiersza polecenia platformy Azure](#tab/azure-cli)

Aby użyć tego rozszerzenia w wersji zapoznawczej, zainstaluj go, uruchamiając `az extension add --name subscription` pierwszy.

Użyj [Utwórz konto az](/cli/azure/ext/subscription/account?view=azure-cli-latest#-ext-subscription-az-account-create) wraz z `enrollmentAccount` obiekt o identyfikatorze jako `enrollment-account-object-id` parametru, aby utworzyć nową subskrypcję.

```azurecli-interactive 
az account create --offer-type "MS-AZR-0017P" --display-name "Dev Team Subscription" --enrollment-account-object-id "747ddfe5-xxxx-xxxx-xxxx-xxxxxxxxxxxx" --owner-object-id "<userObjectId>","<servicePrincipalObjectId>"
```

| Nazwa elementu  | Wymagane | Typ   | Opis                                                                                               |
|---------------|----------|--------|-----------------------------------------------------------------------------------------------------------|
| `display-name` | Nie      | Ciąg | Nazwa wyświetlana subskrypcji. Jeśli nie zostanie określony, jest ustawiona na nazwę tej oferty, takimi jak "Microsoft Azure Enterprise."                                 |
| `offer-type`   | Yes      | Ciąg | Oferta subskrypcji. Istnieją dwie opcje w przypadku umowy EA [MS-AZR - 0017P](https://azure.microsoft.com/pricing/enterprise-agreement/) (użycia w środowisku produkcyjnym) i [MS-AZR - 0148P](https://azure.microsoft.com/offers/ms-azr-0148p/) (Tworzenie i testowanie, musi być [włączone w witrynie EA portal](https://ea.azure.com/helpdocs/DevOrTestOffer)).                |
| `enrollment-account-object-id`      | Yes       | Ciąg | Identyfikator obiektu konta rejestracji, że subskrypcja jest utworzone w ramach i rozliczane. Ta wartość jest identyfikatorem GUID, który można pobrać z `az billing enrollment-account list`. |
| `owner-object-id`      | Nie       | Ciąg | Identyfikator obiektu każdemu użytkownikowi, który chcesz dodać jako właściciela RBAC w ramach subskrypcji, podczas jego tworzenia.  |
| `owner-upn`    | Nie       | Ciąg | Adres e-mail każdemu użytkownikowi, który chcesz dodać jako właściciela RBAC w ramach subskrypcji, podczas jego tworzenia. Można użyć tego parametru zamiast `owner-object-id`.|
| `owner-spn` | Nie       | Ciąg | Identyfikator aplikacji nazwy głównej usługi, który chcesz dodać jako właściciela RBAC w ramach subskrypcji, podczas jego tworzenia. Można użyć tego parametru zamiast `owner-object-id`. Korzystając z tego parametru, jednostka usługi musi mieć [dostęp do odczytu do katalogu](/powershell/azure/active-directory/signing-in-service-principal?view=azureadps-2.0#give-the-service-principal-reader-access-to-the-current-tenant-get-azureaddirectoryrole).| 

Aby wyświetlić pełną listę wszystkich parametrów, zobacz [Utwórz konto az](/cli/azure/ext/subscription/account?view=azure-cli-latest#-ext-subscription-az-account-create).

----

## <a name="limitations-of-azure-enterprise-subscription-creation-api"></a>Ograniczenia interfejsu API tworzenia subskrypcji Azure Enterprise

- Tylko subskrypcje Azure Enterprise mogą być tworzone za pomocą tego interfejsu API.
- Ma limitu 50 subskrypcji na jednym koncie. Po tym można tworzyć za pomocą Centrum kont tylko subskrypcje.
- Musi istnieć co najmniej jedną EA lub oferty i testowanie subskrypcje w ramach konta, co oznacza, że właściciel konta stała się za pomocą ręcznego tworzenia konta co najmniej raz.
- Użytkownicy, którzy nie są właścicielami kont, ale zostały dodane do konta rejestracji za pośrednictwem RBAC, nie można utworzyć subskrypcji za pomocą Centrum kont.
- Nie można wybrać dzierżawy dla subskrypcji, które zostały utworzone w. Subskrypcja zawsze jest tworzony w głównej dzierżawy właściciela konta. Aby przenieść subskrypcję do innej dzierżawy, zobacz [dzierżawy subskrypcji zmienić](../active-directory/fundamentals/active-directory-how-subscriptions-associated-directory.md).

## <a name="next-steps"></a>Kolejne kroki

* Na przykład na temat tworzenia subskrypcji przy użyciu platformy .NET, zobacz [przykładowego kodu w serwisie GitHub](https://github.com/Azure-Samples/create-azure-subscription-dotnet-core).
* Teraz, po utworzeniu subskrypcji, można przyznać tej możliwości do innych użytkowników i nazwy główne usług. Aby uzyskać więcej informacji, zobacz [udzielić dostępu do utworzenia subskrypcji Azure Enterprise (wersja zapoznawcza)](grant-access-to-create-subscription.md).
* Aby dowiedzieć się więcej na temat zarządzania dużą liczbą subskrypcji przy użyciu grup zarządzania, zobacz [organizowanie zasobów przy użyciu grup zarządzania platformy Azure](management-groups-overview.md)
