---
title: Publikowanie bazy wiedzy, REST, Java
titleSuffix: QnA Maker - Azure Cognitive Services
description: Ten przewodnik Szybki start oparty na protokole REST języka Java przeprowadzi Cię przez proces publikowania bazy wiedzy, który polega na wypchnięciu najnowszej wersji przetestowanej bazy wiedzy do dedykowanego indeksu usługi Azure Search reprezentującego opublikowaną bazę wiedzy. Zostanie również utworzony punkt końcowy, który można wywoływać w aplikacji lub czatbocie.
services: cognitive-services
author: diberry
manager: cgronlun
ms.custom: seodec18
ms.service: cognitive-services
ms.component: qna-maker
ms.topic: quickstart
ms.date: 11/19/2018
ms.author: diberry
ms.openlocfilehash: a115c5180044da1fe66349fefd9c28824fdd2e51
ms.sourcegitcommit: efcd039e5e3de3149c9de7296c57566e0f88b106
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/10/2018
ms.locfileid: "53163960"
---
# <a name="quickstart-publish-a-knowledge-base-in-qna-maker-using-java"></a>Szybki start: Publikowanie bazy wiedzy w usłudze QnA Maker przy użyciu języka Java

Ten przewodnik Szybki start oparty na protokole REST przeprowadzi Cię przez programowe publikowanie bazy wiedzy. Publikowanie wypycha najnowszą wersję bazy wiedzy do dedykowanego indeksu usługi Azure Search i tworzy punkt końcowy, który może być wywoływany w Twojej aplikacji lub czatbocie.

Ten przewodnik Szybki start wywołuje interfejsy API usługi QnA Maker:
* [Publikowanie](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75fe) — ten interfejs API nie wymaga żadnych informacji zawartych w treści żądania.

## <a name="prerequisites"></a>Wymagania wstępne

* [JDK SE](https://aka.ms/azure-jdks) (Java Development Kit, Standard Edition)
* Ten przykład używa [klienta HTTP](http://hc.apache.org/httpcomponents-client-ga/) Apache z projektu HTTP Components. Dodaj następujące biblioteki klienta HTTP Apache do projektu: 
    * httpclient-4.5.3.jar
    * httpcore-4.4.6.jar
    * commons-logging-1.2.jar
* [Visual Studio Code](https://code.visualstudio.com/)
* Musisz mieć [usługę QnA Maker](../How-To/set-up-qnamaker-service-azure.md). Aby uzyskać klucz, wybierz pozycję **Klucze** w obszarze **Zarządzanie zasobami** na pulpicie nawigacyjnym platformy Azure dla zasobu usługi QnA Maker. . 
* Identyfikator bazy wiedzy usługi QnA Maker dostępny w adresie URL w parametrze ciągu zapytania kbid, jak pokazano poniżej.

    ![Identyfikator bazy wiedzy usługi QnA Maker](../media/qnamaker-quickstart-kb/qna-maker-id.png)

    Jeśli nie masz jeszcze bazy wiedzy, możesz utworzyć przykładową bazę na potrzeby tego podręcznika Szybki start: [Tworzenie nowej bazy wiedzy](create-new-kb-csharp.md).

> [!NOTE] 
> Pliki kompletnego rozwiązania są dostępne w [repozytorium GitHub **Azure-Samples/cognitive-services-qnamaker-java**](https://github.com/Azure-Samples/cognitive-services-qnamaker-java/tree/master/documentation-samples/quickstarts/publish-knowledge-base).

## <a name="create-a-java-file"></a>Tworzenie pliku języka Java

Otwórz program VSCode i utwórz nowy plik o nazwie `PublishKB.java`.

## <a name="add-the-required-dependencies"></a>Dodawanie wymaganych zależności

Na początku pliku `PublishKB.java`, powyżej klasy, dodaj następujące wiersze, aby dodać niezbędne zależności do projektu:

[!code-java[Add the required dependencies](~/samples-qnamaker-java/documentation-samples/quickstarts/publish-knowledge-base/PublishKB.java?range=1-13 "Add the required dependencies")]

## <a name="create-publishkb-class-with-main-method"></a>Tworzenie klasy PublishKB z metodą main

Poniżej zależności dodaj następującą klasę:

```Go
public class PublishKB {

    public static void main(String[] args) 
    {
    }
}
```

## <a name="add-required-constants"></a>Dodawanie wymaganych stałych

W metodzie **main** dodaj wymagane stałe na potrzeby dostępu do usługi QnA Maker. Przedstawione wartości zastąp własnymi.

[!code-java[Add the required constants](~/samples-qnamaker-java/documentation-samples/quickstarts/publish-knowledge-base/PublishKB.java?range=27-30 "Add the required constants")]

## <a name="add-post-request-to-publish-knowledge-base"></a>Dodawanie żądania POST w celu publikowania bazy wiedzy

Poniżej wymaganych stałych dodaj następujący kod, który wysyła żądanie HTTPS do interfejsu API usługi QnA Maker, aby opublikować bazę wiedzy, oraz odbiera odpowiedź:

[!code-java[Add a POST request to publish knowledge base](~/samples-qnamaker-java/documentation-samples/quickstarts/publish-knowledge-base/PublishKB.java?range=32-44 "Add a POST request to publish knowledge base")]

W przypadku pomyślnego publikowania wywołanie interfejsu API zwraca stan 204 bez jakiejkolwiek zawartości w treści odpowiedzi. Ten kod dodaje zawartość dla odpowiedzi stanu 204.

W przypadku wszystkich innych odpowiedzi są one zwracane w niezmienionej postaci.

## <a name="build-and-run-the-program"></a>Kompilowanie i uruchamianie programu

Skompiluj i uruchom program z poziomu wiersza polecenia. Automatycznie wyśle on żądanie do interfejsu API usługi QnA Maker, a następnie wyświetli informacje w oknie konsoli.

1. Skompiluj plik:

    ```bash
    javac -cp "lib/*" PublishKB.java
    ```

1. Uruchom plik:

    ```bash
    java -cp ".;lib/*" PublishKB
    ```

[!INCLUDE [Clean up files and knowledge base](../../../../includes/cognitive-services-qnamaker-quickstart-cleanup-resources.md)] 

## <a name="next-steps"></a>Następne kroki

Po opublikowaniu bazy wiedzy potrzebny jest [adres URL punktu końcowego do wygenerowania odpowiedzi](../Tutorials/create-publish-answer.md#generating-an-answer).  

> [!div class="nextstepaction"]
> [QnA Maker (V4) REST API Reference (Dokumentacja interfejsu API REST usługi QnA Maker w wersji 4)](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75ff)