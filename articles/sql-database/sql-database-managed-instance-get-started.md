---
title: 'Azure Portal: tworzenie wystąpienia zarządzanego SQL | Microsoft Docs'
description: Tworzenie wystąpienia zarządzanego SQL, środowiska sieciowego i udostępnionej maszyny wirtualnej klienta.
services: sql-database
ms.service: sql-database
ms.subservice: managed-instance
ms.custom: ''
ms.devlang: ''
ms.topic: quickstart
author: jovanpop-msft
ms.author: jovanpop
ms.reviewer: Carlrab
manager: craigg
ms.date: 01/15/2019
ms.openlocfilehash: 201ba431a4382741815536db2bb4d08f0068be80
ms.sourcegitcommit: dede0c5cbb2bd975349b6286c48456cfd270d6e9
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/16/2019
ms.locfileid: "54329545"
---
# <a name="quickstart-create-an-azure-sql-database-managed-instance"></a>Szybki start: Tworzenie wystąpienia zarządzanego usługi Azure SQL Database

Ten przewodnik Szybki start przeprowadzi Cię przez proces tworzenia [wystąpienia zarządzanego](sql-database-managed-instance.md) usługi Azure SQL Database w witrynie Azure Portal.

Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem [utwórz bezpłatne konto](https://azure.microsoft.com/free/).

## <a name="sign-in-to-the-azure-portal"></a>Logowanie się do witryny Azure Portal

Zaloguj się w witrynie [Azure Portal](https://portal.azure.com/).

## <a name="create-a-managed-instance"></a>Tworzenie wystąpienia zarządzanego

Poniższe kroki przedstawiają sposób tworzenia wystąpienia zarządzanego.

1. W lewym górnym rogu okna witryny Azure Portal wybierz pozycję **Utwórz zasób**.
2. Zlokalizuj pozycję **Wystąpienie zarządzane**, a następnie wybierz pozycję **Wystąpienie zarządzane usługi Azure SQL**.
3. Wybierz pozycję **Utwórz**.

   ![Tworzenie wystąpienia zarządzanego](./media/sql-database-managed-instance-get-started/managed-instance-create.png)

4. Wypełnij formularz **wystąpienia zarządzanego**, podając wymagane informacje. Skorzystaj z informacji w następującej tabeli:

   | Ustawienie| Sugerowana wartość | Opis |
   | ------ | --------------- | ----------- |
   | **Subskrypcja** | Twoja subskrypcja | Subskrypcja, w której masz uprawnienie do tworzenia nowych zasobów |
   |**Nazwa wystąpienia zarządzanego**|Dowolna prawidłowa nazwa|Prawidłowe nazwy opisano w artykule [Ograniczenia i reguły nazewnictwa](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).|
   |**Identyfikator logowania administratora wystąpienia zarządzanego**|Dowolna prawidłowa nazwa użytkownika|Prawidłowe nazwy opisano w artykule [Ograniczenia i reguły nazewnictwa](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions). Nie używaj nazwy „serveradmin”, gdyż jest ona zarezerwowana dla roli poziomu serwera.|
   |**Hasło**|Dowolne prawidłowe hasło|Hasło musi mieć co najmniej 16 znaków i spełniać [zdefiniowane wymagania dotyczące złożoności](../virtual-machines/windows/faq.md#what-are-the-password-requirements-when-creating-a-vm).|
   |**Sortowanie**|Sortowanie, którego chcesz użyć dla wystąpienia zarządzanego|Aby uzyskać informacje na temat sortowań, zobacz [Collations](https://docs.microsoft.com/sql/t-sql/statements/collations) (Sortowania).|
   |**Lokalizacja**|Lokalizacja, w której chcesz utworzyć wystąpienie zarządzane|Aby uzyskać informacje na temat regionów, zobacz temat [Regiony platformy Azure](https://azure.microsoft.com/regions/).|
   |**Sieć wirtualna**|Wybierz opcję **Utwórz nową sieć wirtualną** lub prawidłową sieć wirtualną i podsieć.| Jeśli sieć/podsieć jest wyszarzona, musi zostać [zmodyfikowana, aby spełnić wymagania dotyczące sieci](sql-database-managed-instance-configure-vnet-subnet.md), zanim będzie można wybrać ją jako miejsce docelowe dla nowego wystąpienia zarządzanego. Aby uzyskać informacje o wymaganiach dotyczących konfigurowania środowiska sieci dla wystąpienia zarządzanego, zobacz [Konfigurowanie sieci wirtualnej dla wystąpienia zarządzanego Azure SQL Database](sql-database-managed-instance-connectivity-architecture.md). |
   |**Grupa zasobów**|Nowa lub istniejąca grupa zasobów|Prawidłowe nazwy grup zasobów opisano w artykule [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Reguły i ograniczenia nazewnictwa).|

   ![formularz wystąpienia zarządzanego](./media/sql-database-managed-instance-get-started/managed-instance-create-form.png)

5. Aby użyć wystąpienia zarządzanego jako pomocniczej grupy trybu failover wystąpienia, zaznacz pole wyboru i określ wystąpienie zarządzane DnsAzurePartner. Ta funkcja jest dostępna w wersji zapoznawczej i nie jest pokazana na towarzyszącym zrzucie ekranu.
6. Wybierz pozycję **Warstwa cenowa**, aby ustalić rozmiar zasobów obliczeniowych i magazynu, a także sprawdzić opcje warstw cenowych. Wartość domyślna to warstwa cenowa Ogólnego przeznaczenia z 32 GB pamięci i 16 rdzeniami wirtualnymi.
7. Użyj suwaków lub pól tekstowych, aby określić ilość pamięci i liczbę rdzeni wirtualnych.
8. Po zakończeniu wybierz pozycję **Zastosuj**, aby zapisać wybór.  
9. Wybierz pozycję **Utwórz**, aby wdrożyć wystąpienie zarządzane.
10. Wybierz ikonę **Powiadomienia**, aby wyświetlić stan wdrożenia.

    ![postęp wdrożenia wystąpienia zarządzanego](./media/sql-database-managed-instance-get-started/deployment-progress.png)

11. Wybierz pozycję **Wdrażanie jest w toku**, aby otworzyć okno wystąpienia zarządzanego i dokładniej monitorować postęp wdrażania.

> [!IMPORTANT]
> W przypadku pierwszego wystąpienia w podsieci czas wdrożenia jest zazwyczaj znacznie dłuższy niż w kolejnych wystąpieniach. Nie anuluj operacji wdrażania, ponieważ proces trwa dłużej niż oczekiwano. Utworzenie drugiego wystąpienia zarządzanego w podsieci trwa tylko kilka minut.

## <a name="review-resources-and-retrieve-your-fully-qualified-server-name"></a>Przeglądanie zasobów i pobieranie w pełni kwalifikowanej nazwy serwera

Po pomyślnym ukończeniu wdrażania przejrzyj utworzone zasoby i pobierz w pełni kwalifikowaną nazwę serwera do użycia w kolejnych przewodnikach Szybki start.

1. Otwórz grupę zasobów wystąpienia zarządzanego i wyświetl jej zasoby utworzone dla Ciebie w przewodniku Szybki start [Tworzenie wystąpienia zarządzanego](#create-a-managed-instance).

2. Wybierz wystąpienie zarządzane.

   ![Zasoby wystąpienia zarządzanego](./media/sql-database-managed-instance-get-started/resources.png)

3. Na karcie **Omówienie** znajdź właściwość **Host** i skopiuj w pełni kwalifikowany adres hosta dla wystąpienia zarządzanego.

   ![Zasoby wystąpienia zarządzanego](./media/sql-database-managed-instance-get-started/host-name.png)

   Nazwa jest podobna do **nazwa_maszyny.a1b2c3d4e5f6.database.windows.net**.

## <a name="next-steps"></a>Następne kroki

- Aby dowiedzieć się więcej na temat nawiązywania połączenia z wystąpieniem zarządzanym, zobacz:
  - Aby uzyskać omówienie opcji połączenia dla aplikacji, zobacz artykuł [Łączenie aplikacji z wystąpieniem zarządzanym](sql-database-managed-instance-connect-app.md).
  - Aby skorzystać z samouczka przedstawiającego sposób łączenia wystąpienia zarządzanego z maszyny wirtualnej platformy Azure, zobacz [Configure an Azure virtual machine connection](sql-database-managed-instance-configure-vm.md) (Konfigurowanie połączenia maszyny wirtualnej platformy Azure).
  - Aby skorzystać z przewodnika Szybki start przedstawiającego sposób łączenia wystąpienia zarządzanego z poziomu lokalnego komputera klienckiego za pomocą połączenia typu punkt-lokacja, zobacz [Konfigurowanie połączenia punkt-lokacja](sql-database-managed-instance-configure-p2s.md).
- Aby przywrócić istniejącą bazę danych programu SQL ze środowiska lokalnego do wystąpienia zarządzanego, możesz użyć [usługi Azure Database Migration Service (DMS) na potrzeby migracji](../dms/tutorial-sql-server-to-managed-instance.md) lub [polecenia T-SQL RESTORE](sql-database-managed-instance-get-started-restore.md) w celu przywrócenia z pliku kopii zapasowej bazy danych.
- Aby uzyskać informacje na temat zaawansowanego monitorowania wydajności bazy danych wystąpienia zarządzanego z wbudowaną analizą rozwiązywania problemów, zobacz [Monitorowanie usługi Azure SQL Database przy użyciu usługi Azure SQL Analytics](../azure-monitor/insights/azure-sql.md)
