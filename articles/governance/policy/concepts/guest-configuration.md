---
title: Dowiedz się, jak przeprowadzić inspekcji na maszynie wirtualnej
description: Dowiedz się, jak korzysta z usługi Azure Policy konfiguracji gościa na Przeprowadź inspekcję ustawienia w ramach maszyny wirtualnej platformy Azure.
services: azure-policy
author: DCtheGeek
ms.author: dacoulte
ms.date: 12/06/2018
ms.topic: conceptual
ms.service: azure-policy
manager: carmonm
ms.custom: seodec18
ms.openlocfilehash: 1ea87dc01048a2747a668db7a5b1f22b37ed9213
ms.sourcegitcommit: eb9dd01614b8e95ebc06139c72fa563b25dc6d13
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/12/2018
ms.locfileid: "53310066"
---
# <a name="understand-azure-policys-guest-configuration"></a>Omówienie usługi Azure Policy gościa konfiguracji

Oprócz przeprowadzania inspekcji i [korygowanie](../how-to/remediate-resources.md) zasobów platformy Azure, usługi Azure Policy jest w stanie inspekcji ustawień na maszynie wirtualnej. Sprawdzanie poprawności jest wykonywane przez rozszerzenie konfiguracji gościa i klienta. Rozszerzenie, za pomocą klienta, sprawdza poprawność ustawień, takich jak konfiguracja systemu operacyjnego, Konfiguracja aplikacji lub obecności i ustawienia środowiska.

> [!IMPORTANT]
> Obecnie tylko **wbudowanych** zasady są obsługiwane przy użyciu konfiguracji gościa.

## <a name="extension-and-client"></a>Rozszerzenie i klienta

Inspekcja ustawień na maszynie wirtualnej [rozszerzenie maszyny wirtualnej](../../../virtual-machines/extensions/overview.md) jest włączona. Rozszerzenie pobiera przypisania zasad mających zastosowanie i odpowiedniej definicji konfiguracji.

### <a name="register-guest-configuration-resource-provider"></a>Procedura Rejestruj dostawcę zasobów konfiguracji gościa

Zanim użyjesz konfiguracji gościa, należy zarejestrować dostawcę zasobów. Możesz zarejestrować się za pośrednictwem portalu lub za pomocą programu PowerShell.

#### <a name="registration---portal"></a>Rejestracja — Portal

Aby zarejestrować dostawcę zasobów dla konfiguracji gościa za pośrednictwem witryny Azure portal, wykonaj następujące kroki:

1. Uruchamianie witryny Azure portal, a następnie kliknij polecenie **wszystkich usług**. Wyszukaj i wybierz pozycję **subskrypcje**.

1. Znajdź, a następnie kliknij subskrypcję, dla której chcesz włączyć konfigurację gościa.

1. W menu po lewej stronie **subskrypcji** kliknij **dostawców zasobów**.

1. Filtruj lub przewiń do momentu zlokalizowania **Microsoft.GuestConfiguration**, następnie kliknij przycisk **zarejestrować** na tym samym wierszu.

#### <a name="registration---powershell"></a>Rejestracja — PowerShell

Aby zarejestrować dostawcę zasobów dla konfiguracji gościa za pomocą programu PowerShell, uruchom następujące polecenie:

```azurepowershell-interactive
# Login first with Connect-AzureRmAccount if not using Cloud Shell
Register-AzureRmResourceProvider -ProviderNamespace 'Microsoft.GuestConfiguration'
```

### <a name="validation-tools"></a>Narzędzia do sprawdzania poprawności

Wewnątrz maszyny wirtualnej gościa konfiguracji klient korzysta z lokalnego narzędzia przeprowadzić inspekcji.

W poniższej tabeli przedstawiono listę narzędzi lokalnego, używane we wszystkich obsługiwanych systemach operacyjnych:

|System operacyjny|Narzędzie sprawdzania poprawności|Uwagi|
|-|-|-|
|Windows|[Microsoft Desired State Configuration](/powershell/dsc) v2| |
|Linux|[Program chef InSpec](https://www.chef.io/inspec/)| Język Ruby i Python są instalowane przez rozszerzenie konfiguracji gościa. |

### <a name="supported-client-types"></a>Typy obsługiwanych klientów

W poniższej tabeli przedstawiono listę obsługiwanych systemów operacyjnych na obrazach platformy Azure:

|Wydawca|Name (Nazwa)|Wersje|
|-|-|-|
|Canonical|Ubuntu Server|14.04 16.04, 18.04|
|credativ|Debian|8, 9|
|Microsoft|Windows Server|2012 Datacenter, 2012 R2 Datacenter, 2016 Datacenter|
|OpenLogic|CentOS|7.3, 7.4, 7.5|
|Red Hat|Red Hat Enterprise Linux|7.4, 7.5|
|SUSE|SLES|12 Z DODATKIEM SP3|

> [!IMPORTANT]
> Konfiguracja gościa nie jest obecnie obsługiwane w przypadku niestandardowych maszyn wirtualnych z obrazów.

### <a name="unsupported-client-types"></a>Typy klientów nieobsługiwanych

W poniższej tabeli wymieniono systemy operacyjne, które nie są obsługiwane:

|System operacyjny|Uwagi|
|-|-|
|Klient systemu Windows | Systemy operacyjne klienta (takich jak Windows 7 i Windows 10) nie są obsługiwane.
|Windows Server 2016 Nano Server | Nieobsługiwane.|

## <a name="guest-configuration-definition-requirements"></a>Wymagania dotyczące definicji konfiguracji gościa

Każdy inspekcji uruchamiane przez gościa konfiguracji wymaga dwiema definicjami zasad **DeployIfNotExists** i **AuditIfNotExists**. **DeployIfNotExists** służy do przygotowywania maszyny wirtualnej za pomocą agenta gościa, konfiguracji i inne składniki do obsługi [narzędzia do sprawdzania poprawności](#validation-tools).

**DeployIfNotExists** definicji zasad sprawdza i naprawia następujące elementy:

- Sprawdzanie poprawności konfiguracji w celu oceny zostały przypisane maszyny wirtualnej. W przypadku aktualnie nie przypisania uzyskać przydział i przygotowywanie maszyny wirtualnej za pomocą:
  - Uwierzytelnianie na maszynę wirtualną przy użyciu [tożsamości zarządzanej](../../../active-directory/managed-identities-azure-resources/overview.md)
  - Instalowanie najnowszej wersji **Microsoft.GuestConfiguration** rozszerzenia
  - Instalowanie [narzędzia do sprawdzania poprawności](#validation-tools) i zależności, jeśli to konieczne

Gdy **DeployIfNotExists** jest zgodne, **AuditIfNotExists** definicji zasad używa lokalna Weryfikacja narzędzi w celu ustalenia, czy przypisanie przypisanej konfiguracji jest zgodne lub Niezgodne. Narzędzie sprawdzania poprawności zapewnia wyniki do klienta konfiguracji gościa. Klient przesyła wyniki z rozszerzeniem gościa i udostępnia je za pośrednictwem dostawcy zasobów gościa konfiguracji.

Usługa Azure Policy korzysta z dostawców zasobów gościa konfiguracji **complianceStatus** właściwości raportu zgodności w **zgodności** węzła. Aby uzyskać więcej informacji, zobacz [pobierania danych zgodności](../how-to/getting-compliance-data.md).

> [!NOTE]
> Dla każdej definicji konfiguracji gościa zarówno **DeployIfNotExists** i **AuditIfNotExists** definicje zasad, musi istnieć.

Wszystkie wbudowane zasady konfiguracji gościa znajdują się w inicjatywy do grupy definicje służące do użycia w przypisaniach. Wbudowane inicjatywę o nazwie *[wersja zapoznawcza]: Przeprowadź inspekcję ustawienia zabezpieczeń hasła wewnątrz maszyn wirtualnych z systemem Linux i Windows* zawiera zasady 18. Sześć **DeployIfNotExists** i **AuditIfNotExists** pary dla Windows i trzy pary dla systemu Linux. W każdym przypadku logiki wewnątrz definicji sprawdza tylko element docelowy system operacyjny jest obliczana na podstawie [reguła zasad](definition-structure.md#policy-rule) definicji.

## <a name="next-steps"></a>Kolejne kroki

- Przejrzyj przykłady na [przykładów usługi Azure Policy](../samples/index.md)
- Przegląd [struktura definicji zasad](definition-structure.md)
- Przegląd [zrozumienia efektów zasad](effects.md)
- Zrozumienie sposobu [programowe tworzenie zasad](../how-to/programmatically-create.md)
- Dowiedz się, jak [uzyskać dane na temat zgodności](../how-to/getting-compliance-data.md)
- Dowiedz się, jak [korygowanie niezgodnych zasobów](../how-to/remediate-resources.md)
- Sprawdzanie, co to jest grupa zarządzania, na stronie [Organize your resources with Azure management groups (Organizowanie zasobów za pomocą grup zarządzania platformy Azure)](../../management-groups/index.md)