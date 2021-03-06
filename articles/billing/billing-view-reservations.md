---
title: Wyświetl rezerwacji dla zasobów platformy Azure | Dokumentacja firmy Microsoft
description: Dowiedz się, jak wyświetlić rezerwacje platformy Azure w witrynie Azure portal.
services: billing
documentationcenter: ''
author: yashesvi
manager: yashar
editor: ''
ms.service: billing
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/03/2018
ms.author: cwatson
ms.openlocfilehash: c7522076987aacacc6fde6a0c9d2fa867a3f14aa
ms.sourcegitcommit: eb9dd01614b8e95ebc06139c72fa563b25dc6d13
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/12/2018
ms.locfileid: "53314044"
---
# <a name="view-reservations-for-azure-in-the-azure-portal"></a>Wyświetlanie rezerwacji dla platformy Azure w witrynie Azure portal

W zależności od typu subskrypcji i uprawnienia istnieje kilka sposobów wyświetlania rezerwacji dla zasobów platformy Azure.

## <a name="view-reservations-as-owner-or-reader"></a>Wyświetlanie rezerwacji jako właściciela lub czytelnika

Domyślnie w przypadku dokonywania zakupu rezerwacji, użytkownika i administratora konta można wyświetlić rezerwacji. Użytkownika i administratora konta automatycznie uzyskują roli właściciela o rezerwacji. Aby zezwolić innym osobom wyświetlić rezerwacji, należy dodać je jako **właściciela** lub **czytnika** na rezerwacji. Aby uzyskać więcej informacji, zobacz [apletu Dodaj lub zmień użytkowników, którzy mogą zarządzać rezerwacji](billing-manage-reserved-vm-instance.md#add-or-change-users-who-can-manage-a-reservation).
 
Aby wyświetlić rezerwacji jako właściciel lub czytnika,

1. Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).
1. Wyszukiwanie **rezerwacje**.

    ![Zrzut ekranu pokazujący usługi Azure search w portalu](./media/billing-view-reservation/portal-reservation-search.png)

1. Możesz wyświetlić listę rezerwacji, których masz rolę właściciela lub czytelnika.

Jeśli musisz zmienić zakres rezerwacji podziału rezerwacji lub zmiany, kto może zarządzać rezerwacji, zapoznaj się z [Zarządzanie zastrzeżeniami Azure](billing-manage-reserved-vm-instance.md).

## <a name="view-reservation-transactions-for-enterprise-enrollments"></a>Wyświetl transakcje rezerwacji dla rejestracji Enterprise

 W przypadku rejestracji Enterprise partnera prowadzone wyświetlić rezerwacje, przechodząc do **raporty** w witrynie EA portal. Inne rejestracje Enterprise można wyświetlić rezerwacje w witrynie EA portal i w witrynie Azure portal. Musi być administrator umowy EA, aby wyświetlać transakcje rezerwacji.

Aby wyświetlić transakcje rezerwacji w witrynie Azure portal

1. Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).
1. Wyszukiwanie **Cost Management + rozliczenia**.

    ![Zrzut ekranu pokazujący usługi Azure search w portalu](./media/billing-view-reservation/portal-cm-billing-search.png)

1. Wybierz **transakcji rezerwacji**.
1. Aby filtrować wyniki, wybierz **Timespan**, **typu**, lub **opis**.
1. Wybierz przycisk **Zastosuj**.

    ![Zrzut ekranu pokazujący rezerwacji wyniki transakcji](./media/billing-view-reservation/portal-billing-reservation-transaction-results.png)

Aby uzyskać dane przy użyciu interfejsu API, zobacz [opłaty za transakcje Pobieranie wystąpień zarezerwowanych dla klientów korporacyjnych](/rest/api/billing/enterprise/billing-enterprise-api-reserved-instance-charges).

## <a name="next-steps"></a>Kolejne kroki

Aby dowiedzieć się więcej na temat rezerwacji platformy Azure, zobacz następujące artykuły:

- [Co to są rezerwacje platformy Azure?](billing-save-compute-costs-reservations.md)
- [Zapłać z góry za pojemność usługi Cosmos DB zastrzeżone](../cosmos-db/cosmos-db-reserved-capacity.md)
- [Prepay for SQL Database compute resources with Azure SQL Database reserved capacity (Opłacanie zasobów obliczeniowych usługi SQL Database z góry przy użyciu zarezerwowanej pojemności usługi Azure SQL Database)](../sql-database/sql-database-reserved-capacity.md)
- [Prepay for Virtual Machines with Azure Reserved VM Instances (Opłacanie maszyn wirtualnych z góry przy użyciu usługi Azure Reserved VM Instances)](../virtual-machines/windows/prepay-reserved-vm-instances.md)
- [Zarządzanie rezerwacjami platformy Azure](billing-manage-reserved-vm-instance.md)
- [Opis zastrzeżenia dla Twojej subskrypcji zgodnie z rzeczywistym użyciem](billing-understand-reserved-instance-usage.md)
- [Opis zastrzeżenia dla Twojej rejestracji Enterprise](billing-understand-reserved-instance-usage-ea.md)
- [Opis zastrzeżenia dla subskrypcji programu CSP](https://docs.microsoft.com/partner-center/azure-reservations)

## <a name="need-help-contact-us"></a>Potrzebujesz pomocy? Skontaktuj się z nami.

Jeśli masz pytania lub potrzebujesz pomocy, [Utwórz żądanie obsługi](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/newsupportrequest).
