---
title: Plik dyrektywy include
description: Plik dyrektywy include
services: azure-policy
author: DCtheGeek
ms.service: azure-policy
ms.topic: include
ms.date: 10/29/2018
ms.author: dacoulte
ms.custom: include file
ms.openlocfilehash: 7bf885f2ab81e5d86878d2b0b53f4e98b8aedd9a
ms.sourcegitcommit: eb9dd01614b8e95ebc06139c72fa563b25dc6d13
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/12/2018
ms.locfileid: "53318355"
---
### <a name="sql-databases"></a>Bazy danych SQL

|  |  |
|---------|---------|
| [Allowed SQL DB SKUs](../articles/governance/policy/samples/allowed-sql-db-skus.md) (Dozwolone jednostki SKU usługi SQL DB) | Wymaga, aby bazy danych SQL używały zatwierdzonych jednostek SKU. Należy określić tablicę identyfikatorów dozwolonych jednostek SKU lub tablicę nazw dozwolonych jednostek SKU. |
| [Audit DB level threat detection setting](../articles/governance/policy/samples/audit-db-threat-detection-setting.md) (Przeprowadzanie inspekcji ustawień wykrywania zagrożeń na poziomie bazy danych) | Przeprowadza inspekcję zasad alertu zabezpieczeń bazy danych SQL, dla których nie ustawiono określonego stanu. Należy określić wartość, która wskazuje, czy wykrywanie zagrożeń ma być włączone czy wyłączone.  |
| [Audit SQL Database encryption](../articles/governance/policy/samples/sql-database-encryption-audit.md) (Inspekcja szyfrowania w usłudze SQL Database) | Sprawdza, czy usługa SQL Database nie ma włączonego przezroczystego szyfrowania danych. |
| [Audit SQL DB Level Audit Setting](../articles/governance/policy/samples/audit-sql-db-audit-setting.md) (Przeprowadzanie inspekcji ustawień inspekcji na poziomie usługi SQL Database) | Sprawdza, czy ustawienia inspekcji usługi SQL Database nie są zgodne z określonym ustawieniem. Należy określić wartość, która wskazuje, czy ustawienia inspekcji mają być włączone czy wyłączone.  |