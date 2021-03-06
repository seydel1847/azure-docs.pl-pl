---
title: Tworzenie nowej aplikacji
titleSuffix: Language Understanding - Azure Cognitive Services
description: Utwórz aplikacje i zarządzaj nimi na stronie sieci Web Language Understanding (LUIS).
services: cognitive-services
author: diberry
manager: cgronlun
ms.custom: seodec18
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 09/10/2018
ms.author: diberry
ms.openlocfilehash: ddfee80c67c22c7c6016ed87dc17925c91637d21
ms.sourcegitcommit: 549070d281bb2b5bf282bc7d46f6feab337ef248
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/21/2018
ms.locfileid: "53714002"
---
# <a name="create-a-new-luis-app-in-the-luis-portal"></a>Utwórz nową aplikację usługi LUIS w portalu usługi LUIS
Istnieje kilka sposobów, aby utworzyć aplikację usługi LUIS. Można utworzyć aplikację usługi LUIS w [LUIS](https://www.luis.ai) portalu lub za pomocą usługi LUIS tworzenia [interfejsów API](https://westus.dev.cognitive.microsoft.com/docs/services/5890b47c39e2bb17b84a55ff/operations/5890b47c39e2bb052c5b9c2f).

## <a name="using-the-luis-portal"></a>Za pomocą portalu usługi LUIS
Można utworzyć nową aplikację w portalu usługi LUIS na kilka sposobów:

* Rozpocznij od pusta aplikacja i tworzyć intencji, wypowiedzi i jednostek.
* Start z pustą aplikacją, a następnie dodaj [ze wstępnie utworzonych domen](luis-how-to-use-prebuilt-domains.md).
* Importowanie aplikacji usługi LUIS z pliku JSON, który zawiera już intencji, wypowiedzi i jednostek.

## <a name="using-the-authoring-apis"></a>Za pomocą tworzenia interfejsów API
Można utworzyć nową aplikację za pomocą tworzenia interfejsów API na kilka sposobów:

* [Rozpocznij](https://westus.dev.cognitive.microsoft.com/docs/services/5890b47c39e2bb17b84a55ff/operations/5890b47c39e2bb052c5b9c2f) z pustą aplikację i utworzyć intencji, wypowiedzi i jednostek.
* [Rozpocznij](https://westus.dev.cognitive.microsoft.com/docs/services/5890b47c39e2bb17b84a55ff/operations/59104e515aca2f0b48c76be5) przy użyciu wbudowanych domeny.  


<a name="export-app"></a>
<a name="import-new-app"></a>
<a name="delete-app"></a>
 

## <a name="create-new-app-in-luis"></a>Utwórz nową aplikację w usługi LUIS

1. Na **Moje aplikacje** wybierz opcję **Utwórz nową aplikację**.

    ![Lista aplikacji LUIS](./media/luis-create-new-app/apps-list.png)


2. W oknie dialogowym Nazwa aplikacji "TravelAgent".

    ![Utwórz nowe okno dialogowe aplikacji](./media/luis-create-new-app/create-app.png)

3. Wybierz Twojej kulturze aplikacji (TravelAgent aplikacji, wybierz język angielski), a następnie wybierz pozycję **gotowe**. 

    > [!NOTE]
    > Kultury nie można zmienić po utworzeniu aplikacji. 


## <a name="next-steps"></a>Kolejne kroki

Pierwsze zadanie w aplikacji jest [Dodawanie intencji](luis-how-to-add-intents.md).