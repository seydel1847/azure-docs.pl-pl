---
title: Zdania i tokeny - interfejsu API analizy językowej
titlesuffix: Azure Cognitive Services
description: Więcej informacji na temat oddzielanie w interfejsu API analizy językowej wyrazów i tokenów.
services: cognitive-services
author: DavidLiCIG
manager: cgronlun
ms.service: cognitive-services
ms.component: linguistic-analysis
ms.topic: conceptual
ms.date: 03/21/2016
ms.author: davl
ROBOTS: NOINDEX
ms.openlocfilehash: 96c2bd1c11554481e441662a6051620f4b2e2993
ms.sourcegitcommit: 803e66de6de4a094c6ae9cde7b76f5f4b622a7bb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/02/2019
ms.locfileid: "53972366"
---
# <a name="sentence-separation-and-tokenization"></a>Oddzielanie wyrazów i tokenów

> [!IMPORTANT]
> Wersja zapoznawcza analizy językowej została wycofana 9 sierpnia 2018 r. W celu przetwarzania i analizy tekstu zalecamy korzystanie z [modułów analizy tekstu w usłudze Azure Machine Learning](https://docs.microsoft.com/azure/machine-learning/studio-module-reference/text-analytics).

## <a name="background-and-motivation"></a>Tło i motywację

Biorąc pod uwagę treści pewnego tekstu, pierwszym krokiem analizy językowej jest podzielenie go na zdania i tokeny.

### <a name="sentence-separation"></a>Rozdzielenie zdania

Na pierwszy rzut oka, wygląda na to podzielenie tekst na zdania to proste: wystarczy znaleźć znaczniki koniec zdania i Podziel zdania istnieje.
Te znaczniki są jednak często skomplikowane i niejednoznaczne.

Należy wziąć pod uwagę następujące tekstowi przykładu:

> Co powiedziałeś?!? Nie zasłyszane dyrektora "Nowa propozycja." Warto Pan i Pani Smith.

Ten tekst zawiera trzy zdania:

- Co powiedziałeś?!?
- Nie zasłyszane dyrektora "Nowa propozycja."
- Warto Pan i Pani Smith.

Należy pamiętać o tym, jak koniec zdania są oznaczone na różne sposoby.
Pierwszy kończy się na kombinacji znaków zapytania i wykrzykniki (czasami nazywany interrobang).
Drugi kończy się kropką ani kropką, ale następujące znaku cudzysłowu powinny były ściągane do poprzedniego zdania.
W trzecim zdania można zobaczyć, jak ten sam znak kropki może służyć do oznaczania także skrótami.
Patrząc tylko znaki interpunkcyjne udostępnia zestaw dobrym kandydatem, ale dalszej pracy jest wymagane w celu zidentyfikowania granice true zdania.

### <a name="tokenization"></a>Tokenizacji

Kolejnym krokiem jest Podziel te zdania na tokeny.
W większości przypadków angielskiej tokeny są rozdzielone biały znak.
(Wyszukiwanie tokenów lub wyrazów jest znacznie łatwiejsze w języku angielskim niż chiński, gdzie przede wszystkim nie służą spacji między wyrazami.
Pierwsze zdanie mogą być zapisane jako "Whatdidyousay?")

Istnieje kilka przypadków trudne.
Po pierwsze znaki interpunkcyjne często (ale nie zawsze) powinny być podziału poza nie otaczającego kontekstu.
Po drugie, ma angielski *skrótów*, takie jak "nie" lub "to", gdy skompresowane i skrót na mniejsze części słowa.
Celem tokenizator jest przerwać sekwencja znaków słowa.

Powrócimy do zdań przykład z góry.
Teraz możemy zostały umieszczone "center dot" (&middot;) między każdy token distinct.

- Co &middot; czy &middot; możesz &middot; powiedzieć &middot; ?!?
- Czy mogę &middot; została &middot; IE &middot; Posłuchaj &middot; o &middot; &middot; Dyrektor ds. &middot; firmy &middot; " &middot; nowe &middot; propozycji &middot; . &middot; "
- Jego &middot; firmy &middot; ważne &middot; do &middot; Pan&middot; i &middot; Pani. &middot; Nowak &middot; .

Należy zauważyć, jak większości tokeny to słowa, które można znaleźć w słowniku (na przykład *ważne*, *Dyrektor*).
Inne może składać się wyłącznie znaków interpunkcyjnych.
Istnieją bardziej nietypowe tokenów do reprezentowania skrótów, takich jak *IE* dla *nie*, i Zaimki dzierżawcze, takich jak *firmy*.
Ta tokenizacji umożliwia obsługę słowa *nie* i zwrot *nie* w bardziej spójny sposób.

## <a name="specification"></a>Specyfikacja

Należy spójne decyzje dotyczące co składa się z zdania i token.
Polegamy na specyfikacji z [Treebank partnerów](https://catalog.ldc.upenn.edu/LDC99T42) (niektóre dodatkowe szczegóły są dostępne pod adresem ftp://ftp.cis.upenn.edu/pub/treebank/public_html/tokenization.html).
