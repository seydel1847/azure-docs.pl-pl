---
title: Co to jest funkcja monitorowania usługi Azure Active Directory? (wersja zapoznawcza) | Microsoft Docs
description: Zawiera ogólne omówienie funkcji monitorowania usługi Azure Active Directory.
services: active-directory
documentationcenter: ''
author: priyamohanram
manager: mtillman
editor: ''
ms.assetid: e2b3d8ce-708a-46e4-b474-123792f35526
ms.service: active-directory
ms.devlang: na
ms.topic: overview
ms.tgt_pltfrm: na
ms.workload: identity
ms.component: report-monitor
ms.date: 11/13/2018
ms.author: priyamo
ms.reviewer: dhanyahk
ms.openlocfilehash: 92e200f358098d5516246d057d1cef406750e326
ms.sourcegitcommit: fa758779501c8a11d98f8cacb15a3cc76e9d38ae
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/20/2018
ms.locfileid: "52264686"
---
# <a name="what-is-azure-active-directory-monitoring-preview"></a>Co to jest funkcja monitorowania usługi Azure Active Directory? (wersja zapoznawcza)

Przy użyciu funkcji monitorowania usługi Azure Active Directory (Azure AD) możesz teraz przekierowywać dzienniki aktywności usługi Azure AD do różnych punktów końcowych. Możesz następnie przechowywać je na potrzeby długoterminowego użytkowania lub zintegrować je z narzędziami do zarządzania informacjami i zdarzeniami zabezpieczeń (SIEM) innych firm, aby uzyskać wgląd w środowisko.

Obecnie dzienniki można przekierowywać do następujących lokalizacji:

- Konto usługi Azure Storage.
- Centrum zdarzeń platformy Azure, aby możliwe było zintegrowanie z wystąpieniami usług Splunk i Sumologic.
- Obszar roboczy usługi Azure Log Analytics, w którym można przeanalizować dane oraz utworzyć pulpit nawigacyjny i alert dla określonych zdarzeń

> [!VIDEO https://www.youtube.com/embed/syT-9KNfug8]

## <a name="diagnostic-settings-configuration"></a>Konfiguracji ustawień diagnostyki

Aby skonfigurować ustawienia monitorowania dla dzienników aktywności usługi Azure AD, najpierw zaloguj się w witrynie [Azure Portal](https://portal.azure.com), a następnie wybierz pozycję **Azure Active Directory**. Z tego miejsca możesz uzyskać dostęp do strony konfiguracji ustawień diagnostycznych na dwa sposoby:

* Wybierz pozycję **Ustawienia diagnostyczne** w sekcji **Monitorowanie**.

    ![Ustawienia diagnostyczne](./media/overview-monitoring/diagnostic-settings.png)
    
* Wybierz pozycję **Dzienniki inspekcji** lub **Logowania**, a następnie wybierz pozycję **Eksportuj ustawienia**. 

    ![Eksportowanie ustawień](./media/overview-monitoring/export-settings.png)


## <a name="route-logs-to-storage-account"></a>Przekierowywanie dzienników do konta magazynu

Przekierowując dzienniki do konta magazynu usługi Azure, możesz przechowywać je dłużej niż w przypadku domyślnego okresu przechowywania określonego w [zasadach przechowywania](reference-reports-data-retention.md). Dowiedz się, jak [kierować dane do konta magazynu](quickstart-azure-monitor-route-logs-to-storage-account.md).

## <a name="stream-logs-to-event-hub"></a>Przesyłanie strumieniowe dzienników do centrum zdarzeń

Przekierowywanie dzienników do centrum zdarzeń platformy Azure umożliwia integrację z narzędziami SIEM takimi jak Sumologic i Splunk. Ta integracja pozwala połączyć dane dzienników aktywności usługi Azure AD z innymi danymi zarządzanymi przez rozwiązania SIEM, co zapewnia lepszy wgląd w środowisko. Dowiedz się, jak [wysyłać strumieniowo dzienniki do centrum zdarzeń](tutorial-azure-monitor-stream-logs-to-event-hub.md).

## <a name="send-logs-to-log-analytics"></a>Wysyłanie dzienników do usługi Log Analytics

[Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview) to rozwiązanie, które konsoliduje dane monitorowania z różnych źródeł i udostępnia język zapytań oraz aparat analityczny, który zapewnia wgląd w działanie aplikacji i zasobów. Wysyłając dzienniki aktywności usługi Azure AD do usługi Log Analytics, możesz szybko pobierać i monitorować zebrane dane oraz wysyłać dotyczące ich alerty. Dowiedz się, jak [wysyłać dane do usługi Log Analytics](howto-integrate-activity-logs-with-log-analytics.md).

Możesz także zainstalować wstępnie utworzone widoki dla dzienników aktywności usługi Azure AD, aby monitorować typowe scenariusze obejmujące logowania i zdarzenia inspekcji. Dowiedz się, jak [zainstalować widoki usługi Log Analytics dla dzienników aktywności usługi Azure AD i używać ich](howto-install-use-log-analytics-views.md).

## <a name="next-steps"></a>Następne kroki

* [Dzienniki aktywności w usłudze Azure Monitor](concept-activity-logs-azure-monitor.md)
* [Przesyłanie strumieniowe dzienników do centrum zdarzeń](tutorial-azure-monitor-stream-logs-to-event-hub.md)
* [Wysyłanie dzienników do usługi Log Analytics](howto-integrate-activity-logs-with-log-analytics.md)
