---
title: Resetowanie TCP modułu równoważenia obciążenia na bezczynności (%) na platformie Azure
titlesuffix: Azure Load Balancer
description: Moduł równoważenia obciążenia za pomocą dwukierunkowych TCP RST pakietów na limit czasu bezczynności
services: load-balancer
documentationcenter: na
author: KumudD
ms.custom: seodec18
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/03/2018
ms.author: kumud
ms.openlocfilehash: 0b3e8fc72eb22a67c0672be19f60d4956d3377b7
ms.sourcegitcommit: 1c1f258c6f32d6280677f899c4bb90b73eac3f2e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/11/2018
ms.locfileid: "53257303"
---
# <a name="load-balancer-with-tcp-reset-on-idle-public-preview"></a>Moduł równoważenia obciążenia za pomocą funkcji resetowania TCP w stanie bezczynności (publiczna wersja zapoznawcza)

Możesz użyć [Balancer w warstwie standardowa](load-balancer-standard-overview.md) do tworzenia bardziej przewidywalne zachowanie aplikacji dla swoich scenariuszy za pomocą dwukierunkowych TCP resetuje (pakiet TCP RST) dla każdego można skonfigurować limit czasu bezczynności.  Zachowanie domyślne równoważenia obciążenia jest dyskretnie pomijać przepływów, po osiągnięciu limitu czasu bezczynności przepływu.

![Resetowanie TCP modułu równoważenia obciążenia](media/load-balancer-tcp-reset/load-balancer-tcp-reset.png)

>[!NOTE] 
>Równoważenia obciążenia za pomocą resetowania na temat funkcji limitu czasu bezczynności protokołu TCP jest dostępna jako publiczna wersja zapoznawcza, w tym momencie i jest dostępna w ograniczonym zestawem [regionów](#regions). Ta wersja zapoznawcza nie jest objęta umową dotyczącą poziomu usług i nie zalecamy korzystania z niej w przypadku obciążeń produkcyjnych. Niektóre funkcje mogą być nieobsługiwane lub ograniczone. Aby uzyskać szczegółowe informacje, zobacz [Dodatkowe warunki użytkowania wersji zapoznawczych platformy Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).
 
Możesz zmienić to domyślne zachowanie i Włącz wysyłania TCP resetuje na limit czasu bezczynności na reguły NAT dla ruchu przychodzącego, reguły równoważenia obciążenia i i [reguł dla ruchu wychodzącego](https://aka.ms/lboutboundrules).  Po włączeniu dla każdej reguły równoważenia obciążenia będzie wysyłać dwukierunkowe TCP Reset (pakiety TCP RST) do punktów końcowych klienta i serwera w momencie limitu czasu bezczynności dla wszystkich zgodnych przepływów.

Punkty końcowe odbierania pakietów TCP RST natychmiast zamknąć odpowiedniego gniazda. Dzięki temu natychmiastowego wysłania powiadomienia do punktów końcowych, które wystąpiło wersji połączenia i komunikację w ramach tego samego połączenia TCP zakończy się niepowodzeniem.  Aplikacje można trwale usunąć połączenia, gdy gniazdo zostanie zamknięty i ponownie ustanowić połączenia, zgodnie z potrzebami bez oczekiwania na połączenie TCP ostatecznie przekroczenie limitu czasu.

W wielu sytuacjach może być mniejszy keepalives konieczności wysyłania TCP (lub warstwa aplikacji), aby odświeżyć limitu czasu bezczynności przepływu. 

Jeśli bezczynności czasów trwania wykraczać poza dozwolone przez tą konfigurację lub aplikacja wyświetla niepożądane zachowanie TCP resetuje włączone, nadal może być konieczne użycie TCP keepalives (lub keepalives warstwa aplikacji) do monitorowania żywotności połączeń TCP.  Ponadto keepalives może pozostać również przydatne w przypadku gdy połączenie jest serwerem proxy gdzieś w ścieżce, szczególnie keepalives warstwy aplikacji.  

Należy dokładnie zbadać wykonywania całego scenariusza typu end to end zdecydować, czy korzyści z włączenia resetuje TCP, dostosowując limit czasu bezczynności, a jeśli dodatkowe kroki potrzebne do zapewnienia zachowania żądaną aplikację.

## <a name="enabling-tcp-reset-on-idle-timeout"></a>Trwa włączanie resetowania TCP na limit czasu bezczynności

Za pomocą interfejsu API w wersji 2018-07-01, można włączyć wysyłanie dwukierunkowych resetuje TCP na limit czasu bezczynności na podstawie poszczególnych reguł:

```json
      "loadBalancingRules": [
        {
          "enableTcpReset": true | false,
        }
      ]
```

```json
      "inboundNatRules": [
        {
          "enableTcpReset": true | false,
        }
      ]
```

```json
      "outboundRules": [
        {
          "enableTcpReset": true | false,
        }
      ]
```

## <a name="regions"></a> Dostępność regionalna

Ten parametr jest obecnie obowiązujące w następujących regionach.  W regionach niewymienione w tym miejscu parametru nie ma znaczenia.

| Region |
|---|
| Azja Południowo-Wschodnia |
| Brazylia Południowa |
| Kanada Środkowa |
| Europa Zachodnia |
| Indie Środkowe |
| Indie Zachodnie |
| Japonia Zachodnia |
| Korea Środkowa |
| Korea Południowa |
| Północne Zjednoczone Królestwo |
| Południowe Zjednoczone Królestwo 2 |
| Wschodnie stany USA |
| Wschodnie stany USA 2 |
| Północne stany USA |
| Zachodnie stany USA |

W tej tabeli zostaną zaktualizowane zgodnie z wersji zapoznawczej jest rozwinięty w innych regionach.  

## <a name="limitations"></a>Ograniczenia

- Ograniczone [dostępność w poszczególnych regionach](#regions).
- Portal nie można skonfigurować lub wyświetlić resetowania TCP.  Zamiast tego użyj szablonów, interfejs API REST, Az interfejsu wiersza polecenia w wersji 2.0 lub programu PowerShell.

## <a name="next-steps"></a>Kolejne kroki

- Dowiedz się więcej o [standardowego modułu równoważenia obciążenia](load-balancer-standard-overview.md).
- Dowiedz się więcej o [reguł dla ruchu wychodzącego](load-balancer-outbound-rules-overview.md).
