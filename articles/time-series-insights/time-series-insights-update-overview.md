---
title: 'Omówienie: usługa Azure Time Series Insights w wersji zapoznawczej | Microsoft Docs'
description: Omówienie usługi Azure Time Series Insights w wersji zapoznawczej
ms.service: time-series-insights
services: time-series-insights
author: ashannon7
ms.author: anshan
manager: cshankar
ms.reviewer: anshan
ms.workload: big-data
ms.topic: overview
ms.date: 12/05/2018
ms.custom: seodec18
ms.openlocfilehash: 847eddc78f8abc938e68e6fe383a773dadeaf779
ms.sourcegitcommit: b767a6a118bca386ac6de93ea38f1cc457bb3e4e
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/18/2018
ms.locfileid: "53557839"
---
# <a name="azure-time-series-insights-preview-overview"></a>Omówienie usługi Azure Time Series Insights w wersji zapoznawczej

Usługa Azure Time Series Insights w wersji zapoznawczej to kompleksowa oferta platformy jako usługi. Służy do pozyskiwania, przetwarzania i magazynowania wysoce skontekstualizowanych, zoptymalizowanych pod kątem szeregów czasowych danych środowiska IoT i wykonywania dotyczących ich zapytań. Usługa Time Series Insights idealnie nadaje się do eksplorowania danych ad hoc oraz do analizy operacyjnej. Usługa Time Series Insights to unikatowo rozszerzalna i niestandardowa oferta, która spełnia szeroki zakres potrzeb związanych z przemysłowymi wdrożeniami IoT.

## <a name="video"></a>Połączenia wideo

W tym wideo omawiamy usługę Azure Time Series Insights w wersji zapoznawczej — platformę do analizy IoT w chmurze.

> [!VIDEO https://channel9.msdn.com/Shows/Internet-of-Things-Show/Azure-Time-Series-Insights-e2e-solution-for-industrial-IoT-analytics/player]

## <a name="define-iot-data"></a>Definiowanie danych IoT

Dane IoT to każde dane „przemysłowe” dostępne w organizacjach intensywnie korzystających z zasobów. Dane IoT są często danymi bez struktury, ponieważ są wysyłane z zasobów służących do rejestrowania znacznej liczby wartości pomiarów. Te pomiary mogą dotyczyć np. temperatury, ruchu lub wilgotności. Te strumienie danych często charakteryzują się znacznymi lukami, uszkodzonymi komunikatami i fałszywymi odczytami. Dane z tych strumieni należy oczyścić, zanim będzie można przeprowadzić na nich jakąkolwiek analizę. Dane IoT często mają znaczenie tylko w kontekście dodatkowych danych pochodzących z własnych (np. systemy CRM i ERP) lub zewnętrznych źródeł danych (np. pogoda lub lokalizacja).

W związku z tym tylko część tych danych jest wykorzystywana do celów operacyjnych i biznesowych. Takie dane zapewniają spójne, kompleksowe, bieżące i prawidłowe informacje na potrzeby raportów i analiz biznesowych. Przekształcanie zbieranych danych IoT na szczegółowe informacje umożliwiające podejmowanie działań wymaga następujących elementów:

* przetwarzanie danych w celu oczyszczenia, przefiltrowania, interpolacji, przekształcenia i przygotowania danych do analizy;
* struktura do nawigowania po danych i ich interpretacji (czyli do normalizacji i ustalenia kontekstu danych);
* ekonomiczny magazyn do długoterminowego lub nieskończonego przechowywania przetworzonych lub uzyskanych danych lub nieprzetworzonych danych z kilkudziesięciu lat.

Na poniższej ilustracji przedstawiono typowy przepływ danych IoT.

  ![Przepływ danych IoT][1]

## <a name="azure-time-series-insights-for-industrial-iot"></a>Usługa Azure Time Series Insights dla przemysłowego Internetu rzeczy

Obecny krajobraz Internetu rzeczy jest zróżnicowany. Obejmuje on klientów z branży produkcyjnej, motoryzacyjnej, energetycznej, usług komunalnych, inteligentnego budownictwa i konsultingowej. Scenariusze obejmują eksplorację danych ad hoc, gdzie forma danych jest nieznana. Mogą dotyczyć również analizy operacyjnej danych objętych schematem lub jawnie modelowanych w celu zwiększenia wydajności operacyjnej. Te scenariusze na ogół istnieją obok siebie i obsługują różne przypadki użycia. Kluczowe znaczenie dla sukcesu przedsiębiorstw korzystających z przemysłowego IoT i ich rewolucji cyfrowej mają następujące możliwości platformy:

- wielowarstwowy magazyn (ciepły i zimny), 
- możliwość przechowywania serii danych z kilkudziesięciu lat, 
- możliwość jawnego modelowania i optymalizowania zapytań dotyczących analiz operacyjnych opartych na zasobach.

Usługa Time Series Insights jest kompleksową ofertą platformy jako usługi, która spełnia wymagania dotyczące eksplorowania danych IoT i uzyskiwania szczegółowych informacji operacyjnych. Usługa Time Series Insights oferuje w pełni zarządzaną usługę w chmurze do analizowania danych szeregów czasowych w skali IoT.

Nieprzetworzone dane można przechowywać w magazynie bez schematu w pamięci. Następnie można wykonywać interaktywne zapytania ad-hoc za pomocą aparatu zapytań rozproszonych i interfejsu API. Można korzystać z zaawansowanego środowiska obsługi użytkownika w celu wizualizacji miliardów zdarzeń w ciągu kilku sekund. Dowiedz się więcej o [funkcjach eksplorowania danych](./time-series-insights-overview.md).

Usługa Time Series Insights oferuje również funkcje dotyczące szczegółowych informacji operacyjnych, obecnie w wersji zapoznawczej. W połączeniu z interaktywnym eksplorowaniem danych i analizą operacyjną usługa Time Series Insights umożliwia uzyskanie większej wartości z danych zgromadzonych z zasobów IoT. Oferta wersji zapoznawczej zapewnia następujące składniki:

* Skalowalny magazyn danych szeregów czasowych zoptymalizowany pod kątem wydajności i kosztów. To rozwiązanie IoT oparte na chmurze umożliwia określenie w ciągu kilku sekund trendów danych szeregów czasowych z wielu lat.
* Obsługa modelu semantycznego w celu opisania domeny i metadanych skojarzonych z pochodnymi i niepochodnymi sygnałami z zasobów i urządzeń.
* Ulepszone środowisko obsługi użytkownika, które łączy szczegółowe informacje o danych oparte na zasobach z rozbudowanymi funkcjami analizy danych ad-hoc. To połączenie umożliwia przeprowadzanie analiz biznesowych i operacyjnych.
* Integracja z zaawansowanymi narzędziami do uczenia maszynowego i analizy. Są to m.in. Azure Databricks, Apache Spark, Azure Machine Learning, notesy programu Jupyter i usługa Power BI. Te narzędzia ułatwiają wykonywanie zadań związanych z danymi szeregów czasowych i zwiększanie wydajności operacyjnej.

Funkcje dotyczące szczegółowych informacji operacyjnych i eksplorowania danych są oferowane razem w prostym modelu płatności zgodnie z rzeczywistym użyciem na potrzeby przetwarzania danych, magazynowania i wysyłania zapytań. Ten model rozliczeń jest dostosowany do zmieniających się potrzeb biznesowych.

Na tym ogólnym diagramie przepływu danych przedstawiono aktualizacje.

  ![Najważniejsze możliwości][2]

Dzięki wprowadzeniu tych najważniejszych możliwości przemysłowego IoT usługa Time Series Insights oferuje następujące kluczowe korzyści.

| | |
| ---| ---|
| **Wielowarstwowy magazyn dla danych szeregów czasowych w skali IoT** | Wspólny potok przetwarzania danych do pozyskiwania danych umożliwia przechowywanie danych w ciepłym magazynie na potrzeby interaktywnych zapytań. Duże ilości danych można również przechowywać w zimnym magazynie. Można też korzystać z zalet wysoce wydajnych [zapytań](./time-series-insights-update-tsq.md) opartych na zasobach. |
| **Model szeregu czasowego na potrzeby określania kontekstu nieprzetworzonych danych telemetrycznych i uzyskiwania szczegółowych danych opartych na zasobach** | Określanie kontekstu dla nieprzetworzonych danych telemetrycznych za pomocą opisowego [modelu szeregów czasowych](./time-series-insights-update-tsm.md). Uzyskiwanie zaawansowanych analiz operacyjnych za pomocą zoptymalizowanych pod kątem wydajności i kosztów zapytań opartych na urządzeniach. |
| **Bezproblemowa i ciągła integracja z innymi rozwiązaniami do obsługi danych** |  Dane w usłudze Time Series Insights są [przechowywane](./time-series-insights-update-storage-ingress.md) w plikach rozwiązania open source Apache Parquet. Możliwa jest łatwa integracja z innymi rozwiązaniami do obsługi danych (zarówno własnymi jak i zewnętrznymi) na potrzeby kompleksowych scenariuszy. Scenariusze mogą obejmować analizę biznesową, zaawansowane uczenie maszynowe oraz analizę predykcyjną. |
| **Eksploracja danych w czasie niemal rzeczywistym** | Środowisko użytkownika [eksploratora usługi Azure Time Series Insights w wersji zapoznawczej](./time-series-insights-update-explorer.md) udostępnia wizualizacje dla wszystkich danych przesyłanych strumieniowo za pośrednictwem potoku pozyskiwania. Wkrótce po nawiązaniu połączenia ze źródłem zdarzeń można wyświetlać i eksplorować dane zdarzeń, jak również wykonywać dotyczące ich zapytania. W ten sposób można sprawdzić, czy urządzenie emituje dane zgodnie z oczekiwaniami. Można również monitorować kondycję, wydajność i ogólną efektywność zasobu IoT. |
| **Analizowanie głównych przyczyn problemów i wykrywanie anomalii** | [Eksplorator usługi Azure Time Series Insights w wersji zapoznawczej](./time-series-insights-update-explorer.md) obsługuje wzorce i widoki perspektyw, które pozwalają przeprowadzać i zapisywać wieloetapowe analizy głównych przyczyn. Łącząc usługę Time Series Insights z usługą Azure Stream Analytics, można wykrywać alerty i anomalie w czasie zbliżonym do rzeczywistego. |
| **Aplikacje niestandardowe tworzone na platformie usługi Time Series Insights** | Usługa Time Series Insights obsługuje [zestaw SDK języka JavaScript](./tutorial-explore-js-client-lib.md). Ten zestaw SDK zapewnia zaawansowane kontrolki i uproszczony dostęp do zapytań. Można go użyć do tworzenia niestandardowych aplikacji IoT opartych na usłudze Time Series Insights odpowiadających określonym potrzebom biznesowym. Można również bezpośrednio korzystać z [interfejsów API zapytań](./time-series-insights-update-tsq.md) usługi Time Series Insights, aby kierować dane do niestandardowych aplikacji IoT. |

## <a name="next-steps"></a>Następne kroki

Wprowadzenie do usługi Azure Time Series Insights w wersji zapoznawczej:

> [!div class="nextstepaction"]
> [Zapoznaj się z przewodnikiem Szybki start](./time-series-insights-update-quickstart.md)

Dowiedz się więcej na temat przypadków użycia:

> [!div class="nextstepaction"]
> [Przypadki użycia usługi Azure Time Series Insights w wersji zapoznawczej](./time-series-insights-update-use-cases.md)

<!-- Images -->
[1]: media/v2-update-overview/overview_one.png
[2]: media/v2-update-overview/overview_two.png