---
title: Usługa Azure AD v2 Windows Desktop wprowadzenie pracę - Config | Dokumentacja firmy Microsoft
description: Jak aplikacji .NET Desktop Windows (XAML) można uzyskać token dostępu i wywołać interfejs API chroniony przez punkt końcowy w wersji 2 usługi Azure Active Directory.
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mtillman
editor: ''
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 47d62b5ea49205a5e639d620d78466e7e4a66bca
ms.sourcegitcommit: 56d20d444e814800407a955d318a58917e87fe94
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/29/2018
ms.locfileid: "52581412"
---
# <a name="add-the-applications-registration-information-to-your-app"></a>Dodaj informacje o rejestracji aplikacji do aplikacji
W tym kroku należy dodać identyfikator aplikacji do projektu.

1.  Otwórz `App.xaml.cs` i Zastąp wiersz zawierający `ClientId` za pomocą:

```csharp
private static string ClientId = "[Enter the application Id here]";
```

### <a name="what-is-next"></a>Co to jest dalej

[!INCLUDE [Test and Validate](../../../../includes/active-directory-develop-guidedsetup-windesktop-test.md)]
