---
author: dominicbetts
ms.service: iot-hub
ms.topic: include
ms.date: 10/26/2018
ms.author: dobett
ms.openlocfilehash: 13eddced155eab6dedfbce77330e7a178ecfb3cb
ms.sourcegitcommit: 48592dd2827c6f6f05455c56e8f600882adb80dc
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/26/2018
ms.locfileid: "50164283"
---
> [!div class="op_single_selector"]
> * [Urządzenie: Node.js, usługa: Node.js](../articles/iot-hub/iot-hub-node-node-device-management-get-started.md)
> * [Urządzenie: C# usługi:C#](../articles/iot-hub/iot-hub-csharp-csharp-device-management-get-started.md)
> * [Urządzenie: Usługa Java: Java](../articles/iot-hub/iot-hub-java-java-device-management-getstarted.md)
> * [Urządzenie: Usługa języka Python: języka Python](../articles/iot-hub/iot-hub-python-python-device-management-get-started.md)

Serwer zaplecza w aplikacji można używać usługi Azure IoT Hub w nim elementów podstawowych, takich jak [bliźniaczej reprezentacji urządzenia] [ lnk-devtwin] i [metody bezpośrednie][lnk-c2dmethod], aby zdalnie uruchomić i monitorować urządzenia akcje z zakresu zarządzania na urządzeniach. Ten samouczek pokazuje, jak aplikacji zaplecza i aplikacji urządzenia mogą pracować razem inicjowania i monitorowania ponownego uruchomienia urządzenia zdalnego za pomocą usługi IoT Hub.

[!INCLUDE [iot-hub-basic](iot-hub-basic-whole.md)]

Użyj metody bezpośredniej do zainicjowania akcji zarządzania urządzeniami (na przykład ponowne uruchomienie komputera, resetowanie do ustawień fabrycznych i aktualizacja oprogramowania układowego) z poziomu aplikacji zaplecza w chmurze. Urządzenie jest odpowiedzialny za:

* Obsługa żądanie metody wysyłane z usługi IoT Hub.
* Inicjowanie odpowiednich czynności specyficznych dla urządzenia na urządzeniu.
* Dostarczanie aktualizacji stanu za pośrednictwem *zgłaszanych właściwości* do usługi IoT Hub.

Uruchamianie zapytań bliźniaczych reprezentacji urządzeń do raportowania postępu działań zarządzania urządzeniami, można użyć aplikacji zaplecza w chmurze.

[lnk-devtwin]: ../articles/iot-hub/iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
