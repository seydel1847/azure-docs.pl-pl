---
title: Obsługa języków — interfejs API wyszukiwania obrazów Bing
titleSuffix: Azure Cognitive Services
description: Dowiedz się, które kraje/regiony i języki są obsługiwane przez interfejs API wyszukiwania obrazów Bing.
services: cognitive-services
author: aahill
manager: cgronlun
ms.service: cognitive-services
ms.component: bing-image-search
ms.topic: article
ms.date: 10/06/2017
ms.author: aahi
ms.openlocfilehash: e5c9a4291501c657a94509aec2edd90d00ab795d
ms.sourcegitcommit: ebf2f2fab4441c3065559201faf8b0a81d575743
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/20/2018
ms.locfileid: "52160431"
---
# <a name="language-and-region-support-for-the-bing-image-search-api"></a>Obsługa języka i regionu dla interfejsu API wyszukiwania obrazów Bing

Interfejs API wyszukiwania obrazów Bing obsługuje więcej niż trzech tuzina kraje/regiony, wiele z więcej niż jednym języku. Określanie kraj/region z zapytaniem służy przede wszystkim, aby zawęzić wyniki wyszukiwania, w oparciu o zainteresowania tego kraju/regionu. Ponadto wyniki mogą zawierać łącza do usługi Bing, a te linki mogą lokalizować Bing środowiska użytkownika zgodnie z określonych krajów/regionów lub języka.

Aby określić kraj/region i język, ustaw `mkt` parametr zapytania (rynek) do kodu ze **rynków** w poniższej tabeli. Rynek Określa kraj/region i język. Jeśli użytkownik chce zobaczyć wyświetlania tekstu w innym języku, należy ustawić `setLang` parametru w kodzie odpowiedni język zapytania.

Alternatywnie można określić za pomocą kraju/regionu `cc` parametr zapytania. Jeśli określisz kraju/regionu, należy także określić co najmniej jeden kod języka przy użyciu `Accept-Language` nagłówka HTTP. Obsługiwane języki zależą od kraju/regionu są one podane dla każdego kraju/regionu w tabeli rynkach.

> [!NOTE]
> Interfejs API obrazów na popularności obecnie obsługuje tylko następujące rynki:
> - EN US (angielski, Stany Zjednoczone)
> - EN-CA (angielski, Kanada)
> - EN-AU (angielski, Australia)
> - nazwy zh-CN (chińskim, Chiny)

## <a name="countries"></a>Kraje

|Kraj/region|Kod|
|-------|----|
|Argentyna|AR|
|Australia|AU|
|Austria|AT|
|Belgia|BE|
|Brazylia|BR|
|Kanada|CA|
|Chile|CL|
|Dania|DK|
|Finlandia|FI|
|Francja|PW|
|Niemcy|DE|
|SRA Hongkong|HK|
|Indie|IN|
|Indonezja|ID|
|Włochy|IT|
|Japonia|JP|
|Korea|KR|
|Malezja|MY|
|Meksyk|MX|
|Holandia|NL|
|Nowa Zelandia|NZ|
|Norwegia|NO|
|Chiny|CN|
|Polska|PL|
|Portugalia|PT|
|Filipiny|PH|
|Rosja|RU|
|Arabia Saudyjska|SA|
|Republika Południowej Afryki|ZA|
|Hiszpania|ES|
|Szwecja|SE|
|Szwajcaria|CH|
|Tajwan|TW|
|Turcja|TR|
|Wielka Brytania|GB|
|Stany Zjednoczone|USA|


## <a name="markets"></a>Rynki

|Kraj/region|Język|Rynek kodu|
|-------|--------|-----------|
|Argentyna|Hiszpański|ES AR|
|Australia|Polski|EN-AU|
|Austria|Niemiecki|de-AT|
|Belgia|Holenderski|Holandia — być|
|Belgia|Francuski|FR — być|
|Brazylia|Portugalski|pt-BR|
|Kanada|Polski|EN-CA|
|Kanada|Francuski|fr-CA|
|Chile|Hiszpański|ES-CL|
|Dania|Duński|Akcelerator deweloperski w wersji DK|
|Finlandia|Fiński|fi-FI|
|Francja|Francuski|fr-FR|
|Niemcy|Niemiecki|de-DE.|
|SRA Hongkong|Chiński (tradycyjny)|zh-HK|
|Indie|Polski|EN-IN|
|Indonezja|Polski|EN-ID|
|Włochy|Włoski|IT-IT|
|Japonia|Japoński|ja-JP|
|Korea|Koreański|ko-KR|
|Malezja|Polski|Moje en|
|Meksyk|Hiszpański|es-MX|
|Holandia|Holenderski|NL-NL|
|Nowa Zelandia|Polski|EN NZ|
|Chiny|Chiński|zh-CN|
|Polska|Polski|pl-PL|
|Portugalia|Portugalski|pt-PT|
|Filipiny|Polski|EN PH|
|Rosja|Rosyjski|ru-RU|
|Arabia Saudyjska|Arabski|ar-SA|
|Republika Południowej Afryki|Polski|EN ZA|
|Hiszpania|Hiszpański|es-ES|
|Szwecja|Szwedzki|sv-SE|
|Szwajcaria|Francuski|FR-CH|
|Szwajcaria|Niemiecki|de-CH|
|Tajwan|Chiński (tradycyjny)|zh-TW|
|Turcja|Turecki|tr-TR|
|Wielka Brytania|Polski|en-GB|
|Stany Zjednoczone|Polski|pl-PL|
|Stany Zjednoczone|Hiszpański|es-US|

## <a name="next-steps"></a>Kolejne kroki
Aby uzyskać więcej informacji na temat punktów końcowych wyszukiwania wiadomości Bing, zobacz [odwołanie do interfejsu API wyszukiwania obrazów wiadomości w wersji 7](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference).
