---
title: Lista zgodności usługi Azure AD z usługami federacyjnymi
description: Ta strona zawiera dostawców tożsamości firm innych niż Microsoft, które mogą służyć do implementowania logowania jednokrotnego.
services: active-directory
documentationcenter: ''
author: billmath
manager: mtillman
editor: curtand
ms.assetid: 22c8693e-8915-446d-b383-27e9587988ec
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2018
ms.component: hybrid
ms.author: billmath
ms.openlocfilehash: 4a31e7ed12e75bd7dee3d53a8d650179d8e118d8
ms.sourcegitcommit: cf606b01726df2c9c1789d851de326c873f4209a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/19/2018
ms.locfileid: "46310982"
---
# <a name="azure-ad-federation-compatibility-list"></a>Lista zgodności usługi Azure AD z usługami federacyjnymi
Usługa Azure Active Directory zawiera logowania jednokrotnego i rozszerzone zabezpieczenia dostępu do aplikacji dla usługi Office 365 i innych usług Online firmy Microsoft dla implementacji tylko w chmurze i hybrydowych, bez konieczności dowolnego rozwiązania innych firm. Usługi Office 365, takich jak większość usług Online firmy Microsoft, jest zintegrowana z usługą Azure Active Directory dla usług katalogowych, uwierzytelniania i autoryzacji. Usługa Azure Active Directory udostępnia logowanie jednokrotne do tysięcy aplikacji SaaS i aplikacje sieci web w środowisku lokalnym. Zobacz Azure Active Directory [galerii aplikacji](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps) obsługiwanych aplikacji SaaS. 

## <a name="idp-validation"></a>Weryfikacja tożsamości
Jeśli Twoja organizacja korzysta z rozwiązania Federacji innej firmy, możesz skonfigurować logowanie jednokrotne dla lokalnych użytkowników usługi Active Directory za pomocą usług Online firmy Microsoft, takich jak Office 365 rozwiązania do Federacji innej firmy jest zgodna z platformą Azure Usługi Active Directory.  Masz pytania dotyczące zgodności skontaktuj się z dostawcą tożsamości.  Jeśli chcesz wyświetlić listę dostawców tożsamości, które wcześniej zostały przetestowane na zgodność z usługą Azure AD przez firmę Microsoft, kliknij przycisk [tutaj](https://www.microsoft.com/download/details.aspx?id=56843). 

>[!NOTE]
>Firma Microsoft udostępnia już testy poprawności w celu dostawców niezależnych tożsamości dla zgodności z usługą Azure Active Directory. Jeśli chcesz przetestować współdziałania w ramach produktu można znaleźć te [wytycznych](https://www.microsoft.com/download/details.aspx?id=56843). 

## <a name="next-steps"></a>Następne kroki

- [Integrowanie katalogów lokalnych z usługą Azure Active Directory](whatis-hybrid-identity.md)
- [Program Azure AD Connect a federacja](how-to-connect-fed-whatis.md)
