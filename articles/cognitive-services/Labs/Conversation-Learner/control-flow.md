---
title: Przepływ sterowania uczeń konwersacji — Microsoft Cognitive Services | Dokumentacja firmy Microsoft
titleSuffix: Azure
description: Dowiedz się więcej na temat formantów flow uczeń konwersacji.
services: cognitive-services
author: v-jaswel
manager: nolachar
ms.service: cognitive-services
ms.component: conversation-learner
ms.topic: article
ms.date: 04/30/2018
ms.author: v-jaswel
ms.openlocfilehash: 8007e9e9fe2f404b4d702471610ff76047f7ed86
ms.sourcegitcommit: 295babdcfe86b7a3074fd5b65350c8c11a49f2f1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/27/2018
ms.locfileid: "53790932"
---
## <a name="control-flow"></a>Przepływ sterowania

W tym dokumencie opisano przepływ sterowania uczeń konwersacji (CL) w postaci wyświetlanej w poniższym diagramie.

![](media/controlflow.PNG)

1. Użytkownik wprowadza termin lub frazę w bot, na przykład "co to jest pogody w Seattle?"
1. CL przekazuje dane wejściowe użytkownika do modelu uczenia maszynowego, która wyodrębnia jednostek
    - Ten model jest kompilowane przez uczeń konwersacji i hostowanych przez www.luis.ai
1. Wyodrębnione dowolnej jednostki, a jego dane wprowadzane przez użytkownika tekst, są przekazywane do metody wywołania zwrotnego wykrywania jednostki w kodzie botów.
    - Ten kod może wartości jednostki manipulowania nimi/set/clear
1. Sieć neuronowa CL następnie pobiera dane wyjściowe działania funkcji wydobywania podmiotów danych wejściowych użytkownika, i wyniki wszystkich akcji określonych w robota
    - W tym przykładzie najwyższy akcji prawdopodobieństwo jest zapewnienie prognozę pogody:

    ![](media/controlflow_forecast.PNG)

1. Wybranej akcji, w tym przypadku wymaga wywołania interfejsu API, aby pobrać prognozę pogody. 
1. Ten interfejs API, który został zarejestrowany przy użyciu CL. Następnie wywoływana jest metoda AddCallback.  Wynik tego interfejsu API jest zwracany do użytkownika jako wiadomość — na przykład Sunny z wysokim 67.
1. Następnie wykonano wywołanie dotyczące sieci neuronowych Aby określić następne działanie w poprzednim kroku.
1. Sieć neuronowa następnie przewiduje następny zestaw możliwych działań i wybranej akcji są prezentowane użytkownikowi, w tym przypadku "Czymkolwiek?"

## <a name="next-steps"></a>Kolejne kroki

> [!div class="nextstepaction"]
> [Jak do nauki o uczeń konwersacji ](./how-to-teach-cl.md)
