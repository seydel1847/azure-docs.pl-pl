---
title: Funkcje
titleSuffix: Language Understanding - Azure Cognitive Services
description: Dodawanie funkcji do języka modelu w celu dostarczanie wskazówek na temat rozpoznawanie dane wejściowe, które chcesz oznaczyć lub klasyfikowanie.
services: cognitive-services
author: diberry
manager: cgronlun
ms.custom: seodec18
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: conceptual
ms.date: 01/02/2019
ms.author: diberry
ms.openlocfilehash: 2d6f7e2fd332e1687db1564befeb6f531045c5dd
ms.sourcegitcommit: fd488a828465e7acec50e7a134e1c2cab117bee8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/03/2019
ms.locfileid: "53993070"
---
# <a name="phrase-list-features-in-your-luis-app"></a>Wyrażenie funkcji listy aplikacją usługi LUIS

W usłudze machine learning *funkcji* wyróżniający cechy lub atrybutu danych, która przestrzega systemu. 

Dodawanie funkcji do języka modelu w celu dostarczanie wskazówek na temat rozpoznawanie dane wejściowe, które chcesz oznaczyć lub klasyfikowanie. Funkcje usługi LUIS rozpoznać intencje i podmioty, funkcje nie są jednak intencji lub jednostek, samodzielnie. Zamiast tego funkcji może zawierać przykłady powiązanych z nimi terminów.  

## <a name="what-is-a-phrase-list-feature"></a>Co to jest funkcja listy fraz?
Lista fraz obejmuje grupy wartości (słów i fraz), które należą do tej samej klasy i muszą być traktowane w podobny sposób (na przykład nazwy miasta lub produktów). Usługa LUIS się o jeden z nich jest automatycznie stosowany do pozostałych. Ta lista nie jest zamknięty [listy jednostek](luis-concept-entity-types.md#types-of-entities) (dokładne dopasowania tekstu) dopasowane słów.

Lista fraz dodaje do słownictwa używanego w domenie aplikacji jako drugi sygnał do usługi LUIS o tych słów.

## <a name="phrase-lists-help-all-models"></a>Wyświetla frazy pomocy wszystkie modele

Wyświetla frazy nie są powiązane z określonym celem lub jednostki, ale są dodawane do wszystkich modeli jako boost. Jego celem jest poprawa intencji klasyfikacji wykrywania i jednostki.

## <a name="how-to-use-phrase-lists"></a>Jak używać listy fraz
W aplikacji zasobów ludzkich [podmiotu prostego samouczka](luis-quickstart-primary-and-secondary-data.md), ta aplikacja używa **zadania** frazy listę typów zadań, takich jak programista, roofer i Sekretarz. Jeśli etykieta jedną z następujących wartości jako jednostki przedstawiono maszyny usługi LUIS jest uczy się rozpoznawać, pozostałe. 

Lista wyrażenie może być zamienne lub -wymienne. *Wymienne* lista frazy to wartości, które są synonimy, i *-wymienne* frazy listy ma służyć jako lista słownictwa określonych aplikacji. Proporcjonalna do rozwoju środowiska listy fraz słownictwa aplikacji może się okazać, niektóre terminy ma wiele form (synonimy). Podziel te, na inną listę frazę, która jest wymienne. 

|Typ listy|Przeznaczenie|
|--|--|
|Wymienne|Synonimy lub słowa, po zmianie na innym słowie na liście, mają tego samego intencji i działania funkcji wydobywania podmiotów.|
|-Wymienne|Słownictwa aplikacji specyficzne dla aplikacji, więcej, niż zazwyczaj innych wyrazów, w tym języku.|

Wyrażenie zawiera nie tylko pomoc dotycząca wykrywania jednostki, ale również intencji klasyfikacji w przypadku, gdy nie są wymienne sens takich jak dodawanie poza słownictwa wyrazy, które nie są znane w języku angielskim.


<a name="phrase-lists-help-identify-simple-exchangeable-entities"></a>

## <a name="phrase-lists-help-identify-simple-interchangeable-entities"></a>Wyrażenie zawiera pomoc zidentyfikować proste jednostki wymienne
Wymienne frazy listy są dobrym sposobem dostrajaniu aplikacją usługi LUIS. Jeśli aplikacja ma problemy z wypowiedzi na intencje prawidłowe przewidywanie lub rozpoznawania jednostek, zastanów się, czy wypowiedzi zawierać słów nietypowe lub słowa, które mogą być niejednoznaczne w znaczenie. Te wyrazy są dobrymi kandydatami do uwzględnienia na liście frazę.

## <a name="phrase-lists-help-identify-intents-by-better-understanding-context"></a>Wyrażenie zawiera pomoc rozpoznać intencje lepsze zrozumienie kontekstu
Lista frazy jest instrukcję do usługi LUIS, aby wykonać dopasowywanie strict lub wszystkie warunki na liście wyrażenie zawsze etykiety, dokładnie tak samo. Jest po prostu wskazówką. Na przykład masz listę frazę, która wskazuje, że "Patti" i "Selma" nazwy, ale usługa LUIS mogą nadal korzystać z informacji kontekstowych, aby rozpoznać, czy ich oznacza coś innego w "Rezerwować 2 w Diner firmy Patti na obiad" i "mnie znaleźć jazdy Wskazówki dojazdu Selma, Gruzja". 

Dodawanie listy fraz jest zamiast dodawać więcej wypowiedzi przykład do intencji. 

## <a name="an-interchangeable-phrase-list"></a>Lista wymienne fraz
Użyj listy fraz wymienne, gdy tworzy listę słów lub fazy, klasę lub grupę. Przykład znajduje się lista miesięcy, takich jak "Stycznia", "Czerwiec", "Marca"; lub nazwy, takie jak "John", "Jan", "Piotr".  Te listy są wymienne, w tym wypowiedź będzie oznaczone przy użyciu tego samego przeznaczenie lub jednostki jeśli były używane różne wyraz na liście frazę. Na przykład jeśli "Pokaż kalendarz styczeń" ma taką samą intencji "Pokaż kalendarz lutego", a następnie wyrazy, które powinny być na liście wymienne. 

## <a name="a-non-interchangeable-phrase-list"></a>Lista frazy-wymienne
Użyj listy-wymienne frazy-równoznaczny słów i fraz, które mogą być grupowane w domenie. 

Jako przykład należy użyć listy-wymienne frazy dla rzadko, własności i obce słowa. Usługa LUIS może być nie można rozpoznać rzadkie i zastrzeżonych słów, jak również obce słowa (poza kultura aplikacji). -Wymienne ustawienie wskazuje, że zbiór słów rzadkich formularzy klasę, która LUIS powinien Naucz się rozpoznawać, ale nie są one synonimy lub wymienne ze sobą.

## <a name="when-to-use-phrase-lists-versus-list-entities"></a>Kiedy należy używać list frazy i listę jednostek
Gdy Lista fraz i listy jednostek może mieć wpływ na wypowiedzi we wszystkich intencji, każdy robi to w inny sposób. Użyj listy fraz wpływa na wynik konwersji prognozy. Użyj jednostki listy wpływa na działania funkcji wydobywania podmiotów dopasowania tekstu do dokładnego dopasowania. 

### <a name="use-a-phrase-list"></a>Użyj listy fraz
Z listą frazy LUIS nadal mogą uwzględniać kontekstu i generalize, aby zidentyfikować elementy, które są podobne do, ale nie dokładne dopasowanie, jako elementów na liście. Jeśli potrzebujesz aplikacją usługi LUIS, aby można było do uogólnienia i identyfikowania nowych elementów w kategorii, użyj listy fraz. 

Aby rozpoznawać nowych wystąpień jednostki, takie jak harmonogram spotkań, który powinien rozpoznawać nazwy nowych kontaktów lub aplikację magazynu, która powinna rozpoznać nowe produkty używać innego typu maszyny do opanowania jednostki, takie jak prosty lub Jednostka hierarchicznej. Następnie utwórz frazy listę słów i fraz, które pomaga LUIS Znajdź innymi słowy podobne do jednostki. Ta lista zawiera informacje na temat usługi LUIS, rozpoznawał przykłady jednostki, dodając dodatkowe znaczenie wartość tych słów. 

Wyświetla frazy są podobne słownictwa specyficznego dla domeny, które ułatwić udoskonalanie jakości zrozumieć intencje i podmioty. Wspólne użycie listy fraz jest nazwy własne takie jak nazwy miast. Nazwa miasta może być kilka słów, takich jak łączniki lub apostrofy.
 
### <a name="dont-use-a-phrase-list"></a>Nie należy używać listy fraz 
Jednostka listy jawnie definiuje każda wartość jednostki może potrwać i identyfikuje tylko wartości, które dokładnie pasować. Jednostka listy może być odpowiednie dla aplikacji, w której wszystkie wystąpienia jednostki są znane i nie zmieniają się często. Przykładami są elementy żywności, w menu restauracji, które zmieniają się rzadko. Jeśli potrzebujesz dopasowania tekstu do dokładnego dopasowania jednostki, nie należy używać listy fraz. 

## <a name="best-practices"></a>Najlepsze praktyki
Dowiedz się, [najlepsze praktyki](luis-concept-best-practices.md).

## <a name="next-steps"></a>Kolejne kroki

Zobacz [Dodaj funkcje](luis-how-to-add-features.md) Aby dowiedzieć się więcej na temat sposobu dodawania funkcji do aplikacji usługi LUIS.
