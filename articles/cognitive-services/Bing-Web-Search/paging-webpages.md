---
title: Jak stronicować za pośrednictwem wyników wyszukiwania - API wyszukiwania w Internecie Bing
titleSuffix: Azure Cognitive Services
description: Dowiedz się, jak stronicować za pośrednictwem wyników wyszukiwania z API wyszukiwania w Internecie Bing.
services: cognitive-services
author: swhite-msft
manager: cgronlun
ms.assetid: 26CA595B-0866-43E8-93A2-F2B5E09D1F3B
ms.service: cognitive-services
ms.component: bing-web-search
ms.topic: conceptual
ms.date: 08/20/2018
ms.author: erhopf
ms.openlocfilehash: e98407dface348dfdbc99a1146d50c46f3bb03a7
ms.sourcegitcommit: ae45eacd213bc008e144b2df1b1d73b1acbbaa4c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/01/2018
ms.locfileid: "50739247"
---
# <a name="how-to-page-through-results-from-the-bing-web-search-api"></a>Jak stronicować za pośrednictwem wyników z API wyszukiwania w Internecie Bing

Po wywołaniu interfejsu API wyszukiwania w Internecie Bing zwraca listę wyników. Lista jest podzbiorem całkowita liczba wyników, które mogą dotyczyć zapytania. Aby uzyskać szacowana liczba dostępnych wyników, dostęp do obiektu odpowiedzi [totalEstimatedMatches](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#totalestimatedmatches) pola.  

W poniższym przykładzie przedstawiono `totalEstimatedMatches` pola, które obejmuje odpowiedzi sieci Web.  

```
{
    "_type" : "SearchResponse",
    "webPages" : {
        "webSearchUrl" : "https:\/\/www.bing.com\/cr?IG=3A43CA...",
        "totalEstimatedMatches" : 262000,
        "value" : [...]
    }
}  
```

Na stronie przy użyciu dostępnych stron sieci Web, należy użyć [liczba](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#count) i [przesunięcie](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#offset) parametry zapytania.  

`count` Parametr określa liczbę wyników do zwrócenia w odpowiedzi. Maksymalna liczba wyników, których może żądać w odpowiedzi jest 50. Wartość domyślna wynosi 10. Rzeczywista liczba dostarczonych może być mniejsza niż żądana.

`offset` Parametr określa liczbę wyników do pominięcia. `offset` Jest liczony od zera i powinna być mniejsza niż (`totalEstimatedMatches` - `count`).  

Jeśli chcesz wyświetlić 15 stron sieci Web na każdej stronie, należy ustawić `count` do 15 i `offset` na 0, aby pobrać pierwszej strony wyników. Na kolejnych stronach, możesz zwiększyć `offset` 15 (na przykład, 15, 30).  

Poniższy przykład żądań 15 stron sieci Web, rozpoczynając od przesunięcia 45.  

```  
GET https://api.cognitive.microsoft.com/bing/v7.0/search?q=sailing+dinghies&count=15&offset=45&mkt=en-us HTTP/1.1  
Ocp-Apim-Subscription-Key: 123456789ABCDE  
Host: api.cognitive.microsoft.com  
```

Jeśli wartość domyślna `count` wartość działa w przypadku implementacji, należy określić `offset` parametr zapytania.  

```  
GET https://api.cognitive.microsoft.com/bing/v7.0/search?q=sailing+dinghies&offset=45&mkt=en-us HTTP/1.1  
Ocp-Apim-Subscription-Key: 123456789ABCDE  
Host: api.cognitive.microsoft.com  
```

Internetowy interfejs API wyszukiwania zwraca wyniki, które obejmują stron sieci Web i może zawierać obrazów, filmów wideo i wiadomości. Po stronie wyników wyszukiwania stronicowania [WebAnswer](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#webanswer) odpowiedzi i nie inne odpowiedzi taką jak obrazy lub wiadomości. Na przykład jeśli ustawisz `count` do 50, wrócisz 50 wyniki strony sieci Web, ale odpowiedź może zawierać wyniki dla innych odpowiedzi także. Na przykład odpowiedź może zawierać 15 obrazów i 4 artykuły z wiadomościami. Istnieje również możliwość, że wyniki mogą obejmować wiadomości na pierwszej stronie, ale nie drugiej strony, lub na odwrót.   

Jeśli określisz `responseFilter` parametr zapytania i nie mają stron sieci Web na liście filtrów, nie używaj `count` i `offset` parametrów. 

> [!NOTE]
> `TotalEstimatedAnswers` Pole jest szacunkową liczbę całkowitą liczbę wyników wyszukiwania, możesz pobrać dla bieżącego zapytania.  Po ustawieniu `count` i `offset` parametrów, `TotalEstimatedAnswers` liczba mogą ulec zmianie. 
