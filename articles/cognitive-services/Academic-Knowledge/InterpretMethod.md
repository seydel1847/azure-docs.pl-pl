---
title: Interpretowanie metody — interfejs Academic Knowledge API
titlesuffix: Azure Cognitive Services
description: Aby powrócić do interpretacji sformatowane ciągi zapytań użytkowników na podstawie danych Academic Graph i akademickich gramatyki w usługach Microsoft Cognitive Services, należy użyć metody interpretację.
services: cognitive-services
author: alch-msft
manager: cgronlun
ms.service: cognitive-services
ms.component: academic-knowledge
ms.topic: conceptual
ms.date: 03/27/2017
ms.author: alch
ms.openlocfilehash: e16a772caa5fba632f8544094e2d8b57ed4ca765
ms.sourcegitcommit: 7824e973908fa2edd37d666026dd7c03dc0bafd0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/10/2018
ms.locfileid: "48902573"
---
# <a name="interpret-method"></a>Interpretowanie — metoda

**Interpretacji** interfejsu API REST trwa użytkownik końcowy ciągu zapytania (czyli zapytanie wprowadzany przez użytkownika w aplikacji), i zwraca sformatowany interpretacji intencji użytkownika na podstawie danych Academic Graph i gramatyki akademickich.

Aby zapewnić środowisko interaktywne, tę metodę można wywołać wielokrotnie, po każdym znaku wprowadzonej przez użytkownika. W takim przypadku należy ustawić **pełną** parametr 1, aby włączyć automatyczne uzupełnianie sugestie. Jeśli aplikacja nie wymaga automatycznego uzupełniania, należy ustawić **pełną** parametru na wartość 0.

**Punkt końcowy REST:**

    https://westus.api.cognitive.microsoft.com/academic/v1.0/interpret?

## <a name="request-parameters"></a>Parametry żądania

Name (Nazwa)     | Wartość | Wymagana?  | Opis
---------|---------|---------|---------
**Zapytanie**    | Ciąg tekstowy | Yes | Zapytanie wprowadzonej przez użytkownika.  Pełne jest ustawiona na 1, zapytania będą interpretowane jako prefiks dla generowania sugestie automatyczne uzupełnianie zapytań.        
**Model**    | Ciąg tekstowy | Nie  | Nazwa modelu, który chcesz zbadać.  Obecnie ma domyślnie wartość *najnowsze*.        
**Wykonaj** | 0 lub 1 | Nie<br>domyślna: 0  | 1 oznacza, że wygenerowany automatycznego uzupełniania, sugestii na podstawie danych gramatyki i graph.         
**Liczba**    | Liczba | Nie<br>domyślny: 10 | Maksymalna liczba interpretacji do zwrócenia.         
**offset**   | Liczba | Nie<br>domyślna: 0  | Indeks pierwszego interpretacji do zwrócenia. Na przykład *count = 2 & przesunięcie = 0* zwraca interpretacje 0 i 1. *liczba = 2 & przesunięcie = 2* zwraca interpretacje 2 i 3.       
**limit czasu**  | Liczba | Nie<br>domyślne: 1000 | Przekroczono limit czasu w milisekundach. Zwracane są tylko interpretacji znaleziono przed upływem limitu czasu.
<br>
  
## <a name="response-json"></a>Odpowiedź (JSON)
Name (Nazwa)     | Opis
---------|---------
**Zapytanie** |*Zapytania* parametrów z żądania.
**interpretacji** |Tablica 0 lub więcej różnych sposobów dopasowywania danych wejściowych użytkownika względem gramatyki.
**.logprob interpretacji [x]**  |Prawdopodobieństwo względne logarytmu naturalnego interpretacji. Większe wartości są bardziej prawdopodobne.
**.parse interpretacji [x]**  |Ciąg XML, który pokazuje, jak interpretować została każda część zapytania.
**Rules interpretacji [x]**  |Tablica co najmniej 1 reguł zdefiniowanych w gramatyce, które były wywoływane podczas interpretacji. Dla interfejsu Academic Knowledge API zawsze będzie 1 regułę.
**interpretacji [.name Rules [t] x]**  |Nazwa reguły.
**interpretacji [.output Rules [t] x]**  |Dane wyjściowe reguły.
**interpretacji [.output.type Rules [t] x]** |Typ danych dane wyjściowe reguły.  Dla interfejsu Academic Knowledge API zawsze będzie to "query".
**interpretacji [.output.value Rules [t] x]**  |Dane wyjściowe reguły. Interfejs Academic Knowledge API to ciąg wyrażenia zapytania, który może być przekazywany do metody Oceń i calchistogram.
**Zostało przerwane** | Wartość true, jeśli upłynął limit czasu żądania.

<br>
#### <a name="example"></a>Przykład:
```
https://westus.api.cognitive.microsoft.com/academic/v1.0/interpret?query=papers by jaime&complete=1&count=2
 ```
<br>Odpowiedź poniżej zawiera dwa pierwsze (ze względu na parametr *count = 2*) najprawdopodobniej interpretacji, kończące danych wejściowych użytkownika częściowe *dokumentach trzyczęściową*: *dokumentach teevan trzyczęściową*  i *dokumentów przez zielony trzyczęściową*.  Uzupełnienia zapytań usługi generowane zamiast biorąc pod uwagę tylko dokładne dopasowania dla autora *trzyczęściową* ponieważ określony w żądaniu *pełną = 1*. Należy pamiętać, że wartość canonical *l "j" zielony* dopasowane za pośrednictwem synonim *zielony Joanna*, zgodnie z analizy.


```JSON
{
  "query": "papers by jaime",
  "interpretations": [
    {
      "logprob": -12.728,
      "parse": "<rule name=\"#GetPapers\">papers by <attr name=\"academic#AA.AuN\">jaime teevan</attr></rule>",
      "rules": [
        {
          "name": "#GetPapers",
          "output": {
            "type": "query",
            "value": "Composite(AA.AuN=='jaime teevan')"
          }
        }
      ]
    },
    {
      "logprob": -12.774,
      "parse": "<rule name=\"#GetPapers\">papers by <attr name=\"academic#AA.AuN\" canonical=\"j l green\">jaime green</attr></rule>",
      "rules": [
        {
          "name": "#GetPapers",
          "output": {
            "type": "query",
            "value": "Composite(AA.AuN=='j l green')"
          }
        }
      ]
    }
  ]
}
```  
<br>Aby pobrać wyniki obiektu interpretacji, użyj *output.value* z **interpretacji** interfejsu API i przekazać go do **oceny** interfejsu API za pośrednictwem *expr*  parametru. W tym przykładzie zapytanie interpretacji pierwszy wygląda tak: 
```
evaluate?expr=Composite(AA.AuN=='jaime teevan')
```
 