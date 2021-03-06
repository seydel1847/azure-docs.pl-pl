---
title: Plik dyrektywy include
description: Plik dyrektywy include
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mtillman
editor: ''
ms.service: active-directory
ms.devlang: na
ms.topic: include
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 09/13/2018
ms.author: andret
ms.custom: include file
ms.openlocfilehash: 9bc8f30d2bbf6a084ad680306da9b1e330d488e3
ms.sourcegitcommit: c2c279cb2cbc0bc268b38fbd900f1bac2fd0e88f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/24/2018
ms.locfileid: "49988338"
---
# <a name="sign-in-users-and-call-the-microsoft-graph-from-an-android-app"></a>Logowania użytkowników i wywoływania usługi Microsoft Graph w aplikacji systemu Android

W tym samouczku dowiesz się, jak utworzyć aplikację dla systemu Android i zintegrować ją z platformą Microsoft identity. Ściślej mówiąc ta aplikacja będzie logowania użytkownika, uzyskania tokenu dostępu do wywołania interfejsu API programu Microsoft Graph i dokonać podstawowego żądania interfejsu API programu Microsoft Graph.  

Po zakończeniu przewodnika, aplikacja będzie akceptować logowania osobistych kont Microsoft (w tym outlook.com, live.com i inne) i służbowego konta z firmy lub organizacji, która używa usługi Azure Active Directory.

## <a name="how-the-sample-app-generated-by-this-guide-works"></a>Jak działa przykładowej aplikacji wygenerowane przez ten przewodnik

![Jak działa ten przykład](media/active-directory-develop-guidedsetup-android-intro/android-intro.png)

Aplikacja w tym przykładzie będzie logować użytkowników i Pobierz dane w ich imieniu.  Te dane będą uzyskiwać dostęp za pośrednictwem zdalnego interfejsu API (Microsoft interfejsu API programu Graph w tym przypadku) wymaga autoryzacji, która jest również chroniony przez platforma tożsamości firmy Microsoft.

Więcej szczegółów:

* Aplikacja uruchomi strony sieci web do logowania użytkownika.
* Aplikacja zostanie wystawiony token dostępu do interfejsu API programu Microsoft Graph.
* Token dostępu zostaną uwzględnione w żądaniu HTTP do interfejsu API sieci web.
* Przetworzenie odpowiedzi programu Microsoft Graph.

W tym przykładzie używa biblioteki Microsoft Authentication dla systemu Android (MSAL) do koordynowania i pomagając przy użyciu uwierzytelniania Biblioteka MSAL automatycznie odnowić tokenów, dostarczanie SSO między innymi aplikacjami na urządzeniu, ułatwiają zarządzanie konta i obsługa większości przypadków dostępu warunkowego.

## <a name="prerequisites"></a>Wymagania wstępne

* Ta instalacja z przewodnikiem używa systemu Android Studio 3.0.
* System android 21 lub nowszy jest wymagany (25 + jest zalecane).
* Google Chrome lub przeglądarki sieci web, która używa kart niestandardowych jest wymagana dla tej wersji biblioteki MSAL dla systemu Android.

## <a name="library"></a>Biblioteka

W tym przewodniku używane są następujące biblioteki uwierzytelniania:

|Biblioteka|Opis|
|---|---|
|[com.microsoft.identity.client](http://javadoc.io/doc/com.microsoft.identity.client/msal)|Microsoft Authentication Library (MSAL)|
