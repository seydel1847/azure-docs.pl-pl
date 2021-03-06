---
title: Przekazywanie plików z urządzeń do usługi Azure IoT Hub za pomocą języka Python | Dokumentacja firmy Microsoft
description: Sposób przekazywania plików z urządzenia do chmury przy użyciu zestawu SDK urządzeń Azure IoT dla języka Python. Przekazane pliki są przechowywane w kontenerze obiektów blob usługi Azure storage.
author: kgremban
manager: timlt
ms.service: iot-hub
services: iot-hub
ms.devlang: python
ms.topic: conceptual
ms.date: 03/05/2018
ms.author: kgremban
ms.openlocfilehash: 193bc3a4eafcdff5d5f28d916afa4600b20c0d86
ms.sourcegitcommit: 5a1d601f01444be7d9f405df18c57be0316a1c79
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/10/2018
ms.locfileid: "51514740"
---
# <a name="upload-files-from-your-device-to-the-cloud-with-iot-hub"></a>Przekazywanie plików z urządzenia do chmury za pomocą usługi IoT Hub

[!INCLUDE [iot-hub-file-upload-language-selector](../../includes/iot-hub-file-upload-language-selector.md)]

W tym samouczku poniżej sposób użycia [pliku przekazywania możliwościami usługi IoT Hub](iot-hub-devguide-file-upload.md) można przekazać pliku do [usługi Azure blob storage](../storage/index.yml). Ten samouczek przedstawia sposób wykonania następujących czynności:

- Kontener magazynu można bezpiecznie przekazać do przekazywania pliku.
- Użyj klienta języka Python, aby przekazać plik za pomocą usługi IoT hub.

[Rozpoczynanie pracy z usługą IoT Hub](quickstart-send-telemetry-node.md) samouczku przedstawiono podstawowe funkcje obsługi komunikatów urządzenia do chmury usługi IoT Hub. Jednak w niektórych scenariuszach nie pozwala na łatwe mapowanie danych wysyłanych przez urządzenia do stosunkowo mały wiadomości urządzenia do chmury, które akceptuje usługi IoT Hub. Gdy zachodzi potrzeba wyżynne plików z urządzenia, można nadal używać zabezpieczeń i niezawodności usługi IoT Hub.

> [!NOTE]
> IoT Hub Python SDK aktualnie obsługuje tylko przekazywania plików opartego na znakach, takich jak **.txt** plików.

Na końcu tego samouczka, możesz uruchomić aplikację konsoli języka Python:

* **FileUpload.py**, która przekazuje plik do magazynu przy użyciu zestawu SDK urządzenia środowiska Python.

> [!NOTE]
> Centrum IoT Hub obsługuje wiele platform urządzeń i językach (w tym C, .NET, Javascript, Python i Java) za pomocą zestawów SDK urządzeń Azure IoT. Zapoznaj się [Centrum deweloperów Azure IoT] instrukcje krok po kroku dotyczące sposobu Podłącz urządzenie do usługi Azure IoT Hub.

Do wykonania kroków tego samouczka niezbędne są następujące elementy:

* [Środowisko Python 2.x lub 3.x][lnk-python-download]. Upewnij się, że używasz 32-bitowej lub 64-bitowej instalacji zgodnie z wymaganiami konfiguracji. Po wyświetleniu monitu podczas instalacji upewnij się, że język Python został dodany do zmiennej środowiskowej specyficznej dla platformy. Jeśli używasz środowiska Python 2.x, może być konieczne [zainstalowanie lub uaktualnienie systemu zarządzania pakietami języka Python — *pip*][lnk-install-pip].
* [Pakiet redystrybucyjny języka Visual C++][lnk-visual-c-redist] (jeśli używasz systemu operacyjnego Windows) umożliwiający korzystanie z natywnych bibliotek DLL języka Python.
* Aktywne konto platformy Azure. (Jeśli nie masz konta, możesz utworzyć [bezpłatne konto](https://azure.microsoft.com/pricing/free-trial/) w zaledwie kilka minut.)

## <a name="create-an-iot-hub"></a>Tworzenie centrum IoT Hub

[!INCLUDE [iot-hub-include-create-hub](../../includes/iot-hub-include-create-hub.md)]

### <a name="retrieve-connection-string-for-iot-hub"></a>Pobieranie parametrów połączenia dla Centrum IoT hub

[!INCLUDE [iot-hub-include-find-connection-string](../../includes/iot-hub-include-find-connection-string.md)]

## <a name="register-a-new-device-in-the-iot-hub"></a>Rejestrowanie nowego urządzenia w usłudze IoT hub

[!INCLUDE [iot-hub-include-create-device](../../includes/iot-hub-include-create-device.md)]

[!INCLUDE [iot-hub-associate-storage](../../includes/iot-hub-associate-storage.md)]


## <a name="upload-a-file-from-a-device-app"></a>Przekaż plik z aplikacji urządzenia

W tej sekcji opisano tworzenie aplikacji urządzenia, aby przekazać plik do usługi IoT hub.

1. W wierszu polecenia, uruchom następujące polecenie, aby zainstalować **azure-iothub-device-client** pakietu:

    ```cmd/sh
    pip install azure-iothub-device-client
    ```

1. Za pomocą edytora tekstów Utwórz **FileUpload.py** pliku w folderze roboczym.

1. Dodaj następujący kod `import` instrukcji i zmienne na początku **FileUpload.py** pliku. Zastąp `deviceConnectionString` przy użyciu parametrów połączenia urządzenia Centrum IoT:

    ```python
    import time
    import sys
    import iothub_client
    import os
    from iothub_client import IoTHubClient, IoTHubClientError, IoTHubTransportProvider, IoTHubClientResult, IoTHubError

    CONNECTION_STRING = "[Device Connection String]"
    PROTOCOL = IoTHubTransportProvider.HTTP

    PATHTOFILE = "[Full path to file]"
    FILENAME = "[File name on storage after upload]"
    ```

1. Utwórz wywołanie zwrotne dla **upload_blob** funkcji:

    ```python
    def blob_upload_conf_callback(result, user_context):
        if str(result) == 'OK':
            print ( "...file uploaded successfully." )
        else:
            print ( "...file upload callback returned: " + str(result) )
    ```

1. Dodaj następujący kod do połączenia klienta, a następnie przekaż plik. Również obejmować `main` procedury:

    ```python
    def iothub_file_upload_sample_run():
        try:
            print ( "IoT Hub file upload sample, press Ctrl-C to exit" )

            client = IoTHubClient(CONNECTION_STRING, PROTOCOL)

            f = open(PATHTOFILE, "r")
            content = f.read()

            client.upload_blob_async(FILENAME, content, len(content), blob_upload_conf_callback, 0)

            print ( "" )
            print ( "File upload initiated..." )

            while True:
                time.sleep(30)

        except IoTHubError as iothub_error:
            print ( "Unexpected error %s from IoTHub" % iothub_error )
            return
        except KeyboardInterrupt:
            print ( "IoTHubClient sample stopped" )
        except:
            print ( "generic error" )

    if __name__ == '__main__':
        print ( "Simulating a file upload using the Azure IoT Hub Device SDK for Python" )
        print ( "    Protocol %s" % PROTOCOL )
        print ( "    Connection string=%s" % CONNECTION_STRING )

        iothub_file_upload_sample_run()
    ```

1. Zapisz i Zamknij **UploadFile.py** pliku.

1. Skopiuj przykładowy plik tekstowy do folderu roboczego i zmień jego nazwę `sample.txt`.

    > [!NOTE]
    > IoT Hub Python SDK aktualnie obsługuje tylko przekazywania plików opartego na znakach, takich jak **.txt** plików.


## <a name="run-the-application"></a>Uruchamianie aplikacji

Teraz można przystąpić do uruchomienia aplikacji.

1. W wierszu polecenia w folderze roboczym uruchom następujące polecenie:

    ```cmd/sh
    python FileUpload.py
    ```

1. Poniższy zrzut ekranu przedstawia dane wyjściowe z **FileUpload** aplikacji:

    ![Dane wyjściowe z aplikacji symulowane urządzenia](./media/iot-hub-python-python-file-upload/1.png)

1. Aby wyświetlić przekazany plik w kontenerze magazynu, które zostały skonfigurowane, można użyć portalu:

    ![Przekazany plik](./media/iot-hub-python-python-file-upload/2.png)


## <a name="next-steps"></a>Kolejne kroki

W tym samouczku przedstawiono sposób użycia funkcji przekazywania plików usługi IoT Hub można uproszczenie przekazywania plików z urządzeń. Możesz kontynuować poznawanie funkcji Centrum IoT i scenariusze z następujących artykułów:

* [Programistyczne tworzenie Centrum IoT hub][lnk-create-hub]
* [Wprowadzenie do zestawu SDK języka C][lnk-c-sdk]
* [Zestawy SDK Azure IoT][lnk-sdks]

<!-- Links -->
[Centrum deweloperów Azure IoT]: http://azure.microsoft.com/develop/iot

[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-python-download]: https://www.python.org/downloads/
[lnk-visual-c-redist]: http://www.microsoft.com/download/confirmation.aspx?id=48145
[lnk-install-pip]: https://pip.pypa.io/en/stable/installing/
