---
title: Wymowa niestandardowych za pomocą usługa Custom Speech Service na platformie Azure | Dokumentacja firmy Microsoft
description: Dowiedz się, jak utworzyć model języka dzięki usłudze Custom Speech Service w usługach Cognitive Services.
services: cognitive-services
author: PanosPeriorellis
manager: onano
ms.service: cognitive-services
ms.component: custom-speech
ms.topic: article
ms.date: 11/23/2017
ms.author: panosper
ms.openlocfilehash: 1e9de9755ef4baee7e2a0e6c093e2cf27cb4281f
ms.sourcegitcommit: 1aacea6bf8e31128c6d489fa6e614856cf89af19
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/16/2018
ms.locfileid: "49339818"
---
# <a name="enable-custom-pronunciation"></a>Włącz Wymowa niestandardowe

[!INCLUDE [Deprecation note](../../../../includes/cognitive-services-custom-speech-deprecation-note.md)]

Wymowa niestandardowych umożliwia użytkownikom na definiowanie w postaci fonetycznej i wyświetlania słowa lub terminy. Jest to przydatne do obsługi warunki niestandardowe, takie jak nazwy produktów lub akronimów. Wszystko co potrzebne jest plikiem Wymowa (pliku txt prosty).

Oto, jak to działa. W pliku txt pojedynczego można wprowadzić kilka niestandardowych Wymowa wpisów. Struktura jest następująca:

```
Display form <Tab> Spoken form <Newline>
```

*Przykłady*:

| Formularz wyświetlania | Mówionej formy |
|----------|-------|
| C3PO | Zobacz trzy PLA o |
| L8R | Rozpoznanie późnego są |
| CNTK | Zobacz n herbaty k|

## <a name="requirements-for-the-spoken-form"></a>Wymagania dotyczące mówionej formy
Mówionej formy musi być pisana małymi literami i który aktualizację można wymusić podczas importowania. Ponadto należy podać zaewidencjonuje odbierający dane. Nie karty w mówionej formy lub formularz wyświetlania jest dozwolone. Może jednak, bardziej zabronione znaki w formularzu wyświetlania (na przykład ~ i ^).

Każdy plik txt może mieć kilka pozycji. Na przykład zobacz poniższy zrzut ekranu:

![Zrzut ekranu Notatnika kilka wpisy dla Wymowa akronim](../../../media/cognitive-services/custom-speech-service/custom-speech-pronunciation-file.png)

Mówionej formy jest ciągiem fonetycznych formularz wyświetlania. Składa się z liter, słowa lub sylab. Obecnie nie ma żadnych dalszych wskazówek lub zestaw standardów, aby pomóc w tworzeniu mówionej formy. 

## <a name="supported-pronunciation-characters"></a>Wymowa obsługiwane znaki
Wymowa niestandardowego jest obecnie obsługiwane dla języka angielskiego (en US) i niemiecki (de-de). Zestaw znaków, który może służyć do wyrażenia mówionej formy termin (w pliku niestandardowego Wymowa) zostały przedstawione w poniższej tabeli: 

| Język | Znaki |
|---------- |----------|
| Angielski (en US) | , b, c, d, e, f, g, h, i, "j", k, l, o, p, pytania i odpowiedzi, r, s, t, u, v, w, x, y, z |
| Niemiecki (de-de) | ä strumień świetlny, znaki ü, ẞ, a, b, c, d, e, f, g, h, i, "j", k, l, o, p, pytania i odpowiedzi, r, s, t, u, v, w, x, y, z |

>[UWAGA] Formularz wyświetlania termin (w pliku Wymowa) zapisywane taki sam sposób w zestawie danych dostosowywania języka.

## <a name="requirements-for-the-display-form"></a>Wymagania dotyczące formularz wyświetlania
Formularz wyświetlania można tylko niestandardowe słowo "," termin "," akronim "lub" wyrazy złożone łączące istniejące słowa. Można również wprowadzić alternatywne wymowy popularne wyrazy. 

>[!NOTE]
Firma Microsoft nie zaleca się używania tej funkcji, aby sformułować popularnych wyrazów lub zmodyfikować mówionej formy. Zaleca dekodera, aby zobaczyć, jeśli niektóre nietypowe wyrazy (na przykład skróty wyrazy techniczne i obce słowa) nie są prawidłowo zdekodować. W takim przypadku należy dodać je do pliku Wymowa niestandardowych. W Model języka należy zawsze i tylko używać formularz wyświetlania wyrazu. 

## <a name="requirements-for-the-file-size"></a>Wymagania dotyczące rozmiaru pliku
Rozmiar pliku txt, zawierające wpisy Wymowa jest ograniczona do 1 MB. Zazwyczaj jest konieczne przekazywanie dużych ilości danych przy użyciu tego pliku. Większość plików niestandardowych Wymowa prawdopodobnie kilka artykułów bazy wiedzy w rozmiarze. Kodowanie pliku txt, dla wszystkich ustawień regionalnych powinna być BOM UTF-8. Angielskie ustawienia regionalne dopuszczalne jest również ANSI.

## <a name="next-steps"></a>Kolejne kroki
* Popraw dokładności rozpoznawania, tworząc usługi [niestandardowy model akustyczny](cognitive-services-custom-speech-create-acoustic-model.md).
* [Utwórz niestandardowy punkt końcowy rozpoznawania mowy na tekst](cognitive-services-custom-speech-create-endpoint.md), którego można używać w aplikacji.
