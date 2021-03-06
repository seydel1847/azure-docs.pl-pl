---
title: Co to jest Video Indexer?
titlesuffix: Azure Media Services
description: Ten temat zawiera omówienie usługi Video Indexer.
services: media-services
author: Juliako
manager: femila
ms.service: media-services
ms.topic: article
ms.date: 12/24/2018
ms.author: juliako
ms.openlocfilehash: 58124ab5938c7bee9f83a8c37ab5c5618b4b7d54
ms.sourcegitcommit: 295babdcfe86b7a3074fd5b65350c8c11a49f2f1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/27/2018
ms.locfileid: "53789827"
---
# <a name="what-is-video-indexer"></a>Co to jest Video Indexer?

Usługa Azure Video Indexer to aplikacja w chmurze utworzona za pomocą usługi Azure Media Analytics, usługi Azure Search oraz usług Cognitive Services (takich jak interfejs API rozpoznawania twarzy, Microsoft Translator, interfejs API przetwarzania obrazów i Custom Speech Service). Umożliwia wyodrębnianie szczegółowych informacji z plików wideo przy użyciu opisanych poniżej modeli usługi Video Indexer:
 
- **Automatyczne wykrywanie języka**: Automatycznie rozpoznaje dominujący język mówiony. Obsługiwane języki: angielski, chiński (uproszczony), francuski, hiszpański, japoński, niemiecki, portugalski (Brazylia), rosyjski i włoski. Gdy języka nie będzie można wykryć, użyty zostanie język angielski.
- **Transkrypcję audio**: Konwertuje mowy na tekst w 12 języków i umożliwia rozszerzeń. Obsługiwane języki angielski, hiszpański, francuski, niemiecki, włoski, chiński (uproszczony), japoński, arabski, rosyjski, portugalski (Brazylia), Hindi i koreańskim.
- **Podpisy kodowane**: Tworzy kodowanych w trzech formatach: SRT VTT, TTML.
- **Dwa kanału przetwarzania**: Automatycznie wykryje, oddziel transkrypcji i scalenia na pojedynczej osi czasu.
- **Redukcja szumów**:  Czyści się nagrania audio lub hałas telefonii (oparte na filtry Skype).
- **Dostosowywanie transkrypcji (CRI)**: Szkolenie modeli i wykonuje rozszerzonej niestandardowa zamiana mowy na tekst modele, aby utworzyć zapisy branżowych.
- **Wyliczenie osoby mówiącej**:  Mapuje i zrozumienie, które osoby mówiącej typu gwiazda które wyrazy i kiedy.
- **Statystyki osoby mówiącej**: Zawiera dane statystyczne prelegentów mowy proporcji.
- **Tekst Visual rozpoznawania znaków (OCR)**: Wyodrębnianie tekstu wyświetlanego wizualnie w trakcie filmu wideo.
- **Ramka kluczowa wyodrębniania**: Wykrywa stabilne ramek kluczowych w filmie wideo.
- **Analiza tonacji**: Identyfikuje dodatnie, ujemne i neutralne tonacji, rozpoznawania mowy i tekstu.
- **Moderowanie zawartości Visual**: Wykrywa przeznaczonej dla osób dorosłych i/lub erotycznej wizualizacji.
- **Wyodrębnianie słów kluczowych**: Wyodrębnianie słów kluczowych z mowy i tekstu.
- **Identyfikator etykiety**: Identyfikuje obiektów wizualnych i wyświetlane czynności.
- **Marki wyodrębniania**: Wyodrębnia marek z mowy i tekstu.
- **Wykrywanie twarzy**: Wykrywa i grupuje twarzy w filmie wideo.
- **Wyodrębnianie miniatury dla powierzchni ("najlepsze rozpoznawania twarzy")**: Automatycznie identyfikuje najlepiej twarzy przechwyconych w każdej grupie twarze (w oparciu jakości, rozmiar i położenie czołowego) i wyodrębnij go jako zasób obrazu.
- **Identyfikacja osobistości**: Indeksator wideo automatycznie rozpoznaje osobistości ponad 1 milion — takich jak liderów world aktorów i aktorki, sportowców, pracowników naukowo-badawczych, firm i liderzy techniczni na całym świecie. Dane dotyczące tych osobistości można znaleźć również w różnych znanych witrynach internetowych, takich jak IMDB czy Wikipedia.
- **Identyfikowanie twarzy oparte na koncie**: Usługa Video Indexer przygotowuje modelu dla określonego konta. Następnie rozpoznaje twarze w nagraniu wideo na podstawie modelu wyszkolonego specjalnie na potrzeby filmów wideo na tym koncie.
- **Moderowanie zawartości tekstowej**: Wykrywa jawnego tekstu transkrypcji audio.
- **Zrzut wykrywania**: Określa, kiedy zmiany sceny, w trakcie filmu wideo.
- **Wykrywanie ramki czarnego**: Identyfikuje czarne ramek przedstawiony w wideo.
- **Efekty dźwiękowe**: Identyfikuje efekty dźwiękowe, takie jak Oklaski ręcznie, mowy i wyciszenia.
- **Wnioskowanie o temacie**: Sprawia, że wnioskowania główne tematy z transkrypcji. Uwzględniana jest taksonomia [IPTC](https://iptc.org/standards/media-topics/) 1. poziomu.
- **Wykrywanie emocji**: Rozpoznaje emocje, które oparte na podpowiedzi mowy i audio. Mogą to być emocje takie jak radość, smutek, gniew czy strach.
- **Artefakty**: Wyodrębnia bogaty zestaw "następny poziom szczegółów" artefaktów dla wszystkich modeli.
- **Tłumaczenie**: Tworzy tłumaczenia transkrypcjach audio do 54 różnych języków.

Gdy usługa Video Indexer zakończy przetwarzanie i analizę, można przeglądać, selekcjonować, przeszukiwać i publikować szczegółowe informacje o wideo.

Bez względu na to, czy jesteś menedżerem zawartości, czy deweloperem, usługa Video Indexer jest w stanie spełnić Twoje wymagania. Menedżerowie zawartości mogą za pomocą portalu internetowego usługi Video Indexer korzystać z niej bez konieczności pisania choćby wiersza kodu — zobacz [Rozpoczynanie korzystania z witryny internetowej usługi Video Indexer](video-indexer-get-started.md). Deweloperzy mogą korzystać z interfejsów API, aby przetwarzać zawartość na dużą skalę — zobacz [Korzystanie z interfejsu API REST usługi Video Indexer](video-indexer-use-apis.md). Usługa ta pozwala też klientom używać widgetów do publikowania strumieni wideo i wyodrębnionych szczegółowych informacji w ich własnych aplikacjach — zobacz [Osadzanie widgetów wizualnych we własnej aplikacji](video-indexer-embed-widgets.md).

Do korzystania z tej usługi możesz się zarejestrować za pomocą już posiadanego konta usługi AAD, LinkedIn, Facebook, Google lub MSA. Aby uzyskać więcej informacji, zobacz [wprowadzenie](video-indexer-get-started.md).

## <a name="scenarios"></a>Scenariusze

Poniżej przedstawiono kilka scenariuszy, w których usługa Video Indexer może być przydatna

- Wyszukiwanie — szczegółowe informacje wyodrębnione z wideo mogą służyć do rozbudowy funkcji wyszukiwania w bibliotece wideo. Na przykład indeksowanie wypowiedzianych słów i twarzy może umożliwić wyszukiwanie w wideo momentów, gdy konkretna osoba wypowiada określone słowa lub gdy dwie osoby są widoczne razem. Wyszukiwanie oparte na takich szczegółowych informacjach przyda się agencjom informacyjnym, instytucjom edukacyjnych, nadawcom, właścicielom zawartości rozrywkowej, w aplikacjach LOB dla przedsiębiorstw i ogólnie w każdej branży z biblioteką wideo, którą użytkownicy muszą przeszukiwać.

- Monetyzacja— usługa Video Indexer może zwiększyć wartość wideo. Przykładowo w branżach zarabiających na reklamach (takich jak media informacyjne czy społecznościowe) możliwe jest dostarczanie trafniejszych reklam przez przekazywanie wyodrębnionych szczegółowych informacji jako dodatkowych danych do serwera reklamowego (wyświetlenie reklamy butów sportowych bardziej pasuje do meczu futbolowego niż zawodów pływackich).

- Zaangażowanie użytkowników — szczegółowe informacje o wideo mogą służyć do zwiększenia stopnia zaangażowania użytkowników przez ustawianie dla nich wideo na odpowiednich momentach. Jako przykład weźmy wideo edukacyjne, w którym przez pierwsze 30 minut omawiane są sfery, a przez kolejne 30 minut — ostrosłupy. Uczeń czytający o ostrosłupach będzie bardziej zadowolony, jeśli wideo będzie ustawione na znaczniku 30. minuty.

Więcej informacji można znaleźć w tym [blogu](https://aka.ms/videoindexerblog).

## <a name="next-steps"></a>Kolejne kroki

Możesz już rozpocząć pracę z usługą Video Indexer. Aby uzyskać więcej informacji zobacz następujące artykuły:

- [Rozpoczynanie korzystania z witryny internetowej usługi Video Indexer](video-indexer-get-started.md)
- [Przetwarzanie zawartości przy użyciu interfejsu REST API usługi Video Indexer](video-indexer-use-apis.md)
- [Osadzanie widgetów wizualnych w aplikacji](video-indexer-embed-widgets.md)
