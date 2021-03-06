---
title: Jak zablokować starsze uwierzytelnianie w usłudze Azure Active Directory (Azure AD) przy użyciu dostępu warunkowego | Dokumentacja firmy Microsoft
description: Dowiedz się, jak skonfigurować zasady dostępu warunkowego w usłudze Azure Active Directory (Azure AD) podczas podejmowania prób dostępu z niezaufanymi sieciami.
services: active-directory
keywords: dostęp warunkowy do aplikacji, dostęp warunkowy w usłudze Azure AD, zabezpieczenia dostępu do zasobów firmy, zasady dostępu warunkowego
documentationcenter: ''
author: MarkusVi
manager: mtillman
editor: ''
ms.component: conditional-access
ms.assetid: 8c1d978f-e80b-420e-853a-8bbddc4bcdad
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 12/06/2018
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 2abf0afb3b6e1cd80168fa3f295297551b9bf7ce
ms.sourcegitcommit: 7862449050a220133e5316f0030a259b1c6e3004
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/22/2018
ms.locfileid: "53755159"
---
# <a name="how-to-block-legacy-authentication-to-azure-ad-with-conditional-access"></a>Instrukcje: Blokuj starsze uwierzytelnianie do usługi Azure AD przy użyciu dostępu warunkowego   

Aby dać użytkownikom łatwy dostęp do aplikacji w chmurze, Azure Active Directory (Azure AD) obsługuje szerokiej gamy protokołów uwierzytelniania, w tym starsze uwierzytelnianie. Uwierzytelnianie wieloskładnikowe (MFA) nie obsługuje jednak starszych protokołów. Uwierzytelnianie wieloskładnikowe w wielu środowiskach jest typowym wymogiem na kradzież tożsamości adresu. 

Jeśli Twoje środowisko jest gotowe do bloku starszych uwierzytelniania w celu zwiększenia ochrony Twojej dzierżawy, można osiągnąć ten cel przy użyciu dostępu warunkowego. W tym artykule opisano sposób konfigurowania zasad dostępu warunkowego bloku starszych uwierzytelniania dla dzierżawy.



## <a name="prerequisites"></a>Wymagania wstępne

W tym artykule założono, że znasz: 

- [Podstawowe pojęcia](overview.md) dostępu warunkowego usługi Azure AD 
- [Najlepsze praktyki](best-practices.md) na temat konfigurowania zasad dostępu warunkowego w witrynie Azure portal



## <a name="scenario-description"></a>Opis scenariusza

Usługa Azure AD obsługuje niektóre z najczęściej używanych protokołów uwierzytelniania i autoryzacji, w tym starsze uwierzytelnianie. Starsze uwierzytelnianie odnosi się do protokołów, które korzystają z uwierzytelniania podstawowego. Zazwyczaj te protokoły nie można wymusić dowolnego typu uwierzytelniania dwuskładnikowego. Przykłady aplikacji, które są oparte na starszych uwierzytelniania są:

- Starsze aplikacje pakietu Microsoft Office

- Aplikacje przy użyciu protokołów poczty, takich jak SMTP, POP i IMAP

Uwierzytelnianie pojedynczy czynnik (na przykład nazwę użytkownika i hasło) nie jest wystarczająco dużo, te dni. Hasła są uszkodzone, są one łatwe do odgadnięcia i firma Microsoft (ludzi) będą nieprawidłowe na wybranie dobre hasła. Hasła są również narażone na różnych atakami, takimi jak osłony techniki wyłudzania informacji oraz hasło. Jeden najprostszym rzeczy, które można zrobić, aby chronić przed zagrożeniami hasła jest zaimplementowanie usługi MFA. Za pomocą usługi MFA nawet wtedy, gdy osoba atakująca uzyskuje w posiadaniu hasła użytkownika samego hasła nie jest wystarczające, aby pomyślnie uwierzytelnić i uzyskać dostęp do danych.

Jak można zapobiec aplikacji korzystających z uwierzytelniania starszej wersji, uzyskiwanie dostępu do zasobów dzierżawy Zalecane jest po prostu je zablokować przy użyciu zasad dostępu warunkowego. Jeśli to konieczne, możesz zezwolić tylko niektórych użytkowników i określone lokalizacje sieciowe korzystać z aplikacji, które są oparte na starszych uwierzytelniania.




## <a name="implementation"></a>Wdrażanie

W tej sekcji opisano sposób konfigurowania zasad dostępu warunkowego w celu uwierzytelniania starszych bloku. 

### <a name="block-legacy-authentication"></a>Blokowanie starszego uwierzytelniania 

W zasadach dostępu warunkowego można ustawić warunek, który jest powiązany z aplikacji klienckich, które są używane do dostępu do zasobów. Stan aplikacji klienta umożliwia zawężenie zakresu do aplikacji przy użyciu starszej wersji uwierzytelniania, wybierając **inni klienci** dla **aplikacje mobilne i klienci stacjonarni**.

![Inni klienci](./media/block-legacy-authentication/01.png)

Aby zablokować dostęp do tych aplikacji, musisz wybrać **blokowana**.

![Blokuj dostęp](./media/block-legacy-authentication/02.png)


### <a name="select-users-and-cloud-apps"></a>Wybierz użytkowników i aplikacje w chmurze

Jeśli chcesz zablokować starsze uwierzytelnianie dla Twojej organizacji, prawdopodobnie uważasz, że można to zrobić, wybierając:

- Wszyscy użytkownicy

- Wszystkie aplikacje w chmurze

- Blokuj dostęp
 

![Przypisania](./media/block-legacy-authentication/03.png)



Platforma Azure ma funkcję bezpieczeństwa, która uniemożliwia tworzenie takie zasady, ponieważ narusza tę konfigurację [najlepsze praktyki](best-practices.md) dla zasad dostępu warunkowego.
 
![Konfiguracja zasad nie jest obsługiwana](./media/block-legacy-authentication/04.png)


Funkcja bezpieczeństwa jest konieczne ponieważ *zablokowanie wszystkich użytkowników i wszystkie aplikacje w chmurze* może potencjalnie zablokować w całej organizacji, zalogowanie się do swojej dzierżawy. Musisz wykluczyć co najmniej jednego użytkownika do zaspokojenia minimalnym wymaganiem najlepszym rozwiązaniem. Można również wykluczyć rolę katalogu.

![Konfiguracja zasad nie jest obsługiwana](./media/block-legacy-authentication/05.png)


Ta funkcja może spełnić przez wykluczenie jednego użytkownika z zasad. W idealnym przypadku należy zdefiniować kilka [dostępu awaryjnego kont administracyjnych w usłudze Azure AD](../users-groups-roles/directory-emergency-access.md) i ich wykluczenie z zasad.
 

## <a name="policy-deployment"></a>Wdrażanie zasad

Zanim przeniesiesz zasad w środowisku produkcyjnym zajmie się:
 
- **Konta usług** -zidentyfikować konta użytkowników, które są używane jako konta usług lub urządzeń, takich jak telefony pokoju konferencji. Upewnij się, te konta silnych haseł i dodać je do grupy wykluczonych.
 
- **Raportów logowania** — przejrzeć raport, zaloguj się i poszukaj **innych klientów** ruchu. Identyfikowanie najważniejszych użycia i zbadać, dlaczego jest on używany. Zwykle ruch jest generowana przez starszych klientów pakietu Office, które nie korzystają z nowoczesnego uwierzytelniania lub niektóre aplikacje poczty innych firm. Stworzyć plan przenieść użycia od tych aplikacji lub jeśli brakuje wpływ powiadomić użytkowników, że te aplikacje nie mogą używać już.
 
Aby uzyskać więcej informacji, zobacz [jak należy wdrożyć nowe zasady?](best-practices.md#how-should-you-deploy-a-new-policy).



## <a name="what-you-should-know"></a>Co należy wiedzieć

Konfigurowanie zasad dla **inni klienci** blokuje całą organizację, z niektórych klientów, takich jak SPConnect. Ten blok wynika z faktu, starsi klienci uwierzytelnić się w nieoczekiwany sposób. Ten problem nie ma zastosowania do głównej aplikacji pakietu Office, takich jak starsi klienci pakietu Office.

Może upłynąć do 24 godzin, aż zasady zaczną obowiązywać.

Można wybrać wszystkie formanty grant dostępne dla innych klientów warunku; jednak środowisko użytkownika końcowego jest zawsze taki sam - dostęp jest zablokowany.

Można skonfigurować inne warunki obok innych warunków klientów.




## <a name="next-steps"></a>Kolejne kroki

Jeśli nie znasz jeszcze konfigurowania zasad dostępu warunkowego, zobacz [wymagać uwierzytelniania Wieloskładnikowego dla określonych aplikacji przy użyciu dostępu warunkowego usługi Azure Active Directory](app-based-mfa.md) przykład.
