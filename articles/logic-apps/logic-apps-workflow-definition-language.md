---
title: Odwołanie do schematu dla język definicji przepływów pracy — Azure Logic Apps | Dokumentacja firmy Microsoft
description: Zapisz definicje niestandardowego przepływu pracy dla usługi Azure Logic Apps za pomocą języka definicji przepływu pracy
services: logic-apps
ms.service: logic-apps
author: ecfan
ms.author: estfan
manager: jeconnoc
ms.topic: reference
ms.date: 04/30/2018
ms.reviewer: klam, LADocs
ms.suite: integration
ms.openlocfilehash: d5dadd054f95e61626942a1cab7d95ba8c9182e1
ms.sourcegitcommit: 30c7f9994cf6fcdfb580616ea8d6d251364c0cd1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2018
ms.locfileid: "42062067"
---
# <a name="schema-reference-for-workflow-definition-language-in-azure-logic-apps"></a>Odwołanie do schematu dla język definicji przepływów pracy w usłudze Azure Logic Apps

Podczas tworzenia przepływu pracy aplikacji logiki za pomocą [usługi Azure Logic Apps](../logic-apps/logic-apps-overview.md), podstawową definicję Twój przepływ pracy w tym artykule opisano rzeczywiste logikę, która jest uruchamiana dla aplikacji logiki. Ten opis jest zgodna to struktura, która została zdefiniowana i zweryfikowane przez schemat języka definicji przepływu pracy, który używa [JavaScript Object Notation (JSON)](https://www.json.org/). 
  
## <a name="workflow-definition-structure"></a>Struktura definicji przepływu pracy

Definicja przepływu pracy ma co najmniej jeden wyzwalacz, który tworzy wystąpienie aplikacji logiki, a także co najmniej jednej akcji, których Twoja aplikacja logiki działa. 

Poniżej przedstawiono ogólną strukturę dla definicji przepływu pracy:  
  
```json
"definition": {
  "$schema": "<workflow-definition-language-schema-version>",
  "contentVersion": "<workflow-definition-version-number>",
  "parameters": { "<workflow-parameter-definitions>" },
  "triggers": { "<workflow-trigger-definitions>" },
  "actions": { "<workflow-action-definitions>" },
  "outputs": { "<workflow-output-definitions>" }
}
```
  
| Element | Wymagane | Opis | 
|---------|----------|-------------| 
| definicja | Yes | Element początkowy dla swojej definicji przepływu pracy | 
| $schema | Tylko wtedy, gdy zewnętrznie odwołujące się do definicji przepływu pracy | Lokalizacja pliku schematu JSON, który opisuje wersję język definicji przepływów pracy, który można znaleźć tutaj: <p>`https://schema.management.azure.com/schemas/2016-06-01/Microsoft.Logic.json`</p> |   
| contentversion — | Nie | Numer wersji dla definicji przepływu pracy, czyli "1.0.0.0" domyślnie. Aby ułatwić identyfikowanie i Potwierdź poprawną definicję, wdrażając przepływu pracy, należy określić wartość do użycia. | 
| parameters | Nie | Definicje dla jednego lub więcej parametrów, które przekazują dane do Twojego przepływu pracy <p><p>Parametry maksymalna: 50 | 
| Wyzwalacze | Nie | Definicje dla co najmniej jeden wyzwalacze, które wystąpienia przepływu pracy. Można zdefiniować więcej niż jeden wyzwalacz, ale tylko za pomocą języka definicji przepływu pracy, nie wizualnie za pomocą projektanta aplikacji logiki. <p><p>Wyzwalacze maksymalna: 10 | 
| Akcje | Nie | Definicje dla co najmniej jedną akcję do wykonania w czasie wykonywania przepływu pracy <p><p>Maksymalną liczbę akcji: 250 | 
| wyjścia | Nie | Definicje dla danych wyjściowych, które zwracają z przebiegu przepływu pracy <p><p>Dane wyjściowe maksymalna: 10 |  
|||| 

## <a name="parameters"></a>Parametry

W `parameters` sekcji, określ wszystkie parametry przepływu pracy używanych przez aplikację logiki we wdrożeniu do akceptowania dane wejściowe. Deklaracji parametru i wartości parametrów są wymagane podczas wdrażania. Przed za pomocą tych parametrów w innych częściach przepływu pracy, upewnij się, że zadeklarować wszystkie parametry w tych sekcjach. 

Poniżej przedstawiono ogólną strukturę dla definicji parametru:  

```json
"parameters": {
  "<parameter-name>": {
    "type": "<parameter-type>",
    "defaultValue": "<default-parameter-value>",
    "allowedValues": [ <array-with-permitted-parameter-values> ],
    "metadata": { 
      "key": { 
        "name": "<key-value>"
      } 
    }
  }
},
```

| Element | Wymagane | Typ | Opis |  
|---------|----------|------|-------------|  
| type | Yes | int, float, string, securestring, bool, tablicę, obiekt JSON, secureobject <p><p>**Uwaga**: w przypadku wszystkich haseł, kluczy i wpisów tajnych, użyj `securestring` i `secureobject` typów, ponieważ `GET` operacji nie zwraca tych typów. | Typ parametru |
| defaultValue | Nie | Takie same jak `type` | Domyślna wartość parametru, jeśli wartość nie zostanie określona, gdy tworzy wystąpienie przepływu pracy | 
| allowedValues | Nie | Takie same jak `type` | Tablica wartości akceptujące parametr |  
| metadane | Nie | Obiekt JSON | Inne szczegóły parametrów, na przykład nazwę lub czytelny opis dla swojej aplikacji logiki lub danych czasu projektowania używanych przez program Visual Studio lub innych narzędzi |  
||||

## <a name="triggers-and-actions"></a>Wyzwalacze i akcje  

W definicji przepływu pracy `triggers` i `actions` sekcje definiują wywołania, które występują podczas wykonywania Twój przepływ pracy. Informacje o składni i dowiedzieć się więcej o tych sekcji, zobacz [wyzwalaczy przepływu pracy i działań](../logic-apps/logic-apps-workflow-actions-triggers.md).
  
## <a name="outputs"></a>Dane wyjściowe 

W `outputs` sekcji, definiują dane, które może zwracać przepływu pracy, po zakończeniu uruchamiania. Na przykład aby śledzić stan określonego lub wartości z poszczególnymi uruchomieniami, określić czy dane wyjściowe przepływu pracy zwraca dane. 

> [!NOTE]
> Podczas odpowiadania na żądania przychodzące z interfejsu API REST usługi, nie używaj `outputs`. Zamiast tego należy użyć `Response` typ akcji. Aby uzyskać więcej informacji, zobacz [wyzwalaczy przepływu pracy i działań](../logic-apps/logic-apps-workflow-actions-triggers.md).

Poniżej przedstawiono ogólną strukturę definicji danych wyjściowych dla: 

```json
"outputs": {
  "<key-name>": {  
    "type": "<key-type>",  
    "value": "<key-value>"  
  }
} 
```

| Element | Wymagane | Typ | Opis | 
|---------|----------|------|-------------| 
| <*Nazwa klucza*> | Yes | Ciąg | Nazwa klucza dla produktu wyjściowego zwracają wartość |  
| type | Yes | int, float, string, securestring, bool, tablicę, obiekt JSON | Typ dla wartości zwracanej w danych wyjściowych | 
| wartość | Yes | Takie same jak `type` | Wartość zwracana w danych wyjściowych |  
||||| 

Aby uzyskać dane wyjściowe z przebiegu przepływu pracy, Przejrzyj historię uruchomień aplikacji logiki i szczegółowe informacje w witrynie Azure portal lub [interfejsu API REST przepływu pracy](https://docs.microsoft.com/rest/api/logic/workflows). Można również przekazać dane wyjściowe z systemami zewnętrznymi, na przykład usługa Power BI, dzięki czemu można tworzyć pulpity nawigacyjne. 

<a name="expressions"></a>

## <a name="expressions"></a>Wyrażenia

Za pomocą formatu JSON może mieć wartości literału, które istnieją w czasie projektowania, na przykład:

```json
"customerName": "Sophia Owen", 
"rainbowColors": ["red", "orange", "yellow", "green", "blue", "indigo", "violet"], 
"rainbowColorsCount": 7 
```

Również może mieć wartości, które nie istnieją do czasu wykonywania. Do reprezentowania tych wartości, można użyć *wyrażenia*, które są oceniane w czasie wykonywania. Wyrażenie jest sekwencji, który może zawierać jeden lub więcej [funkcje](#functions), [operatory](#operators), zmiennych, jawne wartości lub stałe. W definicji przepływu pracy, można użyć wyrażenia dowolnym miejscu w wartości ciągu JSON przez dodanie przedrostka wyrażenia ze znakiem w (\@). Podczas obliczania wyrażenia, która reprezentuje wartość JSON, treści wyrażenia jest wyodrębniany, usuwając \@ znaków i zawsze skutkuje inną wartość JSON. 

Na przykład uprzednio zdefiniowany `customerName` właściwości, można pobrać wartości właściwości, za pomocą [parameters()](../logic-apps/workflow-definition-language-functions-reference.md#parameters) działać w wyrażeniach, a następnie przypisać tę wartość do `accountName` właściwości:

```json
"customerName": "Sophia Owen", 
"accountName": "@parameters('customerName')"
```

*Interpolacja ciągów* również pozwala używać wielu wyrażeń wewnątrz ciągów, które zostaną opakowane przy \@ znaków i nawiasy klamrowe ({}). Poniżej przedstawiono składnię:

```json
@{ "<expression1>", "<expression2>" }
```

Wynik to zawsze ciąg wprowadzania tej możliwości podobne do `concat()` funkcji, na przykład: 

```json
"customerName": "First name: @{parameters('firstName')} Last name: @{parameters('lastName')}"
```

Jeśli masz ciąg literału, który rozpoczyna się od \@ znak, prefiks \@ znak z inną \@ znak jako znak ucieczki: \@\@

Poniższe przykłady pokazują, jak są obliczane wyrażenia:

| Wartość JSON | Wynik |
|------------|--------| 
| "Sophia Owen" | Zwraca następujące znaki: "Sophia Owen" |
| "tablica [1]" | Zwraca następujące znaki: "array [1]" |
| "\@\@" | Zwraca te znaki jako ciąg jednego znaku: "\@" |   
| " \@" | Zwracają te znaki jako ciąg dwóch znaków: " \@" |
|||

W poniższych przykładach Załóżmy, że należy zdefiniować "myBirthMonth" równa się "Stycznia" i "myAge" równą liczbie 42:  
  
```json
"myBirthMonth": "January",
"myAge": 42
```

Poniższe przykłady pokazują, jak są obliczane następujących wyrażeń:

| Wyrażenie JSON | Wynik |
|-----------------|--------| 
| "\@parameters('myBirthMonth')" | Zwraca następujący ciąg: "Stycznia" |  
| "\@{parameters('myBirthMonth')}" | Zwraca następujący ciąg: "Stycznia" |  
| "\@parameters('myAge')" | Zwraca to numer: 42 |  
| "\@{parameters('myAge')}" | Zwraca ten numer jako ciąg znaków: "42" |  
| "Mój wiek to \@{parameters('myAge')}" | Zwraca następujący ciąg: "Mój wiek to 42" |  
| "\@concat ("Mój wiek to", string(parameters('myAge')))" | Zwraca następujący ciąg: "Mój wiek to 42" |  
| "Mój wiek to \@ \@{parameters('myAge')}" | Ten ciąg, który zawiera wyrażenie zwraca: "Mój wiek to \@{parameters('myAge')}" | 
||| 

Podczas pracy wizualnie w Projektancie aplikacji logiki, możesz utworzyć wyrażenia przez Konstruktor wyrażeń na przykład: 

![Projektant aplikacji logiki > Konstruktor wyrażeń](./media/logic-apps-workflow-definition-language/expression-builder.png)

Gdy wszystko będzie gotowe, znajduje się wyrażenie dla odpowiednich właściwości w definicji przepływu pracy, na przykład, `searchQuery` właściwości w tym miejscu:

```json
"Search_tweets": {
  "inputs": {
    "host": {
      "connection": {
       "name": "@parameters('$connections')['twitter']['connectionId']"
      }
    }
  },
  "method": "get",
  "path": "/searchtweets",
  "queries": {
    "maxResults": 20,
    "searchQuery": "Azure @{concat('firstName','', 'LastName')}"
  }
},
```

<a name="operators"></a>

## <a name="operators"></a>Operatory

W [wyrażeń](#expressions) i [funkcje](#functions), operatory wykonywania określonych zadań, takich jak odwołanie do właściwości lub wartość w tablicy. 

| Operator | Zadanie | 
|----------|------|
| ' | Aby użyć literału ciągu jako dane wejściowe lub w wyrażeniach i funkcje, opakowywanie ciąg tylko pojedynczy cudzysłów, na przykład `'<myString>'`. Nie należy używać podwójnego cudzysłowu (""), które powodują konflikt z formatowaniem JSON wokół całe wyrażenie. Na przykład: <p>**Tak**: length('Hello') </br>**Nie**: length("Hello") <p>Jeśli przekazujesz, tablic lub liczby, nie trzeba zawijanie znaków interpunkcyjnych. Na przykład: <p>**Tak**: długość ([1, 2, 3]) </br>**Nie**: długość ("[1, 2, 3]") | 
| [] | Aby odwołać się do wartości w określonym położeniu (indeks) w tablicy, Użyj nawiasów kwadratowych. Na przykład, aby uzyskać drugi element w tablicy: <p>`myArray[1]` | 
| . | Aby odwoływać się do właściwości w obiekcie, użyj operatora kropki. Na przykład, aby uzyskać `name` właściwość `customer` obiekt JSON: <p>`"@parameters('customer').name"` | 
| ? | Odwoływanie się do wartości null właściwości w obiekcie bez błędów środowiska uruchomieniowego, użyj operatora znaku zapytania. Na przykład do obsługi o wartości null dane wyjściowe z wyzwalaczem, możesz użyć tego wyrażenia: <p>`@coalesce(trigger().outputs?.body?.<someProperty>, '<property-default-value>')` | 
||| 

<a name="functions"></a>

## <a name="functions"></a>Funkcje

Niektóre wyrażenia, Uzyskaj ich wartości z akcji środowiska uruchomieniowego, które jeszcze nie istnieje podczas uruchamiania aplikacji logiki. Aby odwołać się i pracować z tych wartości w wyrażeniach, można użyć [ *funkcje* ](../logic-apps/workflow-definition-language-functions-reference.md) zapewniająca język definicji przepływów pracy. 

## <a name="next-steps"></a>Kolejne kroki

* Dowiedz się więcej o [język definicji przepływów pracy akcji i wyzwalaczy](../logic-apps/logic-apps-workflow-actions-triggers.md)
* Dowiedz się więcej o programowe tworzenie i zarządzanie aplikacjami logiki za pomocą [interfejsu API REST przepływu pracy](https://docs.microsoft.com/rest/api/logic/workflows)
