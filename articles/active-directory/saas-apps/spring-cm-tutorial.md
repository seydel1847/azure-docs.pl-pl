---
title: 'Samouczek: Integracja usługi Azure Active Directory z SpringCM | Dokumentacja firmy Microsoft'
description: Dowiedz się, jak skonfigurować logowanie jednokrotne między usługi Azure Active Directory i SpringCM.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 4a42f797-ac58-4aca-a8e6-53bfe5529083
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: 777586bc24c0962ec1f0ba3913397bfe26d0d0d5
ms.sourcegitcommit: 11d8ce8cd720a1ec6ca130e118489c6459e04114
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2018
ms.locfileid: "52841068"
---
# <a name="tutorial-azure-active-directory-integration-with-springcm"></a>Samouczek: Integracja usługi Azure Active Directory z SpringCM

W tym samouczku dowiesz się, jak zintegrować SpringCM w usłudze Azure Active Directory (Azure AD).

Integrowanie SpringCM z usługą Azure AD zapewnia następujące korzyści:

- Możesz kontrolować w usłudze Azure AD, kto ma dostęp do SpringCM
- Umożliwia użytkownikom automatyczne pobieranie zalogowanych do SpringCM (logowanie jednokrotne) przy użyciu konta usługi Azure AD
- Możesz zarządzać konta w jednej centralnej lokalizacji — witryny Azure portal

Jeśli chcesz dowiedzieć się więcej na temat integracji aplikacji SaaS z usługą Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Wymagania wstępne

Aby skonfigurować integrację usługi Azure AD za pomocą SpringCM, potrzebne są następujące elementy:

- Subskrypcji usługi Azure AD
- SpringCM logowanie jednokrotne włączone subskrypcji

> [!NOTE]
> Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.

Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:

- Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.
- Jeśli nie masz środowisko usługi Azure AD w wersji próbnej, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Opis scenariusza
W ramach tego samouczka można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym. Scenariusz opisany w tym samouczku składa się z dwóch głównych bloków konstrukcyjnych:

1. Dodawanie SpringCM z galerii
1. Konfigurowanie i testowania usługi Azure AD logowanie jednokrotne

## <a name="adding-springcm-from-the-gallery"></a>Dodawanie SpringCM z galerii
Aby skonfigurować integrację SpringCM w usłudze Azure AD, należy dodać SpringCM z galerii z listą zarządzanych aplikacji SaaS.

**Aby dodać SpringCM z galerii, wykonaj następujące czynności:**

1. W **[witryny Azure portal](https://portal.azure.com)**, w panelu nawigacyjnym po lewej stronie kliknij pozycję **usługi Azure Active Directory** ikony. 

    ![Usługa Active Directory][1]

1. Przejdź do **aplikacje dla przedsiębiorstw**. Następnie przejdź do **wszystkie aplikacje**.

    ![Aplikacje][2]
    
1. Aby dodać nową aplikację, kliknij **nową aplikację** przycisk u góry okna dialogowego.

    ![Aplikacje][3]

1. W polu wyszukiwania wpisz **SpringCM**.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/spring-cm-tutorial/tutorial_springcm_search.png)

1. W panelu wyników wybierz **SpringCM**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/spring-cm-tutorial/tutorial_springcm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurowanie i testowania usługi Azure AD logowanie jednokrotne
W tej sekcji Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne za pomocą SpringCM w oparciu o użytkownika testu o nazwie "Britta Simon."

Dla logowania jednokrotnego do pracy usługi Azure AD musi znać użytkownika odpowiednika w SpringCM do użytkownika w usłudze Azure AD. Innymi słowy relację łącza między użytkownika usługi Azure AD i powiązanego użytkownika w SpringCM musi można ustanowić.

W SpringCM, należy przypisać wartość **nazwa_użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łączy.

Aby skonfigurować i testowanie usługi Azure AD logowanie jednokrotne za pomocą SpringCM, należy wykonać poniższe bloki konstrukcyjne:

1. **[Konfigurowanie usługi Azure AD logowania jednokrotnego](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.
1. **[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD logowanie jednokrotne za pomocą Britta Simon.
1. **[Tworzenie użytkownika testowego SpringCM](#creating-a-springcm-test-user)**  — aby odpowiednikiem Britta Simon w SpringCM połączonego z usługi Azure AD reprezentacja użytkownika.
1. **[Przypisywanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — Aby włączyć Britta Simon korzystać z usługi Azure AD logowania jednokrotnego.
1. **[Testowanie logowania jednokrotnego](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurowanie usługi Azure AD logowania jednokrotnego

W tej sekcji możesz włączyć usługi Azure AD logowania jednokrotnego w witrynie Azure portal i konfigurowanie logowania jednokrotnego w aplikacji SpringCM.

**Aby skonfigurować usługę Azure AD logowanie jednokrotne z SpringCM, wykonaj następujące czynności:**

1. W witrynie Azure portal na **SpringCM** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.

    ![Konfigurowanie logowania jednokrotnego][4]

1. Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **opartej na SAML logowania jednokrotnego** włączyć logowanie jednokrotne.
 
    ![Konfigurowanie logowania jednokrotnego](./media/spring-cm-tutorial/tutorial_springcm_samlbase.png)

1. Na **SpringCM domena i adresy URL** sekcji, wykonaj następujące czynności:

    ![Konfigurowanie logowania jednokrotnego](./media/spring-cm-tutorial/tutorial_springcm_url.png)

    W **adres URL logowania** pole tekstowe, wpisz adres URL przy użyciu następującego wzorca: `https://na11.springcm.com/atlas/SSO/SSOEndpoint.ashx?aid=<identifier>`

    > [!NOTE] 
    > Ta wartość nie jest prawdziwe. Zaktualizuj tę wartość przy użyciu rzeczywisty adres URL logowania. Skontaktuj się z pomocą [zespołem pomocy technicznej klienta SpringCM](https://knowledge.springcm.com/support) aby zyskać tę wartość. 
 
1. Na **certyfikat podpisywania SAML** kliknij **Certificate(Raw)** , a następnie zapisz plik certyfikatu na komputerze.

    ![Konfigurowanie logowania jednokrotnego](./media/spring-cm-tutorial/tutorial_springcm_certificate.png) 

1. Kliknij przycisk **Zapisz** przycisku.

    ![Konfigurowanie logowania jednokrotnego](./media/spring-cm-tutorial/tutorial_general_400.png)

1. Na **konfiguracji SpringCM** , kliknij przycisk **skonfigurować SpringCM** otworzyć **Konfigurowanie logowania jednokrotnego** okna. Kopiuj **identyfikator jednostki języka SAML i SAML pojedynczego logowania jednokrotnego adres URL usługi** z **krótki przewodnik po sekcji.**

    ![Konfigurowanie logowania jednokrotnego](./media/spring-cm-tutorial/tutorial_springcm_configure.png)     

1. W oknie przeglądarki internetowej innej, zaloguj się na swoje **SpringCM** witryny firmy jako administrator.

1. W menu u góry kliknij **przejdź do**, kliknij przycisk **preferencje**, a następnie w **preferencje konta** kliknij **logowania jednokrotnego SAML**.
   
    ![LOGOWANIA JEDNOKROTNEGO SAML](./media/spring-cm-tutorial/ic797051.png "LOGOWANIA JEDNOKROTNEGO SAML")

1. W sekcji konfiguracji dostawcy tożsamości wykonaj następujące czynności:
   
    ![Konfiguracja dostawcy tożsamości](./media/spring-cm-tutorial/ic797052.png "konfiguracji dostawcy tożsamości")
    
    a. Aby przekazać pobrany certyfikat usługi Azure Active Directory, kliknij przycisk **Wybieranie certyfikatu wystawcy** lub **zmiany wystawcy certyfikatu**.
    
    b. Wklej **identyfikator jednostki SAML** wartości, które zostały skopiowane z witryny Azure portal do **wystawcy** pola tekstowego.
    
    c. Wklej **SAML pojedynczego logowania jednokrotnego usługi adresu URL** wartości, które zostały skopiowane z witryny Azure portal do **usługi dostawcy (SP) zainicjowane w punkcie końcowym** pola tekstowego.
            
    d. Wybierz **SAML włączone** jako **Włącz**.

    e. Kliknij pozycję **Zapisz**.
 
> [!TIP]
> Teraz mogą odczytywać zwięzłe wersji tych instrukcji wewnątrz [witryny Azure portal](https://portal.azure.com), podczas gdy konfigurujesz aplikacji!  Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij pozycję **logowania jednokrotnego** karty i uzyskać dostęp do osadzonych dokumentacji za pośrednictwem  **Konfiguracja** sekcji u dołu. Możesz dowiedzieć się więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacja embedded usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Tworzenie użytkownika testowego usługi Azure AD
Celem tej sekcji jest tworzenie użytkownika testowego w witrynie Azure portal, o nazwie Britta Simon.

![Utwórz użytkownika usługi Azure AD][100]

**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**

1. W **witryny Azure portal**, w okienku nawigacji po lewej stronie kliknij **usługi Azure Active Directory** ikony.

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/spring-cm-tutorial/create_aaduser_01.png) 

1. Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/spring-cm-tutorial/create_aaduser_02.png) 

1. Aby otworzyć **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry okna dialogowego.
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/spring-cm-tutorial/create_aaduser_03.png) 

1. Na **użytkownika** okna dialogowego strony, wykonaj następujące czynności:
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/spring-cm-tutorial/create_aaduser_04.png) 

    a. W **nazwa** polu tekstowym wpisz **BrittaSimon**.

    b. W **nazwa_użytkownika** polu tekstowym wpisz **adres e-mail** z BrittaSimon.

    c. Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.

    d. Kliknij pozycję **Utwórz**.
 
### <a name="creating-a-springcm-test-user"></a>Tworzenie użytkownika testowego SpringCM

Aby umożliwić użytkownikom usługi Azure Active Directory, zaloguj się do SpringCM, musi być obsługiwana w SpringCM. W przypadku SpringCM Inicjowanie obsługi administracyjnej jest zadanie ręczne.

>[!NOTE]
>Aby uzyskać więcej informacji, zobacz [tworzenie i edytowanie użytkownika SpringCM](https://knowledge.springcm.com/create-and-edit-a-springcm-user). 

**Aby udostępnić konto SpringCM, wykonaj następujące czynności:**

1. Zaloguj się do Twojej **SpringCM** witryny firmy jako administrator.

1. Kliknij przycisk **GOTO**, a następnie kliknij przycisk **KSIĄŻKI ADRESOWEJ**.
   
    ![Tworzenie użytkownika](./media/spring-cm-tutorial/ic797054.png "Tworzenie użytkownika")

1. Kliknij przycisk **Utwórz użytkownika**.

1. Wybierz **roli użytkownika**.

1. Wybierz **wysyłania wiadomości e-mail dotyczącej aktywacji**.

1. Wpisz imię, nazwisko i adres e-mail prawidłowe konto użytkownika usługi Azure Active Directory, które chcesz aprowizować do powiązanych pól tekstowych.

1. Dodaj użytkownika do **grupy zabezpieczeń**.

1. Kliknij pozycję **Zapisz**.

  >[!NOTE]
  >Można użyć jakichkolwiek innych SpringCM użytkownika konta tworzenie narzędzi lub interfejsów API dostarczonych przez SpringCM do aprowizacji kont użytkowników usługi AAD.  
  > 

### <a name="assigning-the-azure-ad-test-user"></a>Przypisywanie użytkownika testowego usługi Azure AD

W tej sekcji możesz włączyć Britta Simon do używania usługi Azure logowanie jednokrotne za udzielanie dostępu do SpringCM.

![Przypisz użytkownika][200] 

**Aby przypisać Britta Simon SpringCM, wykonaj następujące czynności:**

1. W witrynie Azure portal Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.

    ![Przypisz użytkownika][201] 

1. Na liście aplikacji wybierz **SpringCM**.

    ![Konfigurowanie logowania jednokrotnego](./media/spring-cm-tutorial/tutorial_springcm_app.png) 

1. W menu po lewej stronie kliknij **użytkowników i grup**.

    ![Przypisz użytkownika][202] 

1. Kliknij przycisk **Dodaj** przycisku. Następnie wybierz pozycję **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.

    ![Przypisz użytkownika][203]

1. Na **użytkowników i grup** okno dialogowe, wybierz opcję **Britta Simon** na liście Użytkownicy.

1. Kliknij przycisk **wybierz** znajdujący się na **użytkowników i grup** okna dialogowego.

1. Kliknij przycisk **przypisać** znajdujący się na **Dodaj przydziału** okna dialogowego.
    
### <a name="testing-single-sign-on"></a>Testowanie logowania jednokrotnego

W tej sekcji służy do testowania konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu panelu dostępu.
 
Po kliknięciu kafelka SpringCM w panelu dostępu, użytkownik powinien uzyskać automatycznie zalogowanych do aplikacji SpringCM.

Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](../user-help/active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Zasoby dodatkowe

* [Lista samouczków dotyczących integrowania aplikacji SaaS w usłudze Azure Active Directory](tutorial-list.md)
* [Czym jest dostęp do aplikacji i logowanie jednokrotne za pomocą usługi Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/spring-cm-tutorial/tutorial_general_01.png
[2]: ./media/spring-cm-tutorial/tutorial_general_02.png
[3]: ./media/spring-cm-tutorial/tutorial_general_03.png
[4]: ./media/spring-cm-tutorial/tutorial_general_04.png

[100]: ./media/spring-cm-tutorial/tutorial_general_100.png

[200]: ./media/spring-cm-tutorial/tutorial_general_200.png
[201]: ./media/spring-cm-tutorial/tutorial_general_201.png
[202]: ./media/spring-cm-tutorial/tutorial_general_202.png
[203]: ./media/spring-cm-tutorial/tutorial_general_203.png

