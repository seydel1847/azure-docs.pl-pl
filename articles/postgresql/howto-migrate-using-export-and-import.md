---
title: Migrowanie bazy danych za pomocą importowania i eksportowania w usłudze Azure Database for PostgreSQL
description: W tym artykule opisano sposób wyodrębniania bazę danych PostgreSQL do pliku skryptu i importowania danych do docelowej bazy danych z tego pliku.
author: rachel-msft
ms.author: raagyema
ms.service: postgresql
ms.topic: conceptual
ms.date: 06/01/2018
ms.openlocfilehash: ecd7dc225379fc9d3eda6fb2e80e3c47a73db49b
ms.sourcegitcommit: 71ee622bdba6e24db4d7ce92107b1ef1a4fa2600
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/17/2018
ms.locfileid: "53547630"
---
# <a name="migrate-your-postgresql-database-using-export-and-import"></a>Migracja bazy danych postgresql w warstwie użycie opcji eksportowania i importowania
Możesz użyć [pg_dump](https://www.postgresql.org/docs/9.3/static/app-pgdump.html) można wyodrębnić bazy danych PostgreSQL w pliku skryptu i [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) do importowania danych do docelowej bazy danych z tego pliku.

## <a name="prerequisites"></a>Wymagania wstępne
Do wykonania kroków w tym przewodniku, potrzebne są:
- [— Azure Database for postgresql w warstwie serwera](quickstart-create-server-database-portal.md) za pomocą reguł zapory, aby zezwolić na dostęp i bazy danych w nim.
- [pg_dump](https://www.postgresql.org/docs/9.6/static/app-pgdump.html) zainstalowane narzędzie wiersza polecenia
- [wersja narzędzia psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) zainstalowane narzędzie wiersza polecenia

Wykonaj następujące kroki, aby wyeksportować i zaimportować bazę danych PostgreSQL.

## <a name="create-a-script-file-using-pgdump-that-contains-the-data-to-be-loaded"></a>Tworzenie pliku skryptu za pomocą pg_dump, która zawiera dane do załadowania
Aby wyeksportować istniejący postgresql w warstwie bazy danych lokalnego lub na maszynie wirtualnej do pliku skryptu sql uruchom następujące polecenie w istniejącym środowiskiem:
```bash
pg_dump –-host=<host> --username=<name> --dbname=<database name> --file=<database>.sql
```
Na przykład w przypadku lokalnego serwera i bazy danych o nazwie **testdb** w nim:
```bash
pg_dump --host=localhost --username=masterlogin --dbname=testdb --file=testdb.sql
```

## <a name="import-the-data-on-target-azure-database-for-postgresql"></a>Importowanie danych w elemencie docelowym — Azure Database for PostgreSQL
Można użyć wiersza polecenia psql, a parametr--dbname (-d) aby importować dane do usługi Azure Database for postgresql w warstwie serwera i ładowanie danych z pliku sql.
```bash
psql --file=<database>.sql --host=<server name> --port=5432 --username=<user@servername> --dbname=<target database name>
```
W tym przykładzie użyto narzędzie psql oraz pliku skryptu o nazwie **testdb.sql** z poprzedniego kroku, aby zaimportować dane do bazy danych **mypgsqldb** na serwerze docelowym  **mydemoserver.postgres.Database.Azure.com**.
```bash
psql --file=testdb.sql --host=mydemoserver.database.windows.net --port=5432 --username=mylogin@mydemoserver --dbname=mypgsqldb
```

## <a name="next-steps"></a>Kolejne kroki
- Aby przeprowadzić migrację bazy danych PostgreSQL za pomocą zrzutu i przywracania, zobacz [Migrowanie przy użyciu zrzutu i przywracania bazy danych postgresql w warstwie](howto-migrate-using-dump-and-restore.md).
- Aby uzyskać więcej informacji na temat migrowania baz danych do usługi Azure Database for PostgreSQL, zobacz [Przewodnik po migracji bazy danych](https://aka.ms/datamigration). 
