---
title: Sterowniki MySQL i zgodność z narzędziami narzędzia do zarządzania
description: W tym artykule opisano MySQL sterowników i narzędzi do zarządzania, które są zgodne z usługą Azure Database for MySQL.
author: ajlam
ms.author: andrela
ms.service: mysql
ms.topic: conceptual
ms.date: 11/21/2018
ms.openlocfilehash: 7bb5f861676517d709f59c1bf50d77c4d9cc49a4
ms.sourcegitcommit: 71ee622bdba6e24db4d7ce92107b1ef1a4fa2600
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/17/2018
ms.locfileid: "53548055"
---
# <a name="mysql-drivers-and-management-tools-compatible-with-azure-database-for-mysql"></a>MySQL sterowników i narzędzi do zarządzania zgodne z usługą Azure Database for MySQL
W tym artykule opisano, sterowników i narzędzi do zarządzania, które są zgodne z usługą Azure Database for MySQL.

## <a name="mysql-drivers"></a>Sterowniki MySQL
Usługa Azure Database for MySQL — używa najpopularniejszych wersji community na świecie bazy danych MySQL. Dlatego jest zgodny z szerokiej gamy języków i sterowniki programowania. Celem jest zapewnienie pomocy technicznej trzy najnowsze wersje sterowników MySQL i kontynuować wysiłków autorów ze społeczności "open source" w celu stale funkcjonalność i użyteczność sterowniki MySQL. Lista sterowników, które zostały sprawdzone i ocenione jako zgodne z usługą Azure Database for MySQL 5.6 i 5.7 znajduje się w poniższej tabeli:

| **Sterownik** | **Łącza** | **Zgodne wersje** | **Niezgodne wersje** | **Uwagi** |
| :-------- | :------------------------ | :----------- | :---------------------- | :--------------------------------------- |
| PHP | https://secure.php.net/downloads.php | 5.5, 5.6, 7.x | 5.3 | Środowisko PHP 7.0 połączenia z MySQLi protokołu SSL należy dodać MYSQLI_CLIENT_SSL_DONT_VERIFY_SERVER_CERT w parametrach połączenia. <br> ```mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306, NULL, MYSQLI_CLIENT_SSL_DONT_VERIFY_SERVER_CERT);```<br> Zestaw PDO: ```PDO::MYSQL_ATTR_SSL_VERIFY_SERVER_CERT``` opcji na wartość false.|
| .Net | [MySqlConnector w witrynie GitHub](https://github.com/mysql-net/MySqlConnector) <br> [Instalacja pakietu Nuget](https://www.nuget.org/packages/MySqlConnector/) | 0.27 oraz po | 0.26.5 i przed | |
| MySQL Connector/NET | [MySQL Connector/NET](https://github.com/mysql/mysql-connector-net) | 8.0, 7.0, 6.10 |  | Kodowanie błędów może spowodować połączeń w niektórych systemach Windows bez UTF8. |
| Nodejs |  [MySQLjs w witrynie GitHub](https://github.com/mysqljs/mysql/) <br> Pakiet instalacyjny z poziomu narzędzia NPM:<br> Uruchom `npm install mysql` z poziomu narzędzia NPM | 2.15 | 2.14.1 i przed | |
| PRZEJDŹ | https://github.com/go-sql-driver/mysql/releases | 1.3 | 1.2 i przed | Użyj allowNativePasswords = true w parametrach połączenia |
| Python | https://pypi.python.org/pypi/mysql-connector-python | 1.2.3, 2.0, 2.1, 2.2 | 1.2.2 i przed | |
| Java | https://downloads.mariadb.org/connector-java/ | 2.1, w wersji 2.0 w wersji 1.6 | 1.5.5 i przed | |

## <a name="management-tools"></a>Narzędzia do zarządzania
Zaletą zgodności obejmuje również narzędzia do zarządzania bazą danych. Istniejącymi narzędziami powinny nadal działać z usługą Azure Database for MySQL, tak długo, jak Manipulowanie bazą danych działa w granicach uprawnień użytkownika. Trzy wspólnej bazy danych narzędzi do zarządzania, które zostały sprawdzone i ocenione jako zgodne z usługą Azure Database for MySQL 5.6 i 5.7 są wymienione w poniższej tabeli:

|                                     | **Aplikację MySQL Workbench 6.x i nowsze** | **Navicat 12** | **Narzędzia PHPMyAdmin 4.x i nowsze** |
| :---------------------------------- | :----------------------------- | :------------- | :-------------------------|
| Create, Update, Read, Write, Delete | X | X | X |
| Połączenia SSL | X | X | X |
| Okno Autouzupełnianie zapytań SQL | X | X |  |
| Importowanie i eksportowanie danych | X | X | X |
| Eksportowanie do wielu formatów | X | X | X |
| Wykonywanie kopii zapasowych i przywracanie |  | X |  |
| Wyświetl parametry serwera | X | X | X |
| Wyświetlanie połączeń klienta | X | X | X |
