---
title: Anuluj operację interfejsu API | Dokumentacja firmy Microsoft
description: Anulowanie operacji.
services: Azure, Marketplace, Cloud Partner Portal,
documentationcenter: ''
author: v-miclar
manager: Patrick.Butler
editor: ''
ms.assetid: ''
ms.service: marketplace
ms.workload: ''
ms.tgt_pltfrm: ''
ms.devlang: ''
ms.topic: reference
ms.date: 09/13/2018
ms.author: pbutlerm
ms.openlocfilehash: 18f00391beded0744c80eab73bb1efe1c6ab8dbc
ms.sourcegitcommit: 9eaf634d59f7369bec5a2e311806d4a149e9f425
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/05/2018
ms.locfileid: "48810265"
---
<a name="cancel-operation"></a>Anuluj operację 
=================

Ten interfejs API anuluje bieżącą operację w przypadku oferty. Użyj [pobrać operacje interfejsu API](./cloud-partner-portal-api-retrieve-operations.md) można pobrać `operationId` do przekazania do tego interfejsu API. Anulowanie jest zwykle Operacja synchroniczna, jednak w niektórych scenariuszach złożonych nową operację może być konieczne anulowanie istniejącą grupę. W tym przypadku treści odpowiedzi HTTP zawiera lokalizacji operacji, które mają być używane do wykonywania zapytań stanu.

Możesz podać rozdzielana przecinkami lista adresów e-mail z żądaniem, a interfejs API powiadomi te adresy o postępie operacji.

  `POST https://cloudpartner.azure.com/api/publishers/<publisherId>/offers/<offerId>/cancel?api-version=2017-10-31`

<a name="uri-parameters"></a>Parametry identyfikatora URI
--------------

|  **Nazwa**    |      **Opis**                                  |    **Typ danych**  |
| ------------ |     ----------------                                  |     -----------   |
| publisherId  |  Identyfikator wydawcy, na przykład `contoso`         |   Ciąg          |
| identyfikatora oferty      |  Identyfikator oferty                                     |   Ciąg          |
| wersja interfejsu API  |  Bieżąca wersja interfejsu API                               |    Date           |
|  |  |  |


<a name="header"></a>Nagłówek
------

|  **Nazwa**              |  **Wartość**         |
|  ---------             |  ----------        |
|  Content-Type          |  application/json  |
|  Autoryzacja         |  TOKEN YOUR elementu nośnego |
|  |  |


<a name="body-example"></a>Przykład treści
------------

### <a name="request"></a>Żądanie

``` json
{
   "metadata": {
     "notification-emails": "jondoe@contoso.com"
    }
}     
```

### <a name="request-body-properties"></a>Właściwości treści żądania

|  **Nazwa**                |  **Opis**                                               |
|  --------                |  ---------------                                               |
|  powiadomienia e-mail     | Lista identyfikatorów, aby otrzymywać powiadomienia o postępie operację publikowania e-mail rozdzielone przecinkami. |
|  |  |


### <a name="response"></a>Odpowiedź

  `Operation-Location: https://cloudpartner.azure.com/api/publishers/contoso/offers/contoso-virtualmachineoffer/operations/56615b67-2185-49fe-80d2-c4ddf77bb2e8`


### <a name="response-header"></a>Nagłówek odpowiedzi

|  **Nazwa**             |    **Wartość**                       |
|  ---------            |    ----------                      |
| Operacja lokalizacji    | Adres URL, które mogą być przeszukiwane w celu określenia stanu bieżącej operacji. |
|  |  |


### <a name="response-status-codes"></a>Kody stanów odpowiedzi

| **Kod**  |  **Opis**                                                                       |
|  ------   |  ------------------------------------------------------------------------               |
|  200      | Ok. Żądanie zostało pomyślnie przetworzone i operacja została anulowana synchronicznie. |
|  202      | Zaakceptowane. Żądanie zostało pomyślnie przetworzone i operacji jest w trakcie anulowania. Lokalizacja operacja anulowania jest zwracany w nagłówku odpowiedzi. |
|  400      | Żądanie nieprawidłowego/Malformed. Treść odpowiedzi błędu może dostarczyć dodatkowych informacji.  |
|  403      | Dostęp zabroniony. Klient nie ma dostępu do przestrzeni nazw określonej w żądaniu. |
|  404      | Nie znaleziono. Określonej jednostki nie istnieje. |
|  |  |
