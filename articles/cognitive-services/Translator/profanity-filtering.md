---
title: Filtrowanie wulgaryzmów — interfejs API tekstu usługi Translator
titlesuffix: Azure Cognitive Services
description: Użyj wulgaryzmów filtrowanie danych na interfejs API tekstu usługi Translator.
services: cognitive-services
author: Jann-Skotdal
manager: cgronlun
ms.service: cognitive-services
ms.component: translator-text
ms.topic: conceptual
ms.date: 12/14/2017
ms.author: v-jansko
ms.openlocfilehash: 4154950cf8d8b6ec2e47a9f8100cb7983ac127bf
ms.sourcegitcommit: ccdea744097d1ad196b605ffae2d09141d9c0bd9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/23/2018
ms.locfileid: "49648041"
---
# <a name="add-profanity-filtering-with-the-translator-text-api"></a>Dodaj wulgaryzmów filtrowanie przy użyciu interfejsu API tłumaczenia tekstu

Zazwyczaj usługa Translator zachowuje wulgaryzmów, który znajduje się w źródle w tłumaczeniu. Stopień wulgaryzmów i kontekst, który sprawia, że wyrazy obsceniczne różnią się od kultury. W wyniku stopień wulgaryzmów w języku docelowym może być większy lub mniejsze.

Jeśli chcesz uniknąć wulgaryzmów w tłumaczeniu, nawet jeśli wulgaryzmów znajduje się w tekście źródłowym, należy użyć wulgaryzmów dostępną w metodzie Translate() opcję filtrowania. Ta opcja umożliwia użytkownikowi oznaczona za pomocą odpowiednich tagów wybierz, czy chcesz zobaczyć wulgaryzmów usunięte, lub wykonać nie podjęto żadnej akcji.

Metoda Translate() przyjmuje parametr "Opcje", który zawiera nowy element "ProfanityAction". Akceptowane wartości ProfanityAction to "NoAction", "Oznaczone" i "Usunięte".

## <a name="accepted-values-of-profanityaction-and-examples"></a>Dopuszczalne wartości ProfanityAction i przykłady
|Wartość ProfanityAction | Akcja | Przykład: Source — japoński | Przykład: Docelowy — angielski|
| :---|:---|:---|:---|
| NoAction | Domyślne. Taka sama jak nie Ustawianie opcji. Wulgaryzmów przekazuje ze źródła do docelowego. | 彼は変態です。 | Jest on ostatnim draniem. |
| Oznaczone jako | Obsceniczne wyrazy są ujęte w znaczników XML \<wulgaryzmów >... \</profanity >. | 彼は変態です。 | Jest on \<wulgaryzmów > jerk\</profanity >. |
| Usunięto | Obsceniczne wyrazy są usuwane z danych wyjściowych bez zastępowania. | 彼は。 | Jest on. |

## <a name="next-steps"></a>Kolejne kroki
> [!div class="nextstepaction"]
> [Zastosuj wulgaryzmów filtrowanie przy użyciu wywołania interfejsu API usługi Translator](reference/v3-0-translate.md)
