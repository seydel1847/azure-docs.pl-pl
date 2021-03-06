---
title: Azure interfejsu wiersza polecenia usługi Service Fabric - sfctl ustawieniami telemetrii | Dokumentacja firmy Microsoft
description: W tym artykule opisano polecenia interfejsu wiersza polecenia usługi Service Fabric sfctl ustawienia danych telemetrycznych.
services: service-fabric
documentationcenter: na
author: Christina-Kang
manager: timlt
editor: ''
ms.assetid: ''
ms.service: service-fabric
ms.devlang: cli
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 12/06/2018
ms.author: bikang
ms.openlocfilehash: e0e229f0edb078fe9ce289d0089f34d7cbf9dbf8
ms.sourcegitcommit: 7fd404885ecab8ed0c942d81cb889f69ed69a146
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/12/2018
ms.locfileid: "53285396"
---
# <a name="sfctl-settings-telemetry"></a>Interfejs sfctl ustawień telemetrii
Skonfiguruj ustawienia danych telemetrycznych lokalnych, jak to wystąpienie interfejsu sfctl.

Interfejs Sfctl telemetrii zbiera nazwę polecenia bez parametrów podanych oraz ich wartości, wersja sfctl, typ systemu operacyjnego, wersji języka python, Powodzenie lub niepowodzenie polecenia, zwracany komunikat o błędzie.

## <a name="commands"></a>Polecenia

|Polecenie|Opis|
| --- | --- |
| dane telemetryczne zestawu | Włączanie lub wyłączanie telemetrii. |

## <a name="sfctl-settings-telemetry-set-telemetry"></a>Interfejs sfctl ustawienia danych telemetrycznych zestawu telemetrii
Włączanie lub wyłączanie telemetrii.

### <a name="arguments"></a>Argumenty

|Argument|Opis|
| --- | --- |
| — wyłączone | Wyłączyć obsługę telemetrii. |
| — na | Włącz telemetrię. Jest to wartość domyślna. |

### <a name="global-arguments"></a>Argumenty globalne

|Argument|Opis|
| --- | --- |
| --debugowania | Zwiększyć szczegółowość rejestrowania, aby pokazać, że debugowanie wszystkich dzienników. |
| — Pomoc -h | Pokaż ten komunikat pomocy i zakończenia. |
| --dane wyjściowe -o | Format danych wyjściowych.  Dozwolone wartości\: json, jsonc, tabela, tsv.  Domyślne\: json. |
| — zapytania | Ciąg zapytania JMESPath. Zobacz http\://jmespath.org/ uzyskać więcej informacji i przykładów. |
| — pełne | Zwiększ poziom szczegółowości rejestrowania. Użyj parametru--debugowania dzienniki pełnego debugowania. |

### <a name="examples"></a>Przykłady

Wyłączyć obsługę telemetrii.

```
sfctl settings telemetry set_telemetry --off
```

Włącz telemetrię.

```
sfctl settings telemetry set_telemetry --on
```


## <a name="next-steps"></a>Kolejne kroki
- [Konfigurowanie](service-fabric-cli.md) interfejsu wiersza polecenia usługi Service Fabric.
- Dowiedz się, jak używać przy użyciu interfejsu wiersza polecenia usługi Service Fabric [przykładowe skrypty](/azure/service-fabric/scripts/sfctl-upgrade-application).