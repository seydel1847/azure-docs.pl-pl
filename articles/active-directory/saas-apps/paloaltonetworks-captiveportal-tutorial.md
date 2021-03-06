---
title: 'Samouczek: integracja usługi Azure Active Directory z aplikacją Palo Alto Networks - Captive Portal | Microsoft Docs'
description: Dowiedz się, jak skonfigurować logowanie jednokrotne między usługą Azure Active Directory a aplikacją Palo Alto Networks - Captive Portal.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: barbkess
ms.assetid: 67a0b476-2305-4157-8658-2ec3625850d5
ms.service: Azure-Active-Directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 12/25/2018
ms.author: jeedes
ms.openlocfilehash: eff08cc17f475e2b6ad6406e463de27371bbe5b1
ms.sourcegitcommit: 3ab534773c4decd755c1e433b89a15f7634e088a
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/07/2019
ms.locfileid: "54064733"
---
# <a name="tutorial-azure-active-directory-integration-with-palo-alto-networks---captive-portal"></a>Samouczek: Integracja usługi Azure Active Directory z aplikacją Palo Alto Networks - Captive Portal

Z tego samouczka dowiesz się, jak zintegrować aplikację Palo Alto Networks - Captive Portal z usługą Azure Active Directory (Azure AD).
Zintegrowanie aplikacji Palo Alto Networks - Captive Portal z usługą Azure AD zapewnia następujące korzyści:

* Możliwość kontrolowania dostępu do aplikacji Palo Alto Networks - Captive Portal za pomocą usługi Azure AD.
* Możesz umożliwić swoim użytkownikom automatyczne logowanie do aplikacji Palo Alto Networks - Captive Portal (logowanie jednokrotne) przy użyciu kont usługi Azure AD.
* Możesz zarządzać swoimi kontami w jednej centralnej lokalizacji — witrynie Azure Portal.

Jeśli chcesz dowiedzieć się więcej na temat integracji aplikacji SaaS z usługą Azure AD, zobacz [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis).
Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem [utwórz bezpłatne konto](https://azure.microsoft.com/free/).

## <a name="prerequisites"></a>Wymagania wstępne

Do skonfigurowania integracji usługi Azure AD z aplikacją Palo Alto Networks - Captive Portal potrzebne są następujące elementy:

* Subskrypcja usługi Azure AD. Jeśli nie masz środowiska usługi Azure AD, możesz skorzystać z miesięcznej wersji próbnej [tutaj](https://azure.microsoft.com/pricing/free-trial/)
* Subskrypcja aplikacji Palo Alto Networks - Captive Portal z obsługą logowania jednokrotnego

## <a name="scenario-description"></a>Opis scenariusza

W tym samouczku skonfigurujesz i przetestujesz logowanie jednokrotne usługi Azure AD w środowisku testowym.

* Aplikacja Palo Alto Networks - Captive Portal obsługuje logowanie jednokrotne inicjowane przez **dostawcę tożsamości**

* Aplikacja Palo Alto Networks - Captive Portal obsługuje aprowizację użytkowników **just in time**

## <a name="adding-palo-alto-networks---captive-portal-from-the-gallery"></a>Dodawanie aplikacji Palo Alto Networks - Captive Portal z galerii

Aby skonfigurować integrację aplikacji Palo Alto Networks - Captive Portal z usługą Azure AD, należy z poziomu galerii dodać tę aplikację do listy zarządzanych aplikacji SaaS.

**Aby dodać aplikację Palo Alto Networks - Captive Portal z galerii, wykonaj następujące kroki:**

1. W witrynie **[Azure Portal](https://portal.azure.com)** w panelu nawigacyjnym po lewej stronie kliknij ikonę usługi **Azure Active Directory**.

    ![Przycisk Azure Active Directory](common/select-azuread.png)

2. Przejdź do grupy **Aplikacje dla przedsiębiorstw** i wybierz opcję **Wszystkie aplikacje**.

    ![Blok Aplikacje dla przedsiębiorstw](common/enterprise-applications.png)

3. Aby dodać nową aplikację, kliknij przycisk **Nowa aplikacja** w górnej części okna dialogowego.

    ![Przycisk Nowa aplikacja](common/add-new-app.png)

4. W polu wyszukiwania wpisz **Palo Alto Networks - Captive Portal**, wybierz pozycję **Palo Alto Networks - Captive Portal** z panelu wyników, a następnie kliknij przycisk **Dodaj**, aby dodać aplikację.

     ![Pozycja Palo Alto Networks - Captive Portal na liście wyników](common/search-new-app.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie logowania jednokrotnego usługi Azure AD

W tej sekcji skonfigurujesz i przetestujesz logowanie jednokrotne usługi Azure AD z aplikacją Palo Alto Networks - Captive Portal, korzystając z danych testowego użytkownika **Britta Simon**.
Aby logowanie jednokrotne działało, należy ustanowić relację połączenia między użytkownikiem usługi Azure AD i powiązanym użytkownikiem aplikacji Palo Alto Networks - Captive Portal.

Aby skonfigurować i przetestować logowanie jednokrotne usługi Azure AD z aplikacją Palo Alto Networks - Captive Portal, należy wykonać czynności opisane w poniższych blokach konstrukcyjnych:

1. **[Konfigurowanie logowania jednokrotnego usługi Azure AD](#configure-azure-ad-single-sign-on)** — aby umożliwić użytkownikom korzystanie z tej funkcji.
2. **[Konfigurowanie logowania jednokrotnego w aplikacji Palo Alto Networks - Captive Portal](#configure-palo-alto-networks---captive-portal-single-sign-on)** — aby skonfigurować ustawienia logowania jednokrotnego po stronie aplikacji.
3. **[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)** — aby przetestować logowanie jednokrotne usługi Azure AD z użytkownikiem Britta Simon.
4. **[Przypisywanie użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)** — aby umożliwić użytkownikowi Britta Simon korzystanie z logowania jednokrotnego usługi Azure AD.
5. **[Tworzenie użytkownika testowego aplikacji Palo Alto Networks - Captive Portal](#create-palo-alto-networks---captive-portal-test-user)** — aby w aplikacji Palo Alto Networks - Captive Portal istniał odpowiednik użytkownika Britta Simon połączony z reprezentacją użytkownika w usłudze Azure AD.
6. **[Testowanie logowania jednokrotnego](#test-single-sign-on)** — aby sprawdzić, czy konfiguracja działa.

### <a name="configure-azure-ad-single-sign-on"></a>Konfigurowanie logowania jednokrotnego usługi Azure AD

W tej sekcji włączysz logowanie jednokrotne usługi Azure AD w witrynie Azure Portal.

Aby skonfigurować logowanie jednokrotne usługi Azure AD z aplikacją Palo Alto Networks - Captive Portal, wykonaj następujące kroki:

1. W witrynie [Azure Portal](https://portal.azure.com/) na stronie integracji aplikacji **Palo Alto Networks - Captive Portal** wybierz pozycję **Logowanie jednokrotne**.

    ![Link do konfigurowania logowania jednokrotnego](common/select-sso.png)

2. W oknie dialogowym **Wybieranie metody logowania jednokrotnego** wybierz tryb **SAML/WS-Fed**, aby włączyć logowanie jednokrotne.

    ![Wybieranie trybu logowania jednokrotnego](common/select-saml-option.png)

3. Na stronie **Konfigurowanie logowania jednokrotnego za pomocą protokołu SAML** kliknij ikonę **Edytuj**, aby otworzyć okno dialogowe **Podstawowa konfiguracja protokołu SAML**.

    ![Edycja podstawowej konfiguracji protokołu SAML](common/edit-urls.png)

4. W oknie dialogowym **Podstawowa konfiguracja protokołu SAML** wykonaj następujące kroki:

    ![Informacje o domenie i adresach URL aplikacji Palo Alto Networks - Captive Portal na potrzeby logowania jednokrotnego](common/idp-intiated.png)

    a. W polu **Identyfikator** wpisz adres URL, korzystając z następującego wzorca: `https://<Customer Firewall Hostname>/SAML20/SP`

    b. W polu tekstowym **Adres URL odpowiedzi** wpisz adres URL, korzystając z następującego wzorca: `https://<Customer Firewall Hostname>/SAML20/SP/ACS`

    > [!NOTE]
    > Te wartości nie są prawdziwe. Zastąp te wartości rzeczywistymi wartościami identyfikatora i adresu URL odpowiedzi. Skontaktuj się z [zespołem pomocy technicznej klienta aplikacji Palo Alto Networks - Captive Portal](https://support.paloaltonetworks.com/support), aby uzyskać te wartości. Przydatne mogą się również okazać wzorce przedstawione w sekcji **Podstawowa konfiguracja protokołu SAML** w witrynie Azure Portal.

5. Na stronie **Konfigurowanie logowania jednokrotnego za pomocą protokołu SAML** w sekcji **Certyfikat podpisywania SAML** kliknij link **Pobierz**, aby pobrać **kod XML metadanych federacji** na podstawie podanych opcji zgodnie z wymaganiami i zapisać go na komputerze.

    ![Link do pobierania certyfikatu](common/metadataxml.png)

### <a name="configure-palo-alto-networks---captive-portal-single-sign-on"></a>Konfigurowanie logowania jednokrotnego w aplikacji Palo Alto Networks - Captive Portal

1. W innym oknie przeglądarki otwórz witrynę aplikacji Palo Alto jako administrator.

2. Kliknij pozycję **Device** (Urządzenie).

    ![Konfigurowanie logowania jednokrotnego w rozwiązaniu Palo Alto](./media/paloaltonetworks-captiveportal-tutorial/tutorial_paloaltoadmin_admin1.png)

3. Wybierz pozycję **SAML Identity Provider** (Dostawca tożsamości SAML) w lewym pasku nawigacyjnym, a następnie kliknij przycisk Import (Importuj), aby zaimportować plik metadanych.

    ![Konfigurowanie logowania jednokrotnego w rozwiązaniu Palo Alto](./media/paloaltonetworks-captiveportal-tutorial/tutorial_paloaltoadmin_admin2.png)

4. Wykonaj następujące czynności w oknie importowania

    ![Konfigurowanie logowania jednokrotnego w rozwiązaniu Palo Alto](./media/paloaltonetworks-captiveportal-tutorial/tutorial_paloaltoadmin_admin3.png)

    a. W polu tekstowym **Profile Name** (Nazwa profilu) wprowadź nazwę np. Interfejs użytkownika usługi Azure AD (administrator).
    
    b. W polu **Identity Provider Metadata** (Metadane dostawcy tożsamości) kliknij przycisk **Przeglądaj** i wybierz plik metadata.xml, który został pobrany z witryny Azure Portal.
    
    d. Kliknij przycisk **OK**.

### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD 

W tej sekcji w witrynie Azure Portal utworzysz użytkownika testowego o nazwie Britta Simon.

1. W witrynie Azure Portal w okienku po lewej stronie wybierz pozycję **Azure Active Directory**, wybierz opcję **Użytkownicy**, a następnie wybierz pozycję **Wszyscy użytkownicy**.

    ![Linki „Użytkownicy i grupy” i „Wszyscy użytkownicy”](common/users.png)

2. Wybierz przycisk **Nowy użytkownik** w górnej części ekranu.

    ![Przycisk Nowy użytkownik](common/new-user.png)

3. We właściwościach użytkownika wykonaj następujące kroki.

    ![Okno dialogowe Użytkownik](common/user-properties.png)

    a. W polu **Nazwa** wprowadź **BrittaSimon**.
  
    b. W polu **Nazwa użytkownika** wpisz **brittasimon@yourcompanydomain.extension**  
    Na przykład: BrittaSimon@contoso.com

    d. Zaznacz pole wyboru **Pokaż hasło** i zanotuj wartość wyświetlaną w polu Hasło.

    d. Kliknij pozycję **Utwórz**.

### <a name="assign-the-azure-ad-test-user"></a>Przypisywanie użytkownika testowego usługi Azure AD

W tej sekcji włączysz dla użytkownika Britta Simon możliwość korzystania z logowania jednokrotnego platformy Azure, udzielając dostępu do aplikacji Palo Alto Networks - Captive Portal.

1. W witrynie Azure Portal wybierz pozycję **Aplikacje dla przedsiębiorstw**, wybierz pozycję **Wszystkie aplikacje**, a następnie wybierz pozycję **Palo Alto Networks - Captive Portal**.

    ![Blok Aplikacje dla przedsiębiorstw](common/enterprise-applications.png)

2. Na liście aplikacji wpisz **Palo Alto Networks - Captive Portal** i wybierz odpowiednią pozycję.

    ![Link do aplikacji Palo Alto Networks - GlobalProtect na liście aplikacji](common/all-applications.png)

3. W menu po lewej stronie wybierz pozycję **Użytkownicy i grupy**.

    ![Link „Użytkownicy i grupy”](common/users-groups-blade.png)

4. Kliknij przycisk **Dodaj użytkownika**, a następnie wybierz pozycję **Użytkownicy i grupy** w oknie dialogowym **Dodawanie przypisania**.

    ![Okienko Dodawanie przypisania](common/add-assign-user.png)

5. W oknie dialogowym **Użytkownicy i grupy** wybierz użytkownika **Britta Simon** na liście użytkowników, a następnie kliknij przycisk **Wybierz** u dołu ekranu.

6. Jeśli oczekujesz wartości roli w asercji SAML, w oknie dialogowym **Wybieranie roli** wybierz z listy odpowiednią rolę dla użytkownika, a następnie kliknij przycisk **Wybierz** u dołu ekranu.

7. W oknie dialogowym **Dodawanie przypisania** kliknij przycisk **Przypisz**.

### <a name="create-palo-alto-networks---captive-portal-test-user"></a>Tworzenie użytkownika testowego aplikacji Palo Alto Networks - Captive Portal

W tej sekcji użytkownik o nazwie Britta Simon jest tworzony w aplikacji Captive Portal. Aplikacja Palo Alto Networks - Captive Portal obsługuje aprowizację użytkowników **just in time**, która jest domyślnie włączona. W tej sekcji nie musisz niczego robić. Jeśli użytkownik jeszcze nie istnieje w aplikacji Palo Alto Networks - Captive Portal, zostanie utworzony po uwierzytelnieniu.

> [!NOTE]
> Jeśli potrzebujesz ręcznie utworzyć użytkownika, skontaktuj się z [zespołem pomocy technicznej klienta aplikacji Palo Alto Networks - Captive Portal](https://support.paloaltonetworks.com/support).

### <a name="test-single-sign-on"></a>Testowanie logowania jednokrotnego 

Aplikacja Captive Portal jest konfigurowana za zaporą na maszynie wirtualnej z systemem Windows. Aby przetestować logowanie jednokrotne w aplikacji Captive Portal, zaloguj się do maszyny wirtualnej z systemem Windows przy użyciu protokołu RDP. W ramach sesji protokołu RDP otwórz w przeglądarce dowolną witrynę internetową, co powinno spowodować automatycznie otwarcie adresu URL logowania jednokrotnego i wyświetlenie monitu o uwierzytelnienie. Po zakończeniu uwierzytelniania użytkownik powinien mieć możliwość korzystania z witryn internetowych.

## <a name="additional-resources"></a>Dodatkowe zasoby

- [ Lista samouczków dotyczących sposobu integrowania aplikacji SaaS z usługą Azure Active Directory ](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list)

- [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)

- [Co to jest dostęp warunkowy w usłudze Azure Active Directory?](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)

