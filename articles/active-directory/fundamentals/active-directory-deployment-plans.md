---
title: Plany wdrażania — usługi Azure Active Directory | Dokumentacja firmy Microsoft
description: End-to-end wskazówki dotyczące wdrażania wiele funkcji usługi Azure Active Directory.
services: active-directory
author: eross-msft
manager: mtillman
ms.service: active-directory
ms.component: fundamentals
ms.workload: identity
ms.topic: conceptual
ms.date: 08/03/2018
ms.author: lizross
ms.custom: it-pro, seodec18
ms.openlocfilehash: f471f1183a7d0d695b5817003fe70a018787731d
ms.sourcegitcommit: 9fb6f44dbdaf9002ac4f411781bf1bd25c191e26
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/08/2018
ms.locfileid: "53094786"
---
# <a name="azure-active-directory-deployment-plans"></a>Plany wdrażania usługi Azure Active Directory
Szukasz kompleksowych wskazówek dotyczących wdrażania niektórych funkcji usługi Azure Active Directory (Azure AD)? W następujących planach wdrażania przedstawiono wartość biznesową, zagadnienia dotyczące planowania, projektowanie i procedury operacyjne potrzebne do pomyślnego wdrożenia niektórych z najpopularniejszych funkcji usługi Azure AD. 

W tych dokumentach znajdziesz szablony wiadomości e-mail, diagramy architektury systemu, typowe przypadki testowe i nie tylko. 

Chętnie poznamy Twoją opinię o tych dokumentach. Weź udział w tej krótkiej [ankiecie](https://aka.ms/deploymentplanfeedback) dotyczącej przydatności tych dokumentów. 

|Scenariusz |Opis |
|-|-|
|[Logowanie jednokrotne](https://aka.ms/SSODPDownload)|Logowanie jednokrotne ułatwia dostęp do wszystkich aplikacji i zasobów potrzebnych do prowadzenia działalności, przy czym można logować się tylko raz, za pomocą jednego konta użytkownika. Po zalogowaniu się można przechodzić z pakietu Microsoft Office do usługi SalesForce lub Box bez konieczności ponownego uwierzytelniania się (na przykład przez wpisanie hasła).|
|[Aprowizacja użytkowników dla ruchu przychodzącego oparte na dzień roboczy](https://aka.ms/WorkdayDeploymentPlan)|Oparte na dzień roboczy dla ruchu przychodzącego aprowizacji użytkowników do usługi Active Directory tworzy ona podstawę do zarządzania tożsamościami bieżące i poprawia jakość procesów biznesowych, które zależą od danych autorytatywne tożsamości. Przy użyciu tej funkcji, można bezproblemowo zarządzać cyklem życia tożsamości pracowników i pracowników warunkowych, konfigurując reguły mapowania akcji aprowizacji IT (np. Utwórz i Włącz, łącznik — modułu przenoszącego spójne kolekcje — wprowadzane procesów (np. Transfer nowego zatrudnienia, zakończenia) Wyłącz, usuwanie kont).|
|[Panel dostępu](https://aka.ms/AccessPanelDPDownload)|Oferuje użytkownikom proste koncentratora do odnajdywania i uzyskują dostęp do wszystkich aplikacji. Umożliwia im mu bardziej wydajnej pracy przy użyciu usługi możliwości samoobsługi, takie jak możliwość żądania dostępu do nowych aplikacji i grup, lub zarządzanie dostępem do tych zasobów w imieniu innych użytkowników.|
|[Aprowizowanie użytkowników](https://aka.ms/UserProvisioningDPDownload)|Usługa Azure AD ułatwia automatyzację tworzenia, obsługi i usuwania tożsamości użytkowników w aplikacjach w chmurze (SaaS), takich jak Dropbox, Salesforce, ServiceNow i nie tylko.|
|[Multi-Factor Authentication](https://aka.ms/MFADPDownload)|Azure Multi-Factor Authentication (MFA) to rozwiązanie firmy Microsoft służące do przeprowadzania weryfikacji dwuetapowej. Przy użyciu zatwierdzonych przez administratora metod uwierzytelniania usługa Azure MFA pomaga w zabezpieczaniu dostępu do danych i aplikacji, jednocześnie spełniając wymagania dotyczące prostoty procesu logowania.|
|[Dostęp warunkowy](https://aka.ms/CADPDownload)|W ramach dostępu warunkowego można implementować automatyczne decyzje kontroli dostępu, które określają na podstawie warunków, kto ma dostęp do aplikacji w chmurze.|
|[Uwierzytelnianie przekazywane za pomocą usługi ADFS](https://aka.ms/ADFSTOPTADPDownload)|Dzięki uwierzytelnianiu przekazywanemu w usłudze Azure AD użytkownicy mogą logować się zarówno do aplikacji lokalnych, jak i w chmurze, używając tego samego hasła. Ta funkcja zapewnia lepszą obsługę użytkowników (jedno hasło mniej do zapamiętania) i obniża koszty pomocy technicznej IT, zmniejszając prawdopodobieństwo tego, że użytkownik zapomni sposób logowania się. Gdy użytkownicy logują się za pomocą usługi Azure AD, ta funkcja weryfikuje ich hasła bezpośrednio w lokalnej usłudze Active Directory.|
|[Synchronizowanie skrótów haseł za pomocą usługi ADFS](https://aka.ms/ADFSTOPHSDPDownload)|Funkcja synchronizacji skrótów zapewnia, że skróty haseł użytkowników są synchronizowane z lokalnej usługi Active Directory do usługi Azure AD, dzięki czemu usługa Azure AD może uwierzytelniać użytkowników bez interakcji z lokalną usługą Active Directory.|
|[Bezproblemowe logowanie jednokrotne](https://aka.ms/SeamlessSSODPDownload)|Bezproblemowe logowanie jednokrotne w usłudze Azure Active Directory zapewnia automatyczne logowanie użytkowników, gdy ich urządzenia są połączone z siecią firmową. Po włączeniu tej funkcji użytkownicy nie muszą wpisywać haseł, aby logować się do usługi Azure AD, i zazwyczaj nie muszą nawet wpisywać swoich nazw użytkownika. Ta funkcja zapewnia użytkownikom łatwy dostęp do aplikacji w chmurze bez konieczności używania dodatkowych składników lokalnych.|
|[Samoobsługowe resetowanie haseł](https://aka.ms/SSPRDPDownload)|Samoobsługowe resetowanie haseł ułatwia użytkownikom resetowanie ich haseł bez udziału administratora w dowolnym miejscu i czasie.|
|[Serwer proxy aplikacji usługi Azure AD](https://aka.ms/AppProxyDPDownload)|Obecnie pracownicy chcą pracować wydajnie w dowolnym miejscu i czasie, na dowolnym urządzeniu. Chcą pracować na własnych urządzeniach — tabletach, telefonach i laptopach. Pracownicy chcą też mieć dostęp do wszystkich swoich aplikacji — zarówno aplikacji SaaS w chmurze, jak i lokalnych aplikacji firmowych. Zapewnienie dostępu do aplikacji lokalnych wymagało dotychczas wirtualnych sieci prywatnych (VPN) lub stref zdemilitaryzowanych (DMZ). Te rozwiązania nie tylko są skomplikowane i trudne do zabezpieczenia, ale też mają wysokie koszty konfigurowania i zarządzania. Jest lepszy sposób — serwer proxy aplikacji usługi Azure AD.|

