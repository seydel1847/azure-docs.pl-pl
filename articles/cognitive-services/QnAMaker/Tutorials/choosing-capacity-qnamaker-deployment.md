---
title: Pojemność zasobów dla wdrożenia — QnA Maker
titleSuffix: Azure Cognitive Services
description: Przed przystąpieniem do tworzenia usługi QnA Maker możesz zdecydować, którą warstwę usług powyżej jest odpowiednia dla Ciebie.
services: cognitive-services
author: tulasim88
manager: cgronlun
ms.service: cognitive-services
ms.component: qna-maker
ms.topic: article
ms.date: 09/12/2018
ms.author: tulasim
ms.custom: seodec18
ms.openlocfilehash: 9e197929ce08f4e0c665f96d1c4ddbd382fdfb22
ms.sourcegitcommit: 9fb6f44dbdaf9002ac4f411781bf1bd25c191e26
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/08/2018
ms.locfileid: "53084463"
---
# <a name="choosing-capacity-for-your-qna-maker-deployment"></a>Wybieranie pojemności dla danego wdrożenia usługi QnA Maker

Usługa QnA Maker przyjmuje zależność dla trzech zasobów platformy Azure:
1.  App Service (dla środowiska wykonawczego)
2.  Usługa Azure Search (do przechowywania znacznie)
3.  App Insights (opcjonalnie, do przechowywania dzienniki czatu i telemetrii)

Przed przystąpieniem do tworzenia usługi QnA Maker możesz zdecydować, którą warstwę usług powyżej jest odpowiednia dla Ciebie. 

Zwykle istnieją trzy parametry, które należy wziąć pod uwagę:
1. **Przepływność należy z niej**: Wybierz odpowiedni [Plan usługi App](https://azure.microsoft.com/pricing/details/app-service/plans/) dla usługi App service zgodnie z potrzebami. Możesz [skalowanie w górę](https://docs.microsoft.com/azure/app-service/web-sites-scale) lub w dół aplikacji. To powinien również mieć wpływ na wybór jednostki SKU usługi Azure Search, zobacz więcej szczegółów [tutaj](https://docs.microsoft.com/azure/search/search-sku-tier).

2. **Rozmiaru i liczby baz wiedzy**: wybierz odpowiednie [Azure wyszukiwanie jednostek SKU](https://azure.microsoft.com/pricing/details/search/) dla danego scenariusza. N-1, baz wiedzy można publikować w konkretnej warstwy, gdzie N to maksymalna liczba indeksów dozwolone w ramach warstwy. Sprawdź również maksymalnego rozmiaru i liczby dokumentów dozwolone na warstwę.

3. **Liczba dokumentów jako źródła**: bezpłatna jednostka SKU usługi zarządzania usługi QnA Maker ogranicza liczbę dokumentów można zarządzać za pośrednictwem portalu i interfejsów API do 3 (1 MB rozmiar każdego). Standardowa jednostka SKU nie ma limitów liczby dokumentów, którymi można zarządzać. Zobacz więcej szczegółów [tutaj](https://aka.ms/qnamaker-pricing).

W poniższej tabeli przedstawiono niektóre wytyczne wysokiego poziomu.

|                        | Usługa QnA Maker zarządzania | App Service | Azure Search | Ograniczenia                      |
| ---------------------- | -------------------- | ----------- | ------------ | -------------------------------- |
| Eksperymentowanie        | Bezpłatna jednostka SKU             | Warstwa Bezpłatna   | Warstwa Bezpłatna    | Publikowanie do 2 artykułów bazy wiedzy, rozmiar 50 MB  |
| Środowisko programistyczne/testowe   | Standardowy SKU         | Udostępniona      | Podstawowa        | Publikowanie do 14 artykułów bazy wiedzy, rozmiar 2 GB    |
| Środowiska produkcyjnego | Standardowy SKU         | Podstawowa       | Standardowa (Standard)     | Publikowanie do 49 artykułów bazy wiedzy, rozmiar 25 GB |

Dla uaktualnienie stosie usługi QnA Maker, zobacz [uaktualnienia usługi QnA Maker](../How-To/upgrade-qnamaker-service.md).

## <a name="next-steps"></a>Kolejne kroki

> [!div class="nextstepaction"]
> [Uaktualnianie usługi QnA Maker](../How-To/upgrade-qnamaker-service.md)
