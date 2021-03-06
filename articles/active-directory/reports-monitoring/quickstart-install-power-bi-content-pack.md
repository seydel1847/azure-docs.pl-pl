---
title: Instalowanie pakietu zawartości Azure AD Power BI | Microsoft Docs
description: Dowiedz się, jak zainstalować pakiet zawartości Azure AD Power BI.
services: active-directory
documentationcenter: ''
author: priyamohanram
manager: mtillman
ms.assetid: fd5604eb-1334-4bd8-bfb5-41280883e2b5
ms.service: active-directory
ms.workload: identity
ms.component: report-monitor
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 11/13/2018
ms.author: priyamo
ms.reviewer: dhanyahk
ms.openlocfilehash: 314f1c1656485f93942eb23f928cc66720a12565
ms.sourcegitcommit: 7862449050a220133e5316f0030a259b1c6e3004
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/22/2018
ms.locfileid: "53753544"
---
# <a name="quickstart-install-azure-active-directory-power-bi-content-pack"></a>Szybki start: Instalowanie pakietu zawartości usługi Power BI dla usługi Azure Active Directory

|  |
|--|
|Obecnie pakiet zawartości usługi Power BI dla usługi Azure AD używa interfejsów API programu Graph usługi Azure AD do pobierania danych z dzierżawy usługi Azure AD. W rezultacie mogą występować różnice między danymi dostępnymi w pakiecie zawartości i danymi pobranymi przy użyciu [interfejsów API programu Microsoft Graph do raportowania](concept-reporting-api.md). |
|  |

Pakiet zawartości usługi Power BI dla usługi Azure Active Directory (Azure AD) umożliwia tworzenie wizualizacji danych raportowania z Twojego środowiska. Możesz pobrać wstępnie skompilowany pakiet zawartości i używać go do raportowania wszystkich działań w katalogu przy użyciu rozbudowanego środowiska wizualizacji oferowanego przez usługę Power BI. Możesz również utworzyć własny pulpit nawigacyjny i w prosty sposób udostępnić go innym osobom w organizacji. 

Z tego przewodnika Szybki start dowiesz się, jak zainstalować pakiet zawartości.

## <a name="prerequisites"></a>Wymagania wstępne

Aby ukończyć ten przewodnik Szybki Start, musisz spełnić następujące warunki:

* Konto usługi Power BI. To jest to samo konto, co konto usługi O365 lub Azure AD. 
* Identyfikator dzierżawy usługi Azure AD. To jest **Identyfikator katalogu** ze [strony właściwości](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Properties) w witrynie Azure Portal.
* Licencja usługi Azure AD Premium (P1/P2). Aby uaktualnić swoją wersję usługi Azure Active Directory, zobacz [Wprowadzenie do usługi Azure Active Directory w wersji Premium](../fundamentals/active-directory-get-started-premium.md).

## <a name="install-azure-ad-power-bi-content-pack"></a>Instalowanie pakietu zawartości Azure AD Power BI 

1. Zaloguj się do usługi [Power BI](https://app.powerbi.com/groups/me/getdata/services) przy użyciu swojego konta usługi Power BI. Jest to to samo konto co usługi O365 lub Azure AD.

2. Wyszukaj **Dzienniki aktywności usługi Azure Active Directory** na stronie **Aplikacje** i wybierz pozycję **Pobierz teraz**. 

   ![Pakiet zawartości usługi Power BI dla usługi Azure Active Directory](./media/quickstart-install-power-bi-content-pack/getitnow.png) 
    
3. W oknie podręcznym wpisz swój identyfikator dzierżawy usługi Azure AD, wpisz **7** jako liczbę dni zapytania, a następnie wybierz przycisk **Dalej**.
    
   ![Pakiet zawartości usługi Power BI dla usługi Azure Active Directory](./media/quickstart-install-power-bi-content-pack/connect.png) 

4. Po utworzeniu pulpitu nawigacyjnego dzienników aktywności usługi Azure Active Directory wybierz go.

   ![Pakiet zawartości usługi Power BI dla usługi Azure Active Directory](./media/quickstart-install-power-bi-content-pack/dashboard.png) 
    
## <a name="next-steps"></a>Następne kroki

* [Korzystanie z pakietu zawartości usługi Power BI](howto-power-bi-content-pack.md).
* [Rozwiązywanie problemów z błędami pakietu zawartości](troubleshoot-content-pack.md).
