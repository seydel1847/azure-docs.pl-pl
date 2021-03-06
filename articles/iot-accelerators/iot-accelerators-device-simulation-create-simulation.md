---
title: Tworzenie nowej symulacji usługi IoT — Azure | Microsoft Docs
description: W tym samouczku użyjesz symulacji urządzenia do utworzenia i uruchomienia nowej symulacji.
author: troyhopwood
manager: timlt
ms.service: iot-accelerators
services: iot-accelerators
ms.topic: tutorial
ms.custom: mvc
ms.date: 10/25/2018
ms.author: troyhop
ms.openlocfilehash: 268efa35f63ac8b9e0c6ea3f22a71242a2984726
ms.sourcegitcommit: 3dcb1a3993e51963954194ba2a5e42260d0be258
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/01/2018
ms.locfileid: "50756851"
---
# <a name="tutorial-create-and-run-an-iot-device-simulation"></a>Samouczek: tworzenie i uruchamianie symulacji urządzenia usługi IoT

W tym samouczku użyjesz symulacji urządzenia do utworzenia i uruchomienia nowej symulacji usługi IoT, która będzie korzystać z co najmniej jednego urządzenia symulowanego.

W tym samouczku zostaną wykonane następujące czynności:

>[!div class="checklist"]
> * Wyświetlanie wszystkich symulacji aktywnych i historycznych
> * Tworzenie i uruchamianie nowej symulacji
> * Wyświetlanie metryk symulacji
> * Zatrzymywanie symulacji

Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).

## <a name="prerequisites"></a>Wymagania wstępne

Do wykonania kroków tego samouczka będzie potrzebne wdrożone wystąpienie symulacji urządzenia w subskrypcji platformy Azure.

Jeśli nie wdrożono jeszcze symulacji urządzenia, należy wykonać czynności opisane w przewodniku Szybki start [Wdrażanie i uruchamianie symulacji urządzenia usługi IoT na platformie Azure](quickstart-device-simulation-deploy.md).

## <a name="open-device-simulation"></a>Otwieranie symulacji urządzenia

Aby uruchomić symulację urządzenia w przeglądarce, przejdź najpierw do [akceleratorów rozwiązań usługi Microsoft Azure IoT](https://www.azureiotsolutions.com). 

Może być konieczne zalogowanie się przy użyciu poświadczeń subskrypcji platformy Azure.

Następnie kliknij pozycję **Uruchom** na kafelku symulacji urządzenia, którą wdrożono w ramach [przewodnika Szybki start](quickstart-device-simulation-deploy.md).

## <a name="view-simulations"></a>Wyświetlanie symulacji

Wybierz pozycję **Symulacje** na pasku menu. Strona **Symulacje** zawiera informacje na temat wszystkich dostępnych symulacji. Na tej stronie można zobaczyć symulacje działające w danej chwili oraz symulacje uruchomione wcześniej. Aby ponownie uruchomić poprzednią symulację, kliknij kafelek symulacji w celu otwarcia jej szczegółów:

![Symulacje](media/iot-accelerators-device-simulation-create-simulation/dashboard.png)

## <a name="create-a-simulation"></a>Tworzenie symulacji

Aby utworzyć symulację, kliknij pozycję **+ Nowa symulacja** w prawym górnym rogu.

Symulacja składa się z co najmniej jednego modelu urządzenia. Model urządzenia definiuje zachowanie, telemetrię i format wiadomości komunikatów urządzenia, które ma być symulowane.

Aby dodać model urządzenia, kliknij pozycję **+ Dodaj typ urządzenia** i z listy wybierz model urządzenia. Symulacja może obejmować więcej niż jeden model urządzenia. Każdy model urządzenia może mieć inną liczbę urządzeń i częstotliwość komunikatów.

Po ukończeniu formularza nowej symulacji kliknij pozycję **Rozpocznij symulację**, aby uruchomić symulację.

W zależności od liczby urządzeń symulowanych skonfigurowanie i uruchomienie symulacji może potrwać kilka minut:

![Nowa symulacja](media/iot-accelerators-device-simulation-create-simulation/newsimulation.png)

## <a name="stop-a-simulation"></a>Zatrzymywanie symulacji

Po kliknięciu pozycji **Rozpocznij symulację** zostanie wyświetlona strona szczegółów symulacji. Ta strona szczegółów zawiera statystyki i metryki symulacji pobierane na żywo z usługi IoT Hub. Możesz także przejść do tej strony szczegółów, klikając kafelek symulacji na stronie **Symulacje**.

Aby zakończyć symulację, kliknij pozycję **Zatrzymaj symulację** na pasku akcji w prawym górnym rogu.

![Zatrzymywanie symulacji](media/iot-accelerators-device-simulation-create-simulation/simulationdetails.png)

## <a name="next-steps"></a>Następne kroki

W tym samouczku przedstawiono sposób tworzenia, uruchamiania i zatrzymywania symulacji. Pokazano również, jak wyświetlać szczegóły symulacji. Aby dowiedzieć się więcej na temat sposobu uruchamiania symulacji, przejdź do następnego samouczka:

> [!div class="nextstepaction"]
> [Utwórz niestandardowe urządzenie symulowane](iot-accelerators-device-simulation-create-custom-device.md)
