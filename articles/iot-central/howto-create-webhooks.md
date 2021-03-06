---
title: Tworzenie elementów webhook w regułach w usłudze Azure IoT Central | Dokumentacja firmy Microsoft
description: Tworzenie elementów webhook w usłudze Azure IoT Central automatycznie powiadamiać innych aplikacji, gdy wyzwolenie reguły.
author: viv-liu
ms.author: viviali
ms.date: 09/17/2018
ms.topic: conceptual
ms.service: iot-central
services: iot-central
manager: peterpr
ms.openlocfilehash: 896d4e9c775fa0b0c8eb062d11d141901daa7242
ms.sourcegitcommit: cf606b01726df2c9c1789d851de326c873f4209a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/19/2018
ms.locfileid: "46295989"
---
# <a name="create-webhook-actions-on-rules-in-azure-iot-central"></a>Utwórz akcje elementu webhook na reguły w usłudze Azure IoT Central

*Ten temat dotyczy konstruktorów i administratorów.*

Elementy Webhook pozwalają połączyć aplikację IoT Central do innych aplikacji i usług, zdalne monitorowanie i powiadomienia. Elementy Webhook powiadamiają automatycznie, inne aplikacje i usługi, z którymi się łączysz zawsze wtedy, gdy reguła jest wyzwalana w swojej aplikacji IoT Central. Aplikacja IoT Central wyśle żądanie POST do punktu końcowego HTTP innej aplikacji przy każdym wyzwoleniu reguły. Ładunek będzie zawierać szczegóły dotyczące urządzenia i wyzwalacza reguły. 

## <a name="how-to-set-up-the-webhook"></a>Jak skonfigurować element webhook
W tym przykładzie połączysz się RequestBin powiadomieniom reguły wyzwalać przy użyciu elementów webhook. 

1. Otwórz [RequestBin](http://requestbin.net/). 
1. Utwórz nowe narzędzia RequestBin i kopiowania **URL pojemnika**. 
1. Tworzenie [reguły telemetrii](howto-create-telemetry-rules.md) lub [reguły zdarzenia](howto-create-event-rules.md). Zapisać regułę, a następnie dodaj nową akcję.
![Ekran tworzenia elementu Webhook](media/howto-create-webhooks/webhookcreate.PNG)
1. Wybierz akcję elementu webhook i podać nazwę wyświetlaną i wklej adres URL pojemnika, jako adres URL wywołania zwrotnego. 
1. Zapisać reguły.

Teraz po wyzwoleniu reguły powinien być widoczny nowe wezwanie są wyświetlane w RequestBin.

## <a name="payload"></a>Ładunek
Po wyzwoleniu reguły żądanie HTTP POST wykonywane, aby adres URL wywołania zwrotnego zawierającego ładunek json z pomiarów, urządzenia, reguły i szczegóły dotyczące aplikacji. Reguły telemetrii obciążenie może wyglądać następująco:

```json
{
    "id": "ID",
    "timestamp": "date-time",
    "device" : {
        "id":"ID",
        "name":  "Refrigerator1",
        "simulated" : true,
        "deviceId": "deviceID",
        "deviceTemplate":{
            "id": "ID",
            "version":"1.0.0"
        },
        "properties":{
            "device":{
                "firmwareversion":"1.0"
            },
            "cloud":{
                "location":"One Microsoft Way"
            }
        },
        "measurements":{
            "telemetry":{
                "temperature":20,
                "pressure":10
            }
        }

    },
    "rule": {
        "id": "ID",
        "name": "High temperature alert",
        "enabled": true,
        "deviceTemplate": {
            "id":"GUID",
            "version":"1.0.0"
        }
    },
    "application": {
        "id": "ID",
        "name": "Contoso app",
        "subdomain":"contoso-app"
    }
}
```

## <a name="known-limitations"></a>Znane ograniczenia
Obecnie nie ma sposobu anulowania subskrypcji/subskrypcji z tych elementów webhook przy użyciu interfejsu API.

Jeśli masz pomysły dotyczące poprawy tę funkcję, opublikuj swoje sugestie naszych [Uservoice forum](https://feedback.azure.com/forums/911455-azure-iot-central).

## <a name="next-steps"></a>Kolejne kroki
Teraz, gdy wiesz jak konfigurowanie i używanie elementów webhook sugerowane następnym krokiem jest Eksplorowanie [tworzenia przepływów pracy w programie Microsoft Flow](howto-add-microsoft-flow.md).
