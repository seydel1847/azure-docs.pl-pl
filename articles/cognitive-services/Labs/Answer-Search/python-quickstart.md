---
title: 'Szybki start: laboratorium Project Answer Search, Python'
titlesuffix: Azure Cognitive Services
description: Wprowadzenie do korzystania z laboratorium Project Answer Search na przykładzie języka Python.
services: cognitive-services
author: mikedodaro
manager: cgronlun
ms.service: cognitive-services
ms.component: answer-search
ms.topic: quickstart
ms.date: 04/13/2018
ms.author: rosh
ms.openlocfilehash: 69c5edfef65af2ed1b27f9a512ad13c21468df7a
ms.sourcegitcommit: 62759a225d8fe1872b60ab0441d1c7ac809f9102
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/19/2018
ms.locfileid: "49465512"
---
# <a name="quickstart-project-answer-search-with-python"></a>Szybki start: laboratorium Project Answer Search w języku Python

Poniższy przykład w języku Python tworzy i wysyła żądanie dotyczące informacji na temat Skały Gibraltarskiej.

## <a name="prerequisites"></a>Wymagania wstępne

Pobierz klucz dostępu dla bezpłatnej wersji próbnej zestawu [Cognitive Services Labs](https://aka.ms/answersearchsubscription).

W tym przykładzie użyto języka Python 3.6.4

## <a name="code-scenario"></a>Scenariusz kodu 

Poniższy kod tworzy podgląd adresu URL.
W celu zaimplementowania kodu wykonaj następujące kroki:
1. Zadeklaruj zmienne, aby określić punkt końcowy na podstawie hosta i ścieżki.
2. Określ adres URL zapytania, dla którego ma zostać wyświetlony podgląd, a następnie dodaj parametr zapytania.  
3. Ustaw parametr zapytania.
4. Zdefiniuj funkcję wyszukiwania, która tworzy żądanie i dodaje nagłówek *Ocp-Apim-Subscription-Key*.
5. Ustaw nagłówek *Ocp-Apim-Subscription-Key*. 
6. Nawiąż połączenie i wyślij żądanie.
7. Wydrukuj wyniki w formacie JSON.

Pełny kod tej wersji demonstracyjnej wygląda następująco:

````
import http.client, urllib.parse
import json

# Replace the subscriptionKey string value with your valid subscription key.
subscriptionKey = 'YOUR-SUBSCRIPTION-KEY'

host = 'https://api.labs.cognitive.microsoft.com'
path = '/answerSearch/v7.0/search '

query = 'Rock of Gibraltar'

params = '?q=' + urllib.parse.quote (query) + '&mkt=en-us'

def get_local():
    headers = {'Ocp-Apim-Subscription-Key': subscriptionKey}
    conn = http.client.HTTPSConnection (host)
    conn.request ("GET", path + params, None, headers)
    response = conn.getresponse ()
    return response.read ()

result = get_local()
print (json.dumps(json.loads(result), indent=4))

````
## <a name="next-steps"></a>Następne kroki
- [Przewodnik Szybki start dla języka C#](c-sharp-quickstart.md)
- [Przewodnik Szybki start dla języka Java](java-quickstart.md)
- [Przewodnik Szybki start dla środowiska Node](node-quickstart.md)