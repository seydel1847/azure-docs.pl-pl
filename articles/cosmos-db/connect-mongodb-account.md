---
title: Łączenie aplikacji bazy danych MongoDB w usłudze Azure Cosmos DB
description: Dowiedz się, jak połączyć aplikację bazy danych MongoDB do usługi Azure Cosmos DB.
author: rimman
ms.service: cosmos-db
ms.subservice: cosmosdb-mongo
ms.topic: conceptual
ms.date: 12/26/2018
ms.author: rimman
ms.reviewer: sngun
ms.openlocfilehash: 737e179c2c16937d00bc9b6601f12ebe392c1906
ms.sourcegitcommit: 8330a262abaddaafd4acb04016b68486fba5835b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/04/2019
ms.locfileid: "54040323"
---
# <a name="connect-a-mongodb-application-to-azure-cosmos-db"></a>Łączenie aplikacji bazy danych MongoDB w usłudze Azure Cosmos DB
Dowiedz się, jak połączyć aplikację bazy danych MongoDB do usługi Azure Cosmos DB przy użyciu parametrów połączenia MongoDB. Bazę danych usługi Azure Cosmos DB można następnie użyć jako danych magazynu dla aplikacji MongoDB. 

Ten samouczek zawiera dwa sposoby, aby pobrać informacje o parametrach połączenia:

- [Metoda szybkiego startu](#QuickstartConnection), do użytku z programem .NET, Node.js, powłoki bazy danych MongoDB, Java i Python sterowników
- [Metoda ciąg połączenia niestandardowego](#GetCustomConnection), do użytku z innych sterowników

## <a name="prerequisites"></a>Wymagania wstępne

- Konto platformy Azure. Jeśli nie masz konta platformy Azure, Utwórz [bezpłatne konto platformy Azure](https://azure.microsoft.com/free/) teraz. 
- Konta usługi Cosmos. Aby uzyskać instrukcje, zobacz [tworzenie aplikacji internetowej przy użyciu interfejsu API usługi Azure Cosmos DB dla bazy danych MongoDB i zestawu SDK platformy .NET](create-mongodb-dotnet.md).

## <a id="QuickstartConnection"></a>Pobieranie parametrów połączenia bazy danych MongoDB przy użyciu szybkiego startu
1. W przeglądarce internetowej, zaloguj się do [witryny Azure portal](https://portal.azure.com).
2. W **usługi Azure Cosmos DB** bloku wybierz interfejs API. 
3. W okienku po lewej stronie bloku konta kliknij **— szybki start**. 
4. Wybierz platformę (**.NET**, **Node.js**, **powłoka MongoDB**, **Java**, **Python**). Jeśli nie widzisz, sterownik lub narzędzie na liście, nie martw się — stale dokumentujemy kolejne fragmentu kodu połączenia. Skomentuj poniżej na chcesz zobaczyć. Aby dowiedzieć się, jak tworzyć własne połączenia, przeczytaj [uzyskać informacje o parametrach połączenia dla konta](#GetCustomConnection).
5. Skopiuj i Wklej fragment kodu w aplikacji bazy danych MongoDB.

    ![Bloku szybki start](./media/connect-mongodb-account/QuickStartBlade.png)

## <a id="GetCustomConnection"></a> Pobieranie parametrów połączenia bazy danych MongoDB do dostosowywania
1. W przeglądarce internetowej, zaloguj się do [witryny Azure portal](https://portal.azure.com).
2. W **usługi Azure Cosmos DB** bloku wybierz interfejs API. 
3. W okienku po lewej stronie bloku konta kliknij **parametry połączenia**. 
4. **Parametry połączenia** zostanie otwarty blok. Ma on wszystkie informacje niezbędne do połączenia do konta za pośrednictwem sterownika dla bazy danych MongoDB, w tym ciągu połączenia preconstructed.

    ![Blok Parametry połączenia](./media/connect-mongodb-account/ConnectionStringBlade.png)

## <a name="connection-string-requirements"></a>Wymagania dotyczące parametrów połączenia
> [!Important]
> usługa Azure Cosmos DB ma ścisłe wymagania i standardy dotyczące bezpieczeństwa. Konta usługi Azure Cosmos DB wymaga uwierzytelniania i bezpiecznej komunikacji za pośrednictwem *SSL*. 
>
>

Usługa Azure Cosmos DB obsługuje standardowe bazy danych MongoDB format ciągu połączenia identyfikatora URI, przy użyciu kilku określonych wymagań: Konta usługi Azure Cosmos DB wymaga uwierzytelniania i bezpiecznej komunikacji SSL. Dlatego jest format parametrów połączenia:

    mongodb://username:password@host:port/[database]?ssl=true

Wartości tych parametrów są dostępne w **parametry połączenia** bloku przedstawionej wcześniej:

* Nazwa użytkownika (wymagane): Nazwa konta usługi cosmos.
* Hasło (wymagane): Hasło konta cosmos.
* Host (wymagane): Nazwa FQDN konto usługi Cosmos.
* Port (wymagane): 10255.
* Baza danych (opcjonalnie): Baza danych korzysta z połączenia. Jeśli żadna baza danych zostanie podany, domyślna baza danych jest "test".
* Protokół SSL = true (wymagane)

Rozważmy na przykład konta pokazanego na **parametry połączenia** bloku. Jest prawidłowe parametry połączenia:

    mongodb://contoso123:0Fc3IolnL12312asdfawejunASDF@asdfYXX2t8a97kghVcUzcDv98hawelufhawefafnoQRGwNj2nMPL1Y9qsIr9Srdw==@contoso123.documents.azure.com:10255/mydatabase?ssl=true

## <a name="next-steps"></a>Kolejne kroki

- Dowiedz się, jak [korzystać z programu Studio 3T](mongodb-mongochef.md) przy użyciu interfejsu API usługi Azure Cosmos DB, bazy danych mongodb.
- Dowiedz się, jak [korzystać z programu 3T Robo](mongodb-robomongo.md) przy użyciu interfejsu API usługi Azure Cosmos DB, bazy danych mongodb.
- Zapoznaj się z bazą danych MongoDB [przykłady](mongodb-samples.md) przy użyciu interfejsu API usługi Azure Cosmos DB, bazy danych mongodb.
