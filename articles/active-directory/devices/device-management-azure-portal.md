---
title: Jak zarządzać urządzeniami przy użyciu witryny Azure portal | Dokumentacja firmy Microsoft
description: Dowiedz się, jak zarządzać urządzeniami przy użyciu witryny Azure portal.
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: mtillman
editor: ''
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.component: devices
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/26/2018
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 4344f0c69554db8c17e62f586d2598f6555aad14
ms.sourcegitcommit: d4f728095cf52b109b3117be9059809c12b69e32
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/10/2019
ms.locfileid: "54196727"
---
# <a name="how-to-manage-devices-using-the-azure-portal"></a>Jak zarządzać urządzeniami przy użyciu witryny Azure portal


Zarządzanie urządzeniami w usłudze Azure Active Directory (Azure AD) pozwala zapewnić, że użytkownicy uzyskują dostęp do zasobów z urządzeń, które spełniają Twoje standardy dotyczące zabezpieczeń i zgodności. 

W tym artykule:

- Przyjęto założenie, że czytelnik zna [wprowadzenie do zarządzania urządzeniami w usłudze Azure Active Directory](overview.md)

- Zawiera informacje na temat zarządzania urządzeniami przy użyciu witryny Azure portal

## <a name="manage-devices"></a>Zarządzanie urządzeniami 

Witryna Azure portal udostępnia centralne miejsce do zarządzania urządzeniami. Można uzyskać w tym miejscu, za pomocą [bezpośredni link](https://portal.azure.com/#blade/Microsoft_AAD_IAM/DevicesMenuBlade/Devices) lub ręcznie wykonaj następujące czynności:

1. Zaloguj się do [witryny Azure portal](https://portal.azure.com) jako administrator.

2. Na lewym pasku nawigacyjnym kliknij **usługi Active Directory**.

    ![Konfiguruj ustawienia urządzenia](./media/device-management-azure-portal/01.png)

3. W **Zarządzaj** kliknij **urządzeń**.

    ![Konfiguruj ustawienia urządzenia](./media/device-management-azure-portal/74.png)
 
**Urządzeń** strony umożliwia:

- Konfiguruj ustawienia zarządzania urządzeniami

- Lokalizowanie urządzeń

- Wykonywanie zadań zarządzania urządzeniami

- Przegląd zarządzania urządzeniami, związane z dziennikami inspekcji  
  

## <a name="configure-device-settings"></a>Konfiguruj ustawienia urządzenia

Do zarządzania urządzeniami przy użyciu portalu Azure, urządzenie musi być on [zarejestrowany lub dołączonych do](overview.md#getting-devices-under-the-control-of-azure-ad) do usługi Azure AD. Jako administrator można dostosować proces rejestracji i dołączenie urządzeń, konfigurując ustawienia urządzenia. 

![Konfiguruj ustawienia urządzenia](./media/device-management-azure-portal/22.png)

Na stronie ustawień urządzenia można skonfigurować:

![Zarządzanie urządzeniami usługi Intune](./media/device-management-azure-portal/21.png)


- **Użytkownicy mogą dołączać urządzania do usługi Azure AD** — to ustawienie umożliwia wybranie użytkowników, którzy mogą [dołączać urządzenia](overview.md#azure-ad-joined-devices) do usługi Azure AD. Wartość domyślna to **wszystkich**. To ustawienie ma zastosowanie tylko do usługi Azure AD Join w systemie Windows 10.

- **Urządzenia przyłączone do dodatkowych administratorów lokalnych w usłudze Azure AD** — możesz wybrać użytkowników, którzy mają prawa administratora lokalnego na urządzeniu. Użytkowników dodanych w tym miejscu są dodawane do *Administratorzy urządzenia* roli w usłudze Azure AD. Administratorzy globalni w usłudze Azure AD i właścicielom urządzeń są domyślnie udzielone prawa administratora lokalnego. Ta opcja jest dostępna za pośrednictwem produktów, takich jak Azure AD Premium lub Enterprise Mobility Suite (EMS) możliwości w wersji premium. 

- **Użytkownicy mogą rejestrować swoje urządzenia w usłudze Azure AD** — należy skonfigurować to ustawienie, aby zezwolić urządzeniom na być [zarejestrowany](overview.md#azure-ad-registered-devices) z usługą Azure AD. Jeśli wybierzesz **Brak**, urządzenia nie są dozwolone do rejestru, jeśli nie są one przyłączony Azure AD lub hybrydowe przyłączone do usługi Azure AD. Rejestracja w usłudze Microsoft Intune lub zarządzania urządzeniami przenośnymi (MDM) dla usługi Office 365 wymaga rejestracji. Jeśli skonfigurowano którąś z tych usług **wszystkich** jest zaznaczone i **NONE** nie jest dostępna.

- **Wymagaj uwierzytelniania wieloskładnikowego do dołączania urządzeń** — możesz wybrać, czy użytkownicy muszą zapewnić drugi składnik uwierzytelniania w celu [sprzężenia](overview.md#azure-ad-joined-devices) swojego urządzenia do usługi Azure AD. Wartość domyślna to **nie**. Zaleca się wymaganie uwierzytelniania wieloskładnikowego podczas rejestrowania urządzenia. Przed włączeniem uwierzytelniania wieloskładnikowego dla tej usługi, musisz zapewnić, że skonfigurowano uwierzytelniania wieloskładnikowego dla użytkowników, które rejestrują swoje urządzenia. Aby uzyskać więcej informacji na temat usług innej usługi Azure Multi-Factor authentication, zobacz [wprowadzenie do usługi Azure Multi-Factor authentication](../authentication/concept-mfa-whichversion.md). To ustawienie nie ma wpływu na dołączenie do hybrydowej dla systemu Windows 10 lub Windows 7. To ma zastosowanie tylko do usługi Azure AD Join w systemie Windows 10 i ang. rejestrację urządzeń dla systemu Windows 10, iOS i Android. 

- **Maksymalna liczba urządzeń** — to ustawienie umożliwia wybranie maksymalną liczbę urządzeń, które użytkownik może mieć w usłudze Azure AD. Jeśli użytkownik osiągnie ten limit przydziału, są one być nie mógł dodać dodatkowych urządzeń dopóki jedna lub więcej istniejących urządzeń są usuwane. Oferta urządzenie jest liczone dla wszystkich urządzeń, które są dołączone do usługi Azure AD lub usługi Azure AD obecnie zarejestrowane. Wartość domyślna to **20**.

- **Użytkownicy mogą synchronizować ustawień i danych aplikacji na urządzeniach** — domyślnie to ustawienie ma wartość **NONE**. Wybranie określonych użytkowników lub grup lub wszystkie umożliwia użytkownika ustawień i danych aplikacji na synchronizacje przez urządzeń z systemem Windows 10. Dowiedz się więcej na temat działania synchronizacji w systemie Windows 10.
Ta opcja jest możliwość premium, dostępna za pośrednictwem produktów, takich jak Azure AD Premium lub Enterprise Mobility Suite (EMS).
 




## <a name="locate-devices"></a>Lokalizowanie urządzeń

Masz dwie opcje można znaleźć urządzenia zarejestrowane i przyłączone do:

- **Wszystkie urządzenia** w **Zarządzaj** części **urządzeń** strony  

    ![Wszystkie urządzenia](./media/device-management-azure-portal/41.png)


- **Urządzenia** w **Zarządzaj** części **użytkownika** strony
 
    ![Wszystkie urządzenia](./media/device-management-azure-portal/43.png)



Za pomocą obu opcji można uzyskać do widoku, który:


- Umożliwia wyszukiwanie urządzeń przy użyciu nazwy wyświetlanej jako filtr.

- Zawiera szczegółowe omówienie urządzenia zarejestrowane i przyłączone do

- Umożliwia wykonywanie typowych zadań zarządzania urządzeniami
   

![Wszystkie urządzenia](./media/device-management-azure-portal/51.png)

Niektóre urządzenia z systemem iOS nazwy urządzenia, zawierające apostrofy mogą za pomocą różnych znaków, które wyglądają w apostrofy. Dlatego wyszukiwania dla takich urządzeń jest trudna — Jeśli nie widzisz wyniki wyszukiwania poprawnie, należy upewnić się, czy ciąg wyszukiwania zawiera znak apostrofu dopasowania.

## <a name="device-management-tasks"></a>Zadania dotyczące zarządzania urządzeniami

Jako administrator globalny można zarządzać zarejestrowane lub dołączonym do urządzenia. Administratorzy usługi Intune mogą:
 
- Aktualizacja urządzenia — przykłady są codziennych operacji, takich jak włączanie/wyłączanie urządzeń

- Usuwanie urządzeń — w przypadku, gdy urządzenie jest wycofywane i należy go usunąć w usłudze Azure AD

Ta sekcja zawiera informacje na temat typowych zadań zarządzania dla urządzenia.



### <a name="manage-an-intune-device"></a>Zarządzanie urządzeniami usługi Intune

Jeśli jesteś administratorem usługi Intune, możesz zarządzać urządzeniami, oznaczone jako **Microsoft Intune**. 

![Zarządzanie urządzeniami usługi Intune](./media/device-management-azure-portal/31.png)


### <a name="enable--disable-an-azure-ad-device"></a>Włącz / Wyłącz urządzenie usługi Azure AD

Aby włączyć / wyłączyć urządzenie, masz dwie opcje:

- Menu zadania ("...") **urządzeniom** strony

    ![Zarządzanie urządzeniami usługi Intune](./media/device-management-azure-portal/71.png)

- Pasek narzędzi na **urządzeń** strony

    ![Zarządzanie urządzeniami usługi Intune](./media/device-management-azure-portal/32.png)


**Uwagi:**

- Musisz być administratorem globalnym w usłudze Azure AD, aby włączyć / wyłączyć urządzenie. 
- Wyłączenie urządzenia powoduje urządzenia z pomyślnym uwierzytelnieniu w usłudze Azure AD, uwalniając urządzenia dostęp do zasobów usługi Azure AD, na które będą chronione przez urządzenie urzędu certyfikacji lub przy użyciu poświadczeń WH4B. 



### <a name="delete-an-azure-ad-device"></a>Usuwanie urządzenia z usługi Azure AD

Aby usunąć urządzenie, masz dwie opcje:

- Menu zadania ("...") **urządzeniom** strony

    ![Zarządzanie urządzeniami usługi Intune](./media/device-management-azure-portal/72.png)

- Pasek narzędzi na **urządzeń** strony

    ![Usuwanie urządzenia](./media/device-management-azure-portal/34.png)


**Uwagi:**

- Musisz być administratorem globalnym lub administratorem usługi Intune w usłudze Azure AD, aby usunąć urządzenie.

- Usuwanie urządzenia:
 
    - Urządzenie uniemożliwia dostęp do zasobów usługi Azure AD. 

    - Usuwa wszystkie szczegółowe informacje, które są dołączone do urządzenia, na przykład, klucze funkcji BitLocker dla urządzeń Windows.  

    - Reprezentuje nieodwracalny działania i nie jest zalecane, chyba że jest to wymagane.

Jeśli urządzenie jest zarządzane przez inny urząd zarządzania (na przykład, Microsoft Intune), upewnij się, że urządzenie zostało wyczyszczone / wycofana przed usunięciem urządzenia w usłudze Azure AD.

 


### <a name="view-or-copy-device-id"></a>Wyświetlanie lub skopiuj identyfikator urządzenia

Identyfikator urządzenia można użyć, aby sprawdzić szczegóły Identyfikatora urządzenia na urządzeniu lub przy użyciu programu PowerShell podczas rozwiązywania problemów. Aby uzyskać dostęp do opcji kopię, kliknij urządzenie.

![Wyświetl identyfikator urządzenia](./media/device-management-azure-portal/35.png)
  

### <a name="view-or-copy-bitlocker-keys"></a>Wyświetlanie i kopiowanie kluczy funkcji BitLocker

Można przeglądać i kopiowanie kluczy funkcji BitLocker, aby ułatwić użytkownikom na odzyskiwanie ich zaszyfrowanego dysku. Te klucze są dostępne tylko dla urządzeń Windows, które są szyfrowane i ich kluczy przechowywanych w usłudze Azure AD. Możesz skopiować te klucze podczas uzyskiwania dostępu do szczegółów urządzenia.
 
![Wyświetl klucze funkcji BitLocker](./media/device-management-azure-portal/36.png)

Aby wyświetlić lub skopiować klucze funkcji BitLocker, musisz być właścicielem urządzenia lub użytkownika, który ma co najmniej jedną z następujących ról, które są przypisane:

- Administratorzy globalni
- Również administratorów pomocy technicznej
- Administratorzy zabezpieczeń
- Czytelnicy zabezpieczeń
- Administratorzy usługi Intune

> [!NOTE]
> Urządzeń z systemem Windows 10 przyłączonych do hybrydowej usługi Azure AD nie ma właściciela. Tak Jeśli szukasz urządzenia przez właściciela, a nie znaleziono jej wyszukiwanie według identyfikatora urządzenia.


## <a name="audit-logs"></a>Dzienniki inspekcji


Działania urządzenia są dostępne za pośrednictwem dzienników aktywności. Dane te obejmują działania wyzwolone przez usługę rejestracji urządzeń i użytkowników:

- Tworzenie urządzenia i dodawanie właścicieli / użytkowników na urządzeniu

- Zmiany w ustawieniach urządzenia

- Operacje dotyczące urządzenia, takie jak usuwanie i aktualizowanie urządzenia
 
Jest punktem wejścia do danych inspekcji **dzienniki inspekcji** w **działania** części **urządzeń** strony.

![Dzienniki inspekcji](./media/device-management-azure-portal/61.png)


Dziennik inspekcji zawiera domyślny widok listy, który pokazuje:

- Data i godzina wystąpienia

- Obiekty docelowe

- Inicjatora / aktora (kto) działania

- Działanie (co)

![Dzienniki inspekcji](./media/device-management-azure-portal/63.png)

Możesz dostosować widok listy, klikając pozycję **Kolumny** na pasku narzędzi.
 
![Dzienniki inspekcji](./media/device-management-azure-portal/64.png)


Aby zawęzić zgłaszane dane do odpowiedniego poziomu, możesz odfiltrować dane inspekcji przy użyciu następujących pól:

- Kategoria
- Typ zasobu działania
- Działanie
- Zakres dat
- Środowisko docelowe
- Zainicjowane przez (aktor)

Oprócz filtrów możesz wyszukać określonych wpisów.

![Dzienniki inspekcji](./media/device-management-azure-portal/65.png)

## <a name="next-steps"></a>Kolejne kroki

* [Wprowadzenie do zarządzania urządzeniami w usłudze Azure Active Directory](overview.md)



