---
title: Biblioteki połączeń dla usługi SQL Database | Dokumentacja firmy Microsoft
description: Zawiera łącza do pobierania modułów, które umożliwiają połączenie z SQL Server i bazy danych SQL z szerokiej gamy klientów, w językach programowania.
services: sql-database
ms.service: sql-database
ms.subservice: development
ms.custom: ''
ms.devlang: ''
ms.topic: conceptual
author: MightyPen
ms.author: genemi
ms.reviewer: ''
manager: craigg
ms.date: 01/03/2019
ms.openlocfilehash: 874aa2610ae1785e9f40841ed3c3279aac42d660
ms.sourcegitcommit: 3ba9bb78e35c3c3c3c8991b64282f5001fd0a67b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/15/2019
ms.locfileid: "54321827"
---
# <a name="connectivity-libraries-and-frameworks-for-sql-server"></a>Biblioteki łączności i platformy dla programu SQL Server

Zapoznaj się z naszym [Pobierz samouczki dla początkujących](https://aka.ms/sqldev) szybko rozpocząć pracę przy programowaniu języków, takich jak C#, Java, Node.js, PHP i Python. Następnie utwórz aplikację przy użyciu programu SQL Server w systemie Linux lub Windows lub platformy Docker w systemie macOS.

Poniższa tabela zawiera listę bibliotek łączności lub *sterowniki* że aplikacje klienckie mogą używać różnych języków, aby połączyć się i używać programu SQL Server działającego lokalnie lub w chmurze. Można ich używać w systemie Linux, Windows lub platformy Docker i ich używać do nawiązania połączenia usługi Azure SQL Database i Azure SQL Data Warehouse. 

| Język | Platforma | Dodatkowe zasoby | Do pobrania | Rozpoczęcie pracy |
| :-- | :-- | :-- | :-- | :-- |
| C# | Windows, Linux, macOS | [Microsoft ADO.NET dla programu SQL Server](https://docs.microsoft.com/sql/connect/ado-net/microsoft-ado-net-for-sql-server) | [Pobieranie](https://www.microsoft.com/net/download/) | [Wprowadzenie](https://www.microsoft.com/sql-server/developer-get-started/csharp/ubuntu)
| Java | Windows, Linux, macOS | [Sterownik JDBC firmy Microsoft dla programu SQL Server](https://msdn.microsoft.com/library/mt484311.aspx) | [Pobieranie](https://go.microsoft.com/fwlink/?linkid=852460) |  [Wprowadzenie](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu)
| PHP | Windows, Linux, macOS| [Sterownik PHP SQL dla programu SQL Server](https://docs.microsoft.com/sql/connect/php/microsoft-php-driver-for-sql-server) | [Pobieranie](https://docs.microsoft.com/sql/connect/php/download-drivers-php-sql-server) | [Wprowadzenie](https://www.microsoft.com/sql-server/developer-get-started/php/ubuntu/)
| Node.js | Windows, Linux, macOS | [Sterownik node.js dla programu SQL Server](https://msdn.microsoft.com/library/mt652093.aspx) | [Instalowanie](https://msdn.microsoft.com/library/mt652094.aspx) |  [Wprowadzenie](https://www.microsoft.com/sql-server/developer-get-started/node/ubuntu)
| Python | Windows, Linux, macOS | [Sterownik SQL języka Python](https://msdn.microsoft.com/library/mt652092.aspx) | Zainstaluj opcje: <br/> \* [pymssql](https://msdn.microsoft.com/library/mt694094.aspx) <br/> \* [pyodbc](https://msdn.microsoft.com/library/mt763257.aspx) |  [Wprowadzenie](https://www.microsoft.com/sql-server/developer-get-started/python/ubuntu)
| Ruby | Windows, Linux, macOS | [Sterownik języka Ruby dla programu SQL Server](https://msdn.microsoft.com/library/mt691981.aspx) | [Instalowanie](https://msdn.microsoft.com/library/mt711041.aspx) | [Wprowadzenie](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu)
| C++ | Windows, Linux, macOS | [Sterownik ODBC firmy Microsoft dla programu SQL Server](https://msdn.microsoft.com/library/mt654048(v=sql.1).aspx) | [Pobieranie](https://msdn.microsoft.com/library/mt654048(v=sql.1).aspx) |  

W poniższej tabeli wymieniono przykłady struktur mapowania obiektowo relacyjny (ORM) i struktury sieci web, które aplikacje klienckie mogą używać z programem SQL Server działającego lokalnie lub w chmurze. Można używać struktur w systemie Linux, Windows lub platformy Docker i ich używać do nawiązania połączenia bazy danych SQL Database i SQL Data Warehouse. 

| Język | Platforma | ORM(s) |
| :-- | :-- | :-- |
| C# | Windows, Linux, macOS | [Entity Framework](https://docs.microsoft.com/ef)<br>[Entity Framework Core](https://docs.microsoft.com/ef/core/index) |
| Java | Windows, Linux, macOS |[Hibernacji ORM](https://hibernate.org/orm)|
| PHP | Windows, Linux, macOS | [Platforma Laravel (Eloquent)](https://laravel.com/docs/5.0/eloquent) |
| Node.js | Windows, Linux, macOS | [Sequelize ORM](https://docs.sequelizejs.com) |
| Python | Windows, Linux, macOS |[Django](https://www.djangoproject.com/) |
| Ruby | Windows, Linux, macOS | [Ruby on Rails](https://rubyonrails.org/) |
||||

## <a name="related-links"></a>Powiązane linki
- [Sterowniki programu SQL Server](https://msdn.microsoft.com/library/mt654049.aspx) służące do łączenia z aplikacji klienckich
- Połącz z bazą danych SQL:
    - [Nawiązywanie połączenia z bazą danych SQL Database przy użyciu platformy .NET (C#)](sql-database-connect-query-dotnet.md)
    - [Nawiązywanie połączenia z bazą danych SQL Database przy użyciu języka PHP](sql-database-connect-query-php.md)
    - [Nawiązywanie połączenia z bazą danych SQL Database przy użyciu języka Node.js](sql-database-connect-query-nodejs.md)
    - [Nawiązywanie połączenia z bazą danych SQL Database przy użyciu platformy Java](sql-database-connect-query-java.md)
    - [Nawiązywanie połączenia z bazą danych SQL Database przy użyciu języka Python](sql-database-connect-query-python.md)
    - [Nawiązywanie połączenia z bazą danych SQL Database przy użyciu języka Ruby](sql-database-connect-query-ruby.md)
- Ponów próbę logiki przykłady kodu:
    - [Nawiązywanie połączeń odpornych do bazy danych SQL za pomocą narzędzia ADO.NET][step-4-connect-resiliently-to-sql-with-ado-net-a78n]
    - [Nawiązywanie połączeń odpornych do bazy danych SQL za pomocą języka PHP][step-4-connect-resiliently-to-sql-with-php-p42h]


<!-- Link references. -->

[step-4-connect-resiliently-to-sql-with-ado-net-a78n]: https://docs.microsoft.com/sql/connect/ado-net/step-4-connect-resiliently-to-sql-with-ado-net

[step-4-connect-resiliently-to-sql-with-php-p42h]: https://docs.microsoft.com/sql/connect/php/step-4-connect-resiliently-to-sql-with-php

