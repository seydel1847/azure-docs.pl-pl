---
title: Ustawianie uprawnień dla usługi Data Lake Storage Gen2 za pomocą Eksploratora usługi Azure Storage
description: Z tego artykułu z instrukcjami dowiesz się, jak za pomocą Eksploratora usługi Azure Storage skonfigurować uprawnienia do plików i katalogów na koncie magazynu obsługującego usługę Azure Data Lake Storage Gen2 (wersja zapoznawcza).
services: storage
author: roygara
ms.custom: mvc
ms.component: data-lake-storage-gen2
ms.service: storage
ms.topic: quickstart
ms.date: 12/11/2018
ms.author: rogarana
ms.openlocfilehash: 1b89553816b6ff8a8076d954274d8404f49154a6
ms.sourcegitcommit: 85d94b423518ee7ec7f071f4f256f84c64039a9d
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2018
ms.locfileid: "53384857"
---
# <a name="set-file-and-directory-level-permissions-using-azure-storage-explorer-with-azure-data-lake-storage-gen2-preview"></a>Ustawianie uprawnień na poziomie plików i katalogów przy użyciu Eksploratora usługi Azure Storage w usłudze Azure Data Lake Storage Gen2 (wersja zapoznawcza)

Pliki przechowywane w usłudze Azure Data Lake Storage Gen2 (wersja zapoznawcza) obsługują uprawnienia szczegółowe i zarządzanie listą kontroli dostępu (ACL). Uprawnienia szczegółowe w połączeniu z zarządzaniem listą ACL umożliwiają zarządzanie dostępem do danych na bardzo szczegółowym poziomie.

Ten artykuł zawiera informacje dotyczące wykonywania następujących czynności za pomocą Eksploratora usługi Azure Storage:

> [!div class="checklist"]
> * Ustawianie uprawnień na poziomie pliku
> * Ustawianie uprawnień na poziomie katalogu
> * Dodawanie użytkowników lub grup do listy kontroli dostępu

## <a name="prerequisites"></a>Wymagania wstępne

Aby jak najlepiej przedstawić ten proces, wymagane jest ukończenie [przewodnika Szybki start dotyczącego Eksploratora usługi Azure Storage](data-lake-storage-Explorer.md). Dzięki temu konto magazynu będzie miało najbardziej odpowiedni stan (utworzony system plików z przekazanymi danymi).

## <a name="managing-access"></a>Zarządzanie dostępem

Uprawnienia można ustawić w katalogu głównym systemu plików. Aby to zrobić, kliknij prawym przyciskiem myszy system plików i wybierz pozycję **Zarządzaj uprawnieniami**, aby wyświetlić okno dialogowe **Zarządzanie uprawnieniami**.

![Eksplorator usługi Microsoft Azure Storage — zarządzanie dostępem do katalogów](media/storage-quickstart-blobs-storage-Explorer/manageperms.png)

Okno dialogowe **Zarządzanie uprawnieniami** służy do zarządzania uprawnieniami właściciela i grupy właściciela. Umożliwia również dodawanie do listy kontroli dostępu nowych użytkowników i grup, dla których można następnie zarządzać uprawnieniami.

Aby dodać do listy kontroli dostępu nowego użytkownika lub nową grupę, wybierz pole **Dodaj użytkownika lub grupę**.

Wprowadź odpowiedni wpis usługi Azure Active Directory (AAD), który chcesz dodać do listy, a następnie wybierz pozycję **Dodaj**.

Użytkownika lub grupę będzie teraz widać w polu **Użytkownicy i grupy:**, co umożliwi rozpoczęcie zarządzania ich uprawnieniami.

> [!NOTE]
> Najlepsze rozwiązanie i zalecenie jest takie, aby utworzyć grupę zabezpieczeń w usłudze AAD i obsługiwać uprawnienia dla grupy, a nie dla poszczególnych użytkowników. Szczegółowe informacje na temat tego zalecenia oraz inne najlepsze rozwiązania można znaleźć w [najlepszych rozwiązaniach dotyczących usługi Data Lake Storage Gen2](data-lake-storage-best-practices.md).

Istnieją dwie kategorie uprawnień, które można przypisać: listy ACL dostępu i domyślne listy ACL.

* **Dostęp**: Listy ACL dostępu kontrolują dostęp do obiektu. Pliki i katalogi mają osobne listy ACL dostępu.

* **Domyślne**: Szablon list ACL skojarzonych z katalogiem, który określa listy ACL dostępu dla wszystkich elementów podrzędnych, które zostały utworzone w tym katalogu. Pliki nie mają domyślnych list ACL.

Obie te kategorie obejmują trzy uprawnienia, które można przypisać do plików lub katalogów: **Odczyt**, **Zapis** i **Wykonywanie**.

>[!NOTE]
> Dokonanie wyboru w tym miejscu nie spowoduje ustawienie uprawnień dla wszystkich elementów znajdujących się obecnie w katalogu. Jeśli dany plik już istnieje, należy przejść do poszczególnych elementów i ustawić uprawnienia ręcznie.

Można zarządzać uprawnieniami dla poszczególnych katalogów, a także dla pojedynczych plików, co umożliwia szczegółową kontrolę dostępu. Proces zarządzania uprawnieniami dla plików i katalogów jest taki sam, jak opisano powyżej. Kliknij prawym przyciskiem myszy plik lub katalog, dla którego chcesz zarządzać uprawnieniami, i wykonaj ten sam proces.

## <a name="next-steps"></a>Następne kroki

W tym artykule z instrukcjami przedstawiono sposób ustawiania uprawnień dla plików i katalogów przy użyciu **Eksploratora usługi Azure Storage**. Aby dowiedzieć się więcej o listach ACL, w tym o domyślnych listach ACL, listach ACL dostępu i odpowiadających im uprawnieniach, przejdź do naszego koncepcyjnego artykułu na ten temat.

> [!div class="nextstepaction"]
> [Kontrola dostępu w usłudze Azure Data Lake Storage Gen2](data-lake-storage-access-control.md)