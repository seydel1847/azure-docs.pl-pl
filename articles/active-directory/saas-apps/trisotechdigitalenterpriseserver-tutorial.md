---
title: 'Samouczek: Integracja usługi Azure Active Directory z Trisotech cyfrowe serwera Enterprise | Dokumentacja firmy Microsoft'
description: Dowiedz się, jak skonfigurować logowanie jednokrotne między usługi Azure Active Directory i Trisotech cyfrowe serwera Enterprise.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 6d54d20c-eca1-4fa6-b56a-4c3ed0593db0
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/16/2018
ms.author: jeedes
ms.openlocfilehash: e36a4be3a95b67c040855171d4b167e495a22496
ms.sourcegitcommit: 1d850f6cae47261eacdb7604a9f17edc6626ae4b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/02/2018
ms.locfileid: "39439630"
---
# <a name="tutorial-azure-active-directory-integration-with-trisotech-digital-enterprise-server"></a>Samouczek: Integracja usługi Azure Active Directory z Trisotech cyfrowego Enterprise Server

W tym samouczku dowiesz się, jak zintegrować Trisotech cyfrowe serwera przedsiębiorstwa za pomocą usługi Azure Active Directory (Azure AD).

Integrowanie Trisotech cyfrowego Enterprise Server z usługą Azure AD zapewnia następujące korzyści:

- Możesz kontrolować, czy w usłudze Azure AD, kto ma dostęp do Trisotech cyfrowe serwera przedsiębiorstwa.
- Użytkowników, aby automatycznie uzyskać zalogowanych do Trisotech cyfrowego Enterprise Server (logowanie jednokrotne) można włączyć za pomocą kont usługi Azure AD.
- Możesz zarządzać konta w jednej centralnej lokalizacji — witryny Azure portal.

Jeśli chcesz dowiedzieć się więcej na temat integracji aplikacji SaaS z usługą Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Wymagania wstępne

Do konfigurowania integracji z usługą Azure AD z Trisotech cyfrowego Enterprise Server, potrzebne są następujące elementy:

- Subskrypcję usługi Azure AD
- Trisotech cyfrowe serwera przedsiębiorstwa logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.

Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:

- Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.
- Jeśli nie masz środowisko usługi Azure AD w wersji próbnej, możesz to zrobić [miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W ramach tego samouczka można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz opisany w tym samouczku składa się z dwóch głównych bloków konstrukcyjnych:

1. Dodawanie Trisotech cyfrowego Enterprise Server z galerii
1. Konfigurowanie i testowania usługi Azure AD logowanie jednokrotne

## <a name="adding-trisotech-digital-enterprise-server-from-the-gallery"></a>Dodawanie Trisotech cyfrowego Enterprise Server z galerii
Aby skonfigurować integrację Trisotech cyfrowego Enterprise Server w usłudze Azure AD, należy dodać Trisotech cyfrowego Enterprise Server z galerii z listą zarządzanych aplikacji SaaS.

**Aby dodać Trisotech cyfrowego Enterprise Server z galerii, wykonaj następujące czynności:**

1. W  **[witryny Azure portal](https://portal.azure.com)**, w panelu nawigacyjnym po lewej stronie kliknij pozycję **usługi Azure Active Directory** ikony. 

    ![Przycisk usługi Azure Active Directory][1]

1. Przejdź do **aplikacje dla przedsiębiorstw**. Następnie przejdź do **wszystkie aplikacje**.

    ![W bloku aplikacji przedsiębiorstwa][2]
    
1. Aby dodać nową aplikację, kliknij **nową aplikację** przycisk u góry okna dialogowego.

    ![Nowy przycisk aplikacji][3]

1. W polu wyszukiwania wpisz **Trisotech cyfrowego Enterprise Server**, wybierz opcję **Trisotech cyfrowego Enterprise Server** z panelu wynik kliknięcie **Dodaj** przycisk, aby dodać aplikacja.

    ![Trisotech cyfrowe Enterprise serwera na liście wyników](./media/trisotechdigitalenterpriseserver-tutorial/tutorial_trisotechdigitalenterpriseserver_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfiguracja i testowanie usługi Azure AD logowania jednokrotnego

W tej sekcji możesz skonfigurować i testowanie usługi Azure AD logowanie jednokrotne za pomocą Trisotech cyfrowe serwera przedsiębiorstw oparte na użytkownika testu o nazwie "Britta Simon".

Dla logowania jednokrotnego do pracy usługi Azure AD musi znać użytkownika odpowiednika w Trisotech cyfrowego Enterprise Server dla użytkownika w usłudze Azure AD. Oznacza to relację łącza między użytkownika usługi Azure AD i powiązanego użytkownika w Trisotech cyfrowego Enterprise Server musi zostać ustanowione.

Aby skonfigurować i testowanie usługi Azure AD logowanie jednokrotne za pomocą Trisotech cyfrowego Enterprise Server, należy wykonać poniższe bloki konstrukcyjne:

1. **[Konfigurowanie usługi Azure AD logowania jednokrotnego](#configure-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.
1. **[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD logowanie jednokrotne za pomocą Britta Simon.
1. **[Tworzenie użytkownika testowego Trisotech cyfrowego Enterprise Server](#create-a-trisotech-digital-enterprise-server-test-user)**  — aby odpowiednikiem Britta Simon w Trisotech cyfrowego Enterprise Server, która jest połączona z usługi Azure AD reprezentacja użytkownika.
1. **[Przypisywanie użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)**  — Aby włączyć Britta Simon korzystać z usługi Azure AD logowania jednokrotnego.
1. **[Testowanie logowania jednokrotnego](#test-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.

### <a name="configure-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD logowania jednokrotnego

W tej sekcji możesz włączyć usługi Azure AD logowania jednokrotnego w witrynie Azure portal i konfigurowanie logowania jednokrotnego w aplikacji Trisotech cyfrowego Enterprise Server.

**Aby skonfigurować usługę Azure AD logowanie jednokrotne z Trisotech cyfrowego Enterprise Server, wykonaj następujące czynności:**

1. W witrynie Azure portal na **Trisotech cyfrowego Enterprise Server** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

1. Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **opartej na SAML logowania jednokrotnego** włączyć logowanie jednokrotne.
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/trisotechdigitalenterpriseserver-tutorial/tutorial_trisotechdigitalenterpriseserver_samlbase.png)

1. Na **Trisotech cyfrowego Enterprise Server domena i adresy URL** sekcji, wykonaj następujące czynności:

    ![Trisotech cyfrowego Enterprise Server domena i adresy URL pojedynczego logowania jednokrotnego informacji](./media/trisotechdigitalenterpriseserver-tutorial/tutorial_trisotechdigitalenterpriseserver_url.png)

    a. W **adres URL logowania** pole tekstowe, wpisz adres URL przy użyciu następującego wzorca: `https://<companyname>.trisotech.com`

    b. W **identyfikator** pole tekstowe, wpisz adres URL przy użyciu następującego wzorca: `https://<companyname>.trisotech.com`

    > [!NOTE] 
    > Te wartości są prawdziwe. Zaktualizuj te wartości przy użyciu rzeczywistego adresu URL logowania jednokrotnego i identyfikator. Skontaktuj się z pomocą [zespołem pomocy technicznej Trisotech cyfrowego Enterprise Server Client](mailto:support@trisotech.com) do uzyskania tych wartości.

1. Na **certyfikat podpisywania SAML** sekcji, kliknij przycisk kopiowania, aby skopiować **adres Url metadanych Federacji aplikacji** i wklej go w Notatniku. 

    ![Link pobierania certyfikatu](./media/trisotechdigitalenterpriseserver-tutorial/tutorial_trisotechdigitalenterpriseserver_certificate.png)

1. Kliknij przycisk **Zapisz** przycisku.

    ![Konfigurowanie pojedynczego logowania jednokrotnego Zapisz przycisku](./media/trisotechdigitalenterpriseserver-tutorial/tutorial_general_400.png)

1. W oknie przeglądarki innej witryny sieci web należy zalogować się jako administrator do witryny firmy Trisotech cyfrowego Enterprise serwera konfiguracji.

1. Kliknij pozycję **ikonę Menu** , a następnie wybierz **administracji**.

    ![Konfigurowanie logowania jednokrotnego](./media/trisotechdigitalenterpriseserver-tutorial/user1.png)

1. Wybierz **dostawca użytkownika**.

    ![Konfigurowanie logowania jednokrotnego](./media/trisotechdigitalenterpriseserver-tutorial/user2.png)

1. W **konfiguracji dostawcy użytkowników** sekcji, wykonaj następujące czynności:

    ![Konfigurowanie logowania jednokrotnego](./media/trisotechdigitalenterpriseserver-tutorial/user3.png)

    a. Wybierz **zabezpieczone Assertion Markup języka 2 (SAML 2)** z listy rozwijanej w **metodę uwierzytelniania**.

    b. W **adres URL metadanych** pola tekstowego, Wklej **adres Url metadanych Federacji aplikacji** wartość, która została skopiowana tworzą witryny Azure portal.

    c. W **identyfikator aplikacji** polu tekstowym wprowadź adres URL, za pomocą następującego wzorca: `https://<companyname>.trisotech.com`.

    d. Kliknij pozycję **Zapisz**

    e. Wprowadź nazwę domeny w **domen z dozwolone (wartość empty oznacza każdy)** pola tekstowego, automatycznie przypisuje licencji dla użytkowników zgodnych domen dozwolone

    f. Kliknij pozycję **Zapisz**

 ### <a name="create-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD

Celem tej sekcji jest tworzenie użytkownika testowego w witrynie Azure portal, o nazwie Britta Simon.

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**

1. W witrynie Azure portal w okienku po lewej stronie kliknij pozycję **usługi Azure Active Directory** przycisku.

    ![Przycisk usługi Azure Active Directory](./media/trisotechdigitalenterpriseserver-tutorial/create_aaduser_01.png)

1. Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.

    !["Użytkownicy i grupy" i "All users" linki](./media/trisotechdigitalenterpriseserver-tutorial/create_aaduser_02.png)

1. Aby otworzyć **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** w górnej części **wszyscy użytkownicy** okno dialogowe.

    ![Przycisk Dodaj](./media/trisotechdigitalenterpriseserver-tutorial/create_aaduser_03.png)

1. W **użytkownika** okna dialogowego pole, wykonaj następujące czynności:

    ![Okno dialogowe użytkownika](./media/trisotechdigitalenterpriseserver-tutorial/create_aaduser_04.png)

    a. W **nazwa** wpisz **BrittaSimon**.

    b. W **nazwa_użytkownika** wpisz adres e-mail użytkownika Britta Simon.

    c. Wybierz **Pokaż hasło** pole wyboru, a następnie zapisz wartość, która jest wyświetlana w **hasło** pole.

    d. Kliknij pozycję **Utwórz**.
 
### <a name="create-a-trisotech-digital-enterprise-server-test-user"></a>Tworzenie użytkownika testowego Trisotech cyfrowego Enterprise Server

Celem tej sekcji jest utworzyć użytkownika o nazwie Britta Simon Trisotech cyfrowego Server Enterprise. Cyfrowe serwera Enterprise Trisotech obsługę just-in-time, który jest domyślnie włączona. Brak elementu akcji dla Ciebie w tej sekcji. Nowy użytkownik jest tworzony podczas próby dostępu Trisotech cyfrowego Enterprise Server, jeśli go jeszcze nie istnieje.
>[!Note]
>Jeśli musisz ręcznie utworzyć użytkownika, skontaktuj się z [zespołem pomocy technicznej Trisotech cyfrowego Enterprise Server](mailto:support@trisotech.com).

### <a name="assign-the-azure-ad-test-user"></a>Przypisywanie użytkownika testowego usługi Azure AD

W tej sekcji możesz włączyć Britta Simon do używania platformy Azure logowanie jednokrotne za udzielanie dostępu do Trisotech cyfrowego Enterprise Server.

![Przypisanie roli użytkownika][200] 

**Aby przypisać Britta Simon Trisotech cyfrowego Enterprise Server, wykonaj następujące czynności:**

1. W witrynie Azure portal Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

1. Na liście aplikacji wybierz **Trisotech cyfrowego Enterprise Server**.

    ![Link Trisotech cyfrowego Enterprise Server, na liście aplikacji](./media/trisotechdigitalenterpriseserver-tutorial/tutorial_trisotechdigitalenterpriseserver_app.png)  

1. W menu po lewej stronie kliknij **użytkowników i grup**.

    ![Link "Użytkownicy i grupy"][202]

1. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz pozycję **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Okienko Dodawanie przypisania][203]

1. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Britta Simon** na liście Użytkownicy.

1. Kliknij przycisk **wybierz** znajdujący się na **użytkowników i grup** okna dialogowego.

1. Kliknij przycisk **przypisać** znajdujący się na **Dodaj przydziału** okna dialogowego.
    
### <a name="test-single-sign-on"></a>Testowanie logowania jednokrotnego

W tej sekcji służy do testowania konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu panelu dostępu.

Po kliknięciu kafelka Trisotech cyfrowego Enterprise Server, w panelu dostępu, możesz należy pobrać automatycznie zalogowanych do aplikacji Trisotech cyfrowego Enterprise Server.
Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](../user-help/active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Zasoby dodatkowe

* [Lista samouczków dotyczących integrowania aplikacji SaaS w usłudze Azure Active Directory](tutorial-list.md)
* [Czym jest dostęp do aplikacji i logowanie jednokrotne za pomocą usługi Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/trisotechdigitalenterpriseserver-tutorial/tutorial_general_01.png
[2]: ./media/trisotechdigitalenterpriseserver-tutorial/tutorial_general_02.png
[3]: ./media/trisotechdigitalenterpriseserver-tutorial/tutorial_general_03.png
[4]: ./media/trisotechdigitalenterpriseserver-tutorial/tutorial_general_04.png

[100]: ./media/trisotechdigitalenterpriseserver-tutorial/tutorial_general_100.png

[200]: ./media/trisotechdigitalenterpriseserver-tutorial/tutorial_general_200.png
[201]: ./media/trisotechdigitalenterpriseserver-tutorial/tutorial_general_201.png
[202]: ./media/trisotechdigitalenterpriseserver-tutorial/tutorial_general_202.png
[203]: ./media/trisotechdigitalenterpriseserver-tutorial/tutorial_general_203.png

