---
title: Źródła danych obsługiwane w usługach Azure Analysis Services | Dokumentacja firmy Microsoft
description: W tym artykule opisano źródła danych obsługiwane dla modeli danych w usługach Azure Analysis Services.
author: minewiskan
manager: kfile
ms.service: azure-analysis-services
ms.topic: conceptual
ms.date: 01/09/2019
ms.author: owend
ms.reviewer: minewiskan
ms.openlocfilehash: e1a001a60151136be6bde9de38f971807cf0c288
ms.sourcegitcommit: 63b996e9dc7cade181e83e13046a5006b275638d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/10/2019
ms.locfileid: "54188406"
---
# <a name="data-sources-supported-in-azure-analysis-services"></a>Źródła danych obsługiwane w usługach Azure Analysis Services

Źródła danych i łączniki, Pobierz dane lub Kreatora importu w programie Visual Studio są wyświetlane dla usług Azure Analysis Services i SQL Server Analysis Services. Jednak nie wszystkie źródła danych i łączników, wyświetlane są obsługiwane w usługach Azure Analysis Services. Rodzaje źródeł danych, którymi się łączysz może zależeć od wielu czynników, takich jak model, poziom zgodności, łączników danych o dostępności, typ uwierzytelniania, dostawców i obsługa bramy danych lokalnych. 

## <a name="azure-data-sources"></a>Źródła danych na platformie Azure

|Źródło danych  |W pamięci  |Tryb DirectQuery  |
|---------|---------|---------|
|Azure SQL Database     |   Yes      |    Yes      |
|Azure SQL Data Warehouse     |   Yes      |   Yes       |
|Azure Blob Storage*     |   Yes       |    Nie      |
|Azure Table Storage*    |   Yes       |    Nie      |
|Azure Cosmos DB*     |  Yes        |  Nie        |
|Azure Data Lake Store*     |   Yes       |    Nie      |
|Azure HDInsight HDFS*     |     Yes     |   Nie       |
|Usługa Azure HDInsight Spark *     |   Yes       |   Nie       |
||||

\* Modele tabelaryczne 1400 tylko.

**Dostawcy**   
W pamięci i modele zapytania bezpośredniego połączenia ze źródłami danych platformy Azure Użyj dostawcy danych .NET Framework dla programu SQL Server.

## <a name="on-premises-data-sources"></a>Lokalne źródła danych

Nawiązywanie połączenia z lokalnych źródeł danych z i serwera usług Azure AS wymagają lokalnej bramy. Podczas korzystania z bramy, 64-bitowego dostawcy są wymagane.

### <a name="in-memory-and-directquery"></a>W pamięci i zapytania bezpośredniego

|Źródło danych | Dostawca w pamięci | Dostawcy zapytań bezpośrednich |
|  --- | --- | --- |
| Oprogramowanie SQL Server |SQL Server Native Client 11.0, dostawca OLE DB firmy Microsoft dla programu SQL Server, .NET Framework Data Provider for SQL Server | .NET framework Data Provider for SQL Server |
| SQL Server Data Warehouse |SQL Server Native Client 11.0, dostawca OLE DB firmy Microsoft dla programu SQL Server, .NET Framework Data Provider for SQL Server | .NET framework Data Provider for SQL Server |
| Oracle |Dostawca Microsoft OLE DB dla Oracle, dostawca danych programu Oracle dla platformy .NET |Dostawca danych programu Oracle dla platformy .NET | |
| Teradata |Dostawca OLE DB dla programu Teradata, dostawca danych programu Teradata dla platformy .NET |Dostawca danych programu Teradata dla platformy .NET | |
| | | |

### <a name="in-memory-only"></a>W pamięci tylko

|Źródło danych  |  
|---------|---------|
|Baza danych programu Access     |  
|Active Directory *     |  
|Analysis Services     |  
|System Analytics Platform System     |  
|Dynamics CRM*     |  
|Skoroszyt programu Excel     |  
|Exchange*     |  
|Folder *     |
|IBM Informix * (wersja Beta) |
|Dokument JSON *     |  
|Wiersze z pliku binarnego *     | 
|Baza danych MySQL     | 
|Źródło danych OData *     |  
|Zapytanie ODBC     | 
|OLE DB     |   
|Baza danych Postgre SQL *    | 
|Obiekty SalesForce * |  
|Raporty usługi SalesForce * |
|SAP HANA *    |  
|SAP Business Warehouse *    |  
|SharePoint*     |   
|Baza danych programu Sybase     |  
|XML tabeli *    |  
|||
 
\* Modele tabelaryczne 1400 tylko.

## <a name="specifying-a-different-provider"></a>Określenie innego dostawcy

Modele danych w usługach Azure Analysis Services może wymagać danych różnych dostawców, podczas nawiązywania połączenia ze źródłami danych, niektórych. W niektórych przypadkach modele tabelaryczne łączenie ze źródłami danych przy użyciu natywnych dostawców, takich jak SQL Server Native Client (SQLNCLI11) może zostać zwrócony błąd. Jeśli przy użyciu natywnych dostawców innych niż SQLOLEDB, mogą pojawić się komunikat o błędzie: **Dostawca "SQLNCLI11.1" nie jest zarejestrowana**. Lub, jeśli mają model zapytania bezpośredniego połączenia ze źródłami danych lokalnie i korzystać z natywnych dostawców, może zostać wyświetlony komunikat o błędzie: **Wystąpił błąd podczas tworzenia zestawu wierszy OLE DB. Błędna składnia w pobliżu "LIMIT"**.

Podczas migracji modelu tabelarycznego usług SQL Server Analysis Services do środowiska lokalnego do usług Azure Analysis Services, może być konieczna zmiana dostawcy.

**Aby określić dostawcę**

1. W programie SSDT > **Eksploratorze modeli tabelarycznych** > **źródeł danych**, kliknij prawym przyciskiem myszy połączenie ze źródłem danych, a następnie kliknij przycisk **Edytuj źródło danych**.
2. W **Edytowanie połączenia**, kliknij przycisk **zaawansowane** aby otworzyć okno właściwości zaawansowane.
3. W **ustawić zaawansowane właściwości** > **dostawców**, następnie wybierz odpowiedniego dostawcę.

## <a name="impersonation"></a>Personifikacja
W niektórych przypadkach może być konieczne określenie konta personifikacji różne. Można określić konta personifikacji w programie Visual Studio (SSDT) lub programu SSMS.

W przypadku lokalnych źródeł danych:

* Jeśli przy użyciu uwierzytelniania SQL, personifikacji powinna być konto usługi.
* W przypadku korzystania z uwierzytelniania Windows należy ustawić hasło użytkownika Windows. Dla programu SQL Server uwierzytelnianie Windows przy użyciu konta personifikacji określonych jest obsługiwane tylko w przypadku modeli danych w pamięci.

W przypadku źródeł danych w chmurze:

* Jeśli przy użyciu uwierzytelniania SQL, personifikacji powinna być konto usługi.

## <a name="next-steps"></a>Kolejne kroki
[Lokalna brama](analysis-services-gateway.md)   
[Zarządzanie serwerem](analysis-services-manage.md)   

