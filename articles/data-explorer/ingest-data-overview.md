---
title: Pozyskiwanie danych w usłudze Azure Eksplorator danych
description: Dowiedz się więcej o różnych sposobów umożliwia pobieranie danych (załaduj) w Eksploratorze danych platformy Azure
services: data-explorer
author: orspod
ms.author: v-orspod
ms.reviewer: mblythe
ms.service: data-explorer
ms.topic: conceptual
ms.date: 1/14/2019
ms.openlocfilehash: 8d5fc1c579fd09f1a71d63dce4d1673ef5a8652b
ms.sourcegitcommit: a1cf88246e230c1888b197fdb4514aec6f1a8de2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/16/2019
ms.locfileid: "54354624"
---
# <a name="azure-data-explorer-data-ingestion"></a>Pozyskiwanie danych w usłudze Azure Eksplorator danych

Pozyskiwanie danych polega na używana do ładowania rekordów danych z co najmniej jednego źródła, można utworzyć lub zaktualizować tabeli w Eksploratorze danych platformy Azure. Gdy pozyskiwane, dane będą dostępne dla zapytania. Na poniższym diagramie przedstawiono przepływ end-to-end do pracy w Eksploratorze danych platformy Azure, w tym pozyskiwanie danych.

![Przepływ danych](media/ingest-data-overview/data-flow.png)

Usługa zarządzania danych Eksploratora danych usługi Azure, która jest odpowiedzialna za przetwarzanie danych, oferuje następujące funkcje:

1. **Ściągania danych**: Pobierania danych z zewnętrznych źródeł (usługa Event Hubs) lub liczbę żądań pozyskiwania odczytu z kolejki usługi Azure.

1. **Przetwarzanie wsadowe**: Przepływać do tej samej bazy danych i tabeli w celu zoptymalizowania przepływności pozyskiwania danych partii.

1. **Sprawdzanie poprawności**: Wstępne sprawdzanie poprawności i formatu konwersji w razie potrzeby.

1. **Manipulowanie danymi**: Pasującego schematu, organizowanie, indeksowanie, kodowanie i kompresji danych.

1. **Punkt stanu trwałego w usłudze flow pozyskiwania**: Zarządzanie obciążenia pozyskiwania na aparacie i obsługiwać ponowne próby na przejściowe awarie.

1. **Zatwierdzenie pozyskiwania danych**: Udostępnia dane dla zapytania.

## <a name="ingestion-methods"></a>Metody wprowadzania

Eksplorator danych usługi Azure obsługuje kilka metod wprowadzania, każdy z własną target scenariuszy, zalety i wady. Eksplorator danych usługi Azure oferuje potoków i łączników, aby typowe usługi, wprowadzanie programowe przy użyciu zestawów SDK i bezpośredni dostęp do aparatu do celów eksploracji.

### <a name="ingestion-using-pipelines"></a>Za pomocą potoków pozyskiwania

Eksplorator danych usługi Azure obsługuje obecnie potoku Centrum zdarzeń, które mogą być zarządzane za pomocą Kreatora zarządzania w witrynie Azure portal. Aby uzyskać więcej informacji, zobacz temat [Szybki start: Pozyskiwanie danych z Centrum zdarzeń do Eksploratora danych usługi Azure](ingest-data-event-hub.md).

### <a name="ingestion-using-connectors-and-plugins"></a>Wprowadzanie za pomocą łączników i wtyczek

* Eksplorator danych usługi Azure obsługuje także wtyczkę Logstash. Aby uzyskać więcej informacji, zobacz [Logstash wtyczka danych wyjściowych dla Eksploratora danych usługi Azure](https://github.com/Azure/logstash-output-kusto/blob/master/README.md).

* Eksplorator danych usługi Azure obsługuje łącznika platformy Kafka. Aby uzyskać więcej informacji, zobacz temat [Szybki start: Pozyskiwanie danych z usługi Kafka do Eksploratora danych usługi Azure](ingest-data-kafka.md)

### <a name="programmatic-ingestion"></a>Wprowadzanie programowe

Eksplorator danych usługi Azure udostępnia zestawy SDK, które mogą służyć do kwerendy i danych. Wprowadzanie programowe jest zoptymalizowane pod kątem pozwala zmniejszyć koszty pozyskiwania (KWS), minimalizując transakcje magazynu, podczas i po procesu pozyskiwania.

**Dostępne zestawy SDK i projektów typu open-source**:

Kusto oferuje zestaw SDK, który może służyć do odbierania i wysyłania zapytań dotyczących danych przy użyciu klienta:

* [Zestaw SDK dla języka Python](/azure/kusto/api/python/kusto-python-client-library)

* [Zestaw SDK platformy .NET](/azure/kusto/api/netfx/about-the-sdk)

* [Zestaw SDK Java](/azure/kusto/api/java/kusto-java-client-library)

* [Węzeł zestawu SDK](/azure/kusto/api/node/kusto-node-client-library)

* [Interfejs API REST](/azure/kusto/api/netfx/kusto-ingest-client-rest)

**Wprowadzanie programowe technik**:

* Wprowadzania danych przez usługę zarządzania danych Eksploratora danych usługi Azure (o wysokiej przepływności i niezawodne pozyskiwanie):

    [**Batch pozyskiwania** ](/azure/kusto/api/netfx/kusto-ingest-queued-ingest-sample) (udostępnione przez zestaw SDK): klient przesyła dane do usługi Azure Blob storage (wyznaczony przez usługę zarządzania danych Eksplorator danych platformy Azure) i wysyła powiadomienie do kolejki usługi Azure. Wprowadzanie usługi Batch jest zalecana technika mocno obciążające, niezawodne i tanie pozyskiwania.

* Dane wprowadzane bezpośrednio do aparatu Eksplorator danych platformy Azure (najbardziej odpowiednie do potrzeb eksploracji i tworzenia prototypów):

  * **Wbudowane pozyskiwania**: polecenia sterowania (.ingest wbudowany) zawierający dane wewnątrzpasmowe jest przeznaczony do testowania zapytań ad-hoc.

  * **Pozyskiwanie z kwerendy**: polecenia sterowania (.set, .set lub dołączania, .set lub zastępowanie), który wskazuje na wyniki zapytania jest używana do generowania raportów lub małych tabel tymczasowych.

  * **Pozyskiwanie z magazynu**: polecenia sterowania (.ingest do) za pomocą — dane przechowywane zewnętrznie (na przykład usługi Azure Blob Storage) umożliwia wydajne zbiorcze pozyskiwania danych.

**Opóźnienie różnych metod**:

| Metoda | Opóźnienie |
| --- | --- |
| **Pozyskiwanie wbudowane** | Natychmiast |
| **Pozyskiwanie z zapytania** | Czas wykonywania zapytania i czas przetwarzania |
| **Pozyskiwanie z magazynu** | Czas pobierania i czas przetwarzania |
| **Pozyskiwanie umieszczonych w kolejce** | Przetwarzanie wsadowe, czas i czas przetwarzania |
| |

Czas przetwarzania zależy od rozmiaru danych trwa dłużej niż kilka sekund. Przetwarzanie wsadowe godziny wartość domyślna to 5 minut.

## <a name="choosing-the-most-appropriate-ingestion-method"></a>Wybranie najbardziej odpowiedniej metody wprowadzania

Przed rozpoczęciem pozyskiwania danych, użytkownik powinien samodzielnie na następujące pytania.

* Gdzie ma się moje dane? 
* Co to jest format danych i można je zmienić? 
* Co to są wymagane pola, aby można wykonywać zapytania? 
* Co to jest ilość oczekiwanych danych i prędkości? 
* Ile typy zdarzeń powinny (widoczna jako liczba tabel)? 
* Jak często schematu zdarzeń oczekuje się, aby zmienić? 
* Ilu węzłów wygeneruje dane? 
* Co to jest źródłowego systemu operacyjnego? 
* Jakie są wymagania dotyczące opóźnień? 
* Jedną z istniejących potoków pozyskiwania zarządzanej można używać? 

W przypadku organizacji z istniejącą infrastrukturą, które są oparte na usługą obsługi wiadomości, takich jak Centrum zdarzeń przy użyciu łącznika prawdopodobnie jest najbardziej odpowiednie rozwiązania. Pozyskiwanie umieszczonych w kolejce jest odpowiednia dla dużych ilości danych.

## <a name="supported-data-formats"></a>Obsługiwane formaty danych

Dla wszystkich pozyskiwania metod innych niż pozyskiwać z zapytania, formatu danych tak, aby można go przeanalizować, Eksplorator danych usługi Azure. Formaty obsługiwane dane są:

* CSV, TSV, PSV, SCSV, SOH
* Avro (oddzielone w wierszu, wiele wierszy), JSON
* ZIP i GZIP 

> [!NOTE]
> Gdy dane są pozyskiwane, są wnioskowane typy danych, na podstawie kolumn tabeli docelowej. Jeśli rekord jest niekompletne lub pola nie może być analizowana jako typ danych, odpowiednie kolumny tabeli zostaną wypełnione przy użyciu wartości null.

## <a name="ingestion-recommendations-and-limitations"></a>Zalecenia dotyczące pozyskiwania i ograniczenia

* Zasady przechowywania skuteczne pozyskiwanych danych jest tworzony na podstawie zasad przechowywania bazy danych. Zobacz [zasady przechowywania](/azure/kusto/concepts/retentionpolicy) Aby uzyskać szczegółowe informacje. Dane wprowadzane wymaga **pozwalająca tabeli** lub **dużych możliwościach skalowania bazy danych** uprawnienia.
* Pozyskiwanie obsługuje maksymalny rozmiar pliku wynoszący 5 GB. Zaleca się pozyskiwać pliki między 100 MB i 1 GB.

## <a name="schema-mapping"></a>mapowanie schematu

Mapowanie schematu pozwala powiązać pola danych źródła kolumny tabeli docelowej.

* [Mapowanie CSV](/azure/kusto/management/mappings?branch=master#csv-mapping) (opcjonalnie) współpracuje z wszystkie formaty oparte na numer. Mogą być wykonywane za pomocą parametru polecenia pozyskiwania lub [wstępnie utworzone w tabeli](/azure/kusto/management/tables?branch=master#create-ingestion-mapping) i do którego istnieje odwołanie parametru polecenia pozyskiwania.
* [Mapowanie JSON](/azure/kusto/management/mappings?branch=master#json-mapping) (obowiązkowe) i [mapowania Avro](/azure/kusto/management/mappings?branch=master#avro-mapping) (obowiązkowe) mogą być wykonywane za pomocą parametru polecenia pozyskiwania lub [wstępnie utworzone w tabeli](/azure/kusto/management/tables#create-ingestion-mapping) i polecenia pozyskiwania parametr.

## <a name="next-steps"></a>Kolejne kroki

> [!div class="nextstepaction"]
> [Szybki start: Pozyskiwanie danych z Centrum zdarzeń do Eksploratora danych usługi Azure](ingest-data-event-hub.md)

> [!div class="nextstepaction"]
> [Szybki start: Pozyskiwanie danych z usługi Kafka do Eksploratora danych usługi Azure](ingest-data-kafka.md)

> [!div class="nextstepaction"]
> [Szybki start: pozyskiwanie danych przy użyciu biblioteki języka Python w usłudze Azure Data Explorer](python-ingest-data.md)

> [!div class="nextstepaction"]
> [Szybki start: Pozyskiwanie danych przy użyciu biblioteki węzeł Eksploratora danych platformy Azure](node-ingest-data.md)

> [!div class="nextstepaction"]
> [Szybki start: Pozyskiwanie danych przy użyciu usługi Azure Data Explorer zestaw .NET Standard SDK (wersja zapoznawcza)](net-standard-ingest-data.md)
