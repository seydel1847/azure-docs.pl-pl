---
title: 'Samouczek: integracja usługi Azure Active Directory z aplikacją Confluence SAML SSO by Microsoft | Microsoft Docs'
description: Dowiedz się, jak skonfigurować logowanie jednokrotne między usługą Azure Active Directory a aplikacją Confluence SAML SSO by Microsoft.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: barbkess
ms.assetid: 1ad1cf90-52bc-4b71-ab2b-9a5a1280fb2d
ms.service: Azure-Active-Directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 12/31/2018
ms.author: jeedes
ms.openlocfilehash: f238a97b7b6e8e9bcbbdc1be60789982face1ac7
ms.sourcegitcommit: 3ab534773c4decd755c1e433b89a15f7634e088a
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/07/2019
ms.locfileid: "54063900"
---
# <a name="tutorial-azure-active-directory-integration-with-confluence-saml-sso-by-microsoft"></a>Samouczek: integracja usługi Azure Active Directory z aplikacją Confluence SAML SSO by Microsoft

W tym samouczku dowiesz się, jak zintegrować aplikację Confluence SAML SSO by Microsoft za pomocą usługi Azure Active Directory (Azure AD).
Integracja aplikacji Confluence SAML SSO by Microsoft z usługą Azure AD zapewnia następujące korzyści:

* W usłudze Azure AD możesz kontrolować, kto ma dostęp do aplikacji Confluence SAML SSO by Microsoft.
* Możesz zezwolić swoim użytkownikom na automatyczne logowanie do aplikacji Confluence SAML SSO by Microsoft (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.
* Możesz zarządzać swoimi kontami w jednej centralnej lokalizacji — witrynie Azure Portal.

Jeśli chcesz dowiedzieć się więcej na temat integracji aplikacji SaaS z usługą Azure AD, zobacz [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis).
Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem [utwórz bezpłatne konto](https://azure.microsoft.com/free/).

## <a name="description"></a>Opis:

Użyj konta usługi Microsoft Azure Active Directory w połączeniu z serwerem Atlassian Confluence, aby umożliwić logowanie jednokrotne. W ten sposób wszyscy użytkownicy w Twojej organizacji będą mogli używać poświadczeń usługi Azure AD do logowania się do aplikacji Confluence. Ta wtyczka używa protokołu SAML 2.0 na potrzeby federacji.

## <a name="prerequisites"></a>Wymagania wstępne

Do skonfigurowania integracji usługi Azure AD z aplikacją Confluence SAML SSO by Microsoft są potrzebne następujące elementy:

- Subskrypcji usługi Azure AD
- Aplikacja serwera Confluence zainstalowana na serwerze z 64-bitowym systemem Windows (lokalnie lub w infrastrukturze IaaS chmury)
- Serwer Confluence obsługuje protokół HTTPS
- Zwróć uwagę na obsługiwane wersje wtyczki Confluence podane w poniższej sekcji.
- Serwer Confluence jest dostępny w Internecie, w szczególności dla strony logowania usługi Azure AD na potrzeby uwierzytelniania, i powinien mieć możliwość odbierania tokenu z usługi Azure AD
- Poświadczenia administratora są skonfigurowane w aplikacji Confluence
- WebSudo jest wyłączone w aplikacji Confluence
- Użytkownik testowy utworzony w aplikacji serwera Confluence

> [!NOTE]
> Nie zalecamy używania środowiska produkcyjnego aplikacji Confluence do testowania czynności opisanych w tym samouczku. Integrację należy najpierw przetestować w środowisku programistycznym lub przejściowym aplikacji, a dopiero później użyć środowiska produkcyjnego.

Aby przetestować czynności opisane w tym samouczku, należy postępować zgodnie z następującymi zaleceniami:

- Nie używaj środowiska produkcyjnego, chyba że jest to konieczne.
- Jeśli nie masz środowiska próbnego usługi Azure AD, możesz skorzystać z miesięcznej wersji próbnej tutaj: [Wersja próbna](https://azure.microsoft.com/pricing/free-trial/).

## <a name="supported-versions-of-confluence"></a>Obsługiwane wersje aplikacji Confluence

Aktualnie obsługiwane są następujące wersje aplikacji Confluence:

- Confluence: 5.0 do 5.10
- Confluence: 6.0.1
- Confluence: 6.1.1
- Confluence: 6.2.1
- Confluence: 6.3.4
- Confluence: 6.4.0
- Confluence: 6.5.0
- Confluence: 6.6.2
- Confluence: 6.7.0
- Confluence: 6.8.1
- Confluence: 6.9.0
- Confluence: 6.10.0
- Confluence: 6.11.0
- Confluence: 6.12.0

## <a name="scenario-description"></a>Opis scenariusza

W tym samouczku skonfigurujesz i przetestujesz logowanie jednokrotne usługi Azure AD w środowisku testowym.

* Program Confluence SAML SSO by Microsoft obsługuje logowanie jednokrotne inicjowane przez **dostawcę usługi**

## <a name="adding-confluence-saml-sso-by-microsoft-from-the-gallery"></a>Dodawanie aplikacji Confluence SAML SSO by Microsoft z galerii

Aby skonfigurować integrację aplikacji Confluence SAML SSO by Microsoft z usługą Azure AD, musisz dodać aplikację Confluence SAML SSO by Microsoft z galerii do swojej listy zarządzanych aplikacji SaaS.

**Aby dodać aplikację Confluence SAML SSO by Microsoft z galerii, wykonaj następujące kroki:**

1. W witrynie **[Azure Portal](https://portal.azure.com)** w panelu nawigacyjnym po lewej stronie kliknij ikonę usługi **Azure Active Directory**.

    ![Przycisk Azure Active Directory](common/select-azuread.png)

2. Przejdź do grupy **Aplikacje dla przedsiębiorstw** i wybierz opcję **Wszystkie aplikacje**.

    ![Blok Aplikacje dla przedsiębiorstw](common/enterprise-applications.png)

3. Aby dodać nową aplikację, kliknij przycisk **Nowa aplikacja** w górnej części okna dialogowego.

    ![Przycisk Nowa aplikacja](common/add-new-app.png)

4. W polu wyszukiwania wpisz **Confluence SAML SSO by Microsoft**, wybierz pozycję **Confluence SAML SSO by Microsoft** z panelu wyników, a następnie kliknij przycisk **Dodaj**, aby dodać aplikację.

     ![Aplikacja Confluence SAML SSO by Microsoft na liście wyników](common/search-new-app.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfigurowanie i testowanie logowania jednokrotnego usługi Azure AD

W tej sekcji skonfigurujesz i przetestujesz logowanie jednokrotne usługi Azure AD z aplikacją Confluence SAML SSO by Microsoft, korzystając z danych testowego użytkownika **Britta Simon**.
Aby logowanie jednokrotne działało, należy ustanowić relację połączenia między użytkownikiem usługi Azure AD i powiązanym użytkownikiem aplikacji Confluence SAML SSO by Microsoft.

Aby skonfigurować i przetestować logowanie jednokrotne usługi Azure AD z aplikacją Confluence SAML SSO by Microsoft, należy utworzyć poniższe bloki konstrukcyjne:

1. **[Konfigurowanie logowania jednokrotnego usługi Azure AD](#configure-azure-ad-single-sign-on)** — aby umożliwić użytkownikom korzystanie z tej funkcji.
2. **[Konfigurowanie logowania jednokrotnego w aplikacji Confluence SAML SSO by Microsoft](#configure-confluence-saml-sso-by-microsoft-single-sign-on)** — aby skonfigurować ustawienia logowania jednokrotnego po stronie aplikacji.
3. **[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)** — aby przetestować logowanie jednokrotne usługi Azure AD z użytkownikiem Britta Simon.
4. **[Przypisywanie użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)** — aby umożliwić użytkownikowi Britta Simon korzystanie z logowania jednokrotnego usługi Azure AD.
5. **[Tworzenie użytkownika testowego aplikacji Confluence SAML SSO by Microsoft](#create-confluence-saml-sso-by-microsoft-test-user)** — aby mieć w aplikacji Confluence SAML SSO by Microsoft odpowiednik użytkownika Britta Simon, który jest połączony z reprezentacją użytkownika w usłudze Azure AD.
6. **[Testowanie logowania jednokrotnego](#test-single-sign-on)** — aby sprawdzić, czy konfiguracja działa.

### <a name="configure-azure-ad-single-sign-on"></a>Konfigurowanie logowania jednokrotnego usługi Azure AD

W tej sekcji włączysz logowanie jednokrotne usługi Azure AD w witrynie Azure Portal.

Aby skonfigurować logowanie jednokrotne usługi Azure AD w aplikacji Confluence SAML SSO by Microsoft, wykonaj następujące kroki:

1. W witrynie [Azure Portal](https://portal.azure.com/) na stronie integracji aplikacji **Confluence SAML SSO by Microsoft** wybierz pozycję **Logowanie jednokrotne**.

    ![Link do konfigurowania logowania jednokrotnego](common/select-sso.png)

2. W oknie dialogowym **Wybieranie metody logowania jednokrotnego** wybierz tryb **SAML/WS-Fed**, aby włączyć logowanie jednokrotne.

    ![Wybieranie trybu logowania jednokrotnego](common/select-saml-option.png)

3. Na stronie **Konfigurowanie logowania jednokrotnego za pomocą protokołu SAML** kliknij ikonę **Edytuj**, aby otworzyć okno dialogowe **Podstawowa konfiguracja protokołu SAML**.

    ![Edycja podstawowej konfiguracji protokołu SAML](common/edit-urls.png)

4. W sekcji **Podstawowa konfiguracja protokołu SAML** wykonaj następujące czynności:

    ![Informacje na temat domeny i adresów URL logowania jednokrotnego aplikacji Confluence SAML SSO by Microsoft](common/sp-identifier-reply.png)

    a. W polu tekstowym **Adres URL logowania** wpisz adres URL, korzystając z następującego wzorca: `https://<domain:port>/plugins/servlet/saml/auth`

    b. W polu **Identyfikator** wpisz adres URL, korzystając z następującego wzorca: `https://<domain:port>/`

    d. W polu tekstowym **Adres URL odpowiedzi** wpisz adres URL, korzystając z następującego wzorca: `https://<domain:port>/plugins/servlet/saml/auth`

    > [!NOTE]
    > Te wartości nie są prawdziwe. Zastąp je rzeczywistymi wartościami identyfikatora, adresu URL odpowiedzi i adresu URL logowania. Port jest opcjonalny, jeśli adres URL zawiera nazwę. Te wartości można uzyskać podczas konfigurowania wtyczki Confluence, co jest objaśnione w dalszej części tego samouczka.

4. Na stronie **Konfigurowanie logowania jednokrotnego za pomocą protokołu SAML** w sekcji **Certyfikat podpisywania SAML** kliknij przycisk kopiowania, aby skopiować **adres URL metadanych federacji aplikacji** i zapisać go na komputerze.

    ![Link do pobierania certyfikatu](common/copy-metadataurl.png)

### <a name="configure-confluence-saml-sso-by-microsoft-single-sign-on"></a>Konfigurowanie logowania jednokrotnego aplikacji Confluence SAML SSO by Microsoft

1. W innym oknie przeglądarki internetowej zaloguj się do swojego wystąpienia aplikacji Confluence jako administrator.

2. Zatrzymaj wskaźnik myszy nad ikoną koła zębatego i kliknij pozycję **Dodatki**.

    ![Konfigurowanie logowania jednokrotnego](./media/confluencemicrosoft-tutorial/addon1.png)

3. Pobierz wtyczkę z [Centrum pobierania Microsoft](https://www.microsoft.com/download/details.aspx?id=56503). Ręcznie przekaż wtyczkę udostępnioną przez firmę Microsoft za pomocą menu **Przekazywanie dodatku**. Pobieranie wtyczki jest objęte [umową serwisową firmy Microsoft](https://www.microsoft.com/servicesagreement/).

    ![Konfigurowanie logowania jednokrotnego](./media/confluencemicrosoft-tutorial/addon12.png)

4. Po zainstalowaniu wtyczki jest ona wyświetlana w sekcji dodatków **Zainstalowane przez użytkownika** w ramach sekcji **Zarządzanie dodatkami**. Kliknij pozycję **Configure** (Konfiguruj), aby skonfigurować nową wtyczkę.

    ![Konfigurowanie logowania jednokrotnego](./media/confluencemicrosoft-tutorial/addon13.png)

5. Wykonaj następujące kroki na stronie konfiguracji:

    ![Konfigurowanie logowania jednokrotnego](./media/confluencemicrosoft-tutorial/addon52.png)

    > [!TIP]
    > Upewnij się, że tylko jeden certyfikat jest zamapowany do aplikacji, aby zapobiec błędom podczas rozpoznawania metadanych. Jeśli dostępnych jest wiele certyfikatów, administrator otrzyma błąd podczas rozpoznawania metadanych.

    a. W polu tekstowym **Adres URL metadanych** wklej wartość pola **Adres URL metadanych federacyjnych aplikacji** skopiowaną z witryny Azure Portal i kliknij przycisk **Rozpoznaj**. Spowoduje to odczytanie adresu URL metadanych dostawcy tożsamości i wypełnienie wszystkich pól danymi.

    b. Skopiuj wartości **identyfikatora, adresu URL odpowiedzi i adresu URL logowania**, a następnie wklej je odpowiednio w polach tekstowych **Identyfikator, Adres URL odpowiedzi i Adres URL logowania** w sekcji **Podstawowa konfiguracja protokołu SAML** w witrynie Azure Portal.

    d. W polu **Nazwa przycisku logowania** wpisz nazwę przycisku, która według Twojej organizacji ma być wyświetlana użytkownikom na ekranie logowania.

    d. W polu **Lokalizacje identyfikatora użytkownika SAML** wybierz opcję **Identyfikator użytkownika znajduje się w elemencie NameIdentifier instrukcji Subject** lub **Identyfikator użytkownika znajduje się w elemencie Attribute**.  Ten identyfikator musi być identyfikatorem użytkownika aplikacji Confluence. Jeśli identyfikator użytkownika nie jest zgodny, system nie będzie zezwalać użytkownikom na logowanie. 

    > [!Note]
    > Domyślna lokalizacja identyfikatora użytkownika SAML to element NameIdentifier. Można ją zmienić za pomocą opcji elementu Attribute, podając nazwę odpowiedniego atrybutu.
    
    e. Jeśli wybierzesz pozycję **Identyfikator użytkownika znajduje się w elemencie Attribute**, w polu tekstowym **Nazwa atrybutu** wpisz nazwę atrybutu, w którym ma znajdować się identyfikator użytkownika. 

    f. Jeśli używasz domeny federacyjnej (na przykład usług ADFS itp.) w połączeniu z usługą Azure AD, kliknij opcję **Włącz odnajdywanie obszaru głównego** i skonfiguruj pole **Nazwa domeny**.
    
    g. W polu **Nazwa domeny** wpisz nazwę domeny w przypadku logowania za pomocą usług ADFS.

    h. Zaznacz pole **Włącz logowanie jednokrotne**, jeśli chcesz wylogować użytkownika z usługi Azure AD, gdy wyloguje się on z aplikacji Confluence. 

    i. Kliknij przycisk **Zapisz**, aby zapisać ustawienia.

    > [!NOTE]
    > Aby uzyskać więcej informacji na temat instalowania i rozwiązywania problemów, odwiedź stronę [MS Confluence SSO Connector Admin Guide (Podręcznik administratora łącznika logowania jednokrotnego firmy Microsoft dla aplikacji Confluence)](../ms-confluence-jira-plugin-adminguide.md). Dostępne są także [często zadawane pytania](../ms-confluence-jira-plugin-faq.md)

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

W tej sekcji włączysz użytkownikowi Britta Simon możliwość korzystania z logowania jednokrotnego platformy Azure, udzielając dostępu do aplikacji Confluence SAML SSO by Microsoft.

1. W witrynie Azure Portal wybierz pozycję **Aplikacje dla przedsiębiorstw**, wybierz pozycję **Wszystkie aplikacje**, a następnie wybierz pozycję **Confluence SAML SSO by Microsoft**.

    ![Blok Aplikacje dla przedsiębiorstw](common/enterprise-applications.png)

2. Na liście aplikacji wybierz pozycję **Confluence SAML SSO by Microsoft**.

    ![Link aplikacji Confluence SAML SSO by Microsoft na liście aplikacji](common/all-applications.png)

3. W menu po lewej stronie wybierz pozycję **Użytkownicy i grupy**.

    ![Link „Użytkownicy i grupy”](common/users-groups-blade.png)

4. Kliknij przycisk **Dodaj użytkownika**, a następnie wybierz pozycję **Użytkownicy i grupy** w oknie dialogowym **Dodawanie przypisania**.

    ![Okienko Dodawanie przypisania](common/add-assign-user.png)

5. W oknie dialogowym **Użytkownicy i grupy** wybierz użytkownika **Britta Simon** na liście użytkowników, a następnie kliknij przycisk **Wybierz** u dołu ekranu.

6. Jeśli oczekujesz wartości roli w asercji SAML, w oknie dialogowym **Wybieranie roli** wybierz z listy odpowiednią rolę dla użytkownika, a następnie kliknij przycisk **Wybierz** u dołu ekranu.

7. W oknie dialogowym **Dodawanie przypisania** kliknij przycisk **Przypisz**.

### <a name="create-confluence-saml-sso-by-microsoft-test-user"></a>Tworzenie użytkownika testowego aplikacji Confluence SAML SSO by Microsoft

Aby umożliwić użytkownikom usługi Azure AD logowanie do lokalnego serwera Confluence, należy ich aprowizować w aplikacji Confluence SAML SSO by Microsoft. W przypadku aplikacji Confluence SAML SSO by Microsoft aprowizowanie to zadanie wykonywane ręcznie.

**Aby aprowizować konto użytkownika, wykonaj następujące kroki:**

1. Zaloguj się do Twojego lokalnego serwera Confluence jako administrator.

2. Zatrzymaj wskaźnik myszy nad ikoną koła zębatego i kliknij pozycję **User management** (Zarządzanie użytkownikami).

    ![Dodawanie pracownika](./media/confluencemicrosoft-tutorial/user1.png) 

3. W sekcji Users (Użytkownicy) kliknij kartę **Add users** (Dodawanie użytkowników). Na stronie **Add a User** (Dodawanie użytkownika) okna dialogowego wykonaj następujące kroki:

    ![Dodawanie pracownika](./media/confluencemicrosoft-tutorial/user2.png) 

    a. W polu tekstowym **Username** (Nazwa użytkownika) wpisz adres e-mail użytkownika, np. Britta Simon.

    b. W polu tekstowym **Imię i nazwisko** wpisz imię i nazwisko użytkownika, na przykład Britta Simon.

    d. W polu tekstowym **Email** (Adres e-mail) wpisz adres e-mail użytkownika, np. Brittasimon@contoso.com.

    d. W polu tekstowym **Password** (Hasło) wpisz hasło użytkownika Britta Simon.

    e. Kliknij pozycję **Confirm Password** (Potwierdź hasło), a następnie ponownie wprowadź hasło.

    f. Kliknij przycisk **Add** (Dodaj).

### <a name="test-single-sign-on"></a>Testowanie logowania jednokrotnego 

W tej sekcji przetestujesz konfigurację logowania jednokrotnego usługi Azure AD przy użyciu panelu dostępu.

Po kliknięciu kafelka Confluence SAML SSO by Microsoft na panelu dostępu powinno nastąpić automatyczne zalogowanie do programu Confluence SAML SSO by Microsoft, dla którego skonfigurowano logowanie jednokrotne. Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [Introduction to the Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) (Wprowadzenie do panelu dostępu).

## <a name="additional-resources"></a>Dodatkowe zasoby

- [ Lista samouczków dotyczących sposobu integrowania aplikacji SaaS z usługą Azure Active Directory ](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list)

- [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)

- [Co to jest dostęp warunkowy w usłudze Azure Active Directory?](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)

