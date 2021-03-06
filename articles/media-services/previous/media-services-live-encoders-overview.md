---
title: Konfigurowanie koderów lokalnych podczas korzystania z usługi Azure Media Services do tworzenia strumieni o różnej szybkości transmisji bitów | Dokumentacja firmy Microsoft
description: Ten temat zawiera listę lokalnych koderów na żywo, które służą do przechwytywania zdarzeń na żywo i wysyłania strumienia na żywo o pojedynczej szybkości transmisji bitów w kanałach usługi AMS, (które są włączone kodowania na żywo) do dalszego przetwarzania. Temat zawiera linki do samouczków, które pokazują, jak skonfigurować koderów uwzględnione na liście.
services: media-services
documentationcenter: ''
author: juliako
manager: cfowler
editor: ''
ms.assetid: 0ec6f046-0841-4673-9057-883bdbc30d5c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/21/2018
ms.author: juliako
ms.openlocfilehash: c0c7e2b8962cb757141b654c2956ed3ff5600c88
ms.sourcegitcommit: 295babdcfe86b7a3074fd5b65350c8c11a49f2f1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/27/2018
ms.locfileid: "53787651"
---
# <a name="how-to-configure-on-premises-encoders-when-using-azure-media-services-to-create-multi-bitrate-streams"></a>Konfigurowanie koderów lokalnych podczas korzystania z usługi Azure Media Services do tworzenia strumieni o różnej szybkości transmisji bitów
Ten temat zawiera listę lokalnych koderów na żywo, które służą do przechwytywania zdarzeń na żywo i wysyłania strumienia na żywo o pojedynczej szybkości transmisji bitów w kanałach usługi AMS, (które są włączone kodowania na żywo) do dalszego przetwarzania. Temat zawiera także linki do samouczków, które pokazują, jak skonfigurować koderów uwzględnione na liście.

> [!NOTE]
> Podczas przesyłania strumieniowego za pośrednictwem protokołu RTMP, sprawdź ustawienia zapory i/lub serwer proxy, aby upewnić się, że porty TCP ruchu wychodzącego 1935 i 1936 są otwarte.

## <a name="flash-media-live-encoder"></a>Flash Media Live Encoder
Aby uzyskać informacje na temat konfigurowania [Flash Media Live Encoder](http://www.adobe.com/products/flash-media-encoder.html) Zobacz encoder (FMLE) do wysyłania strumienia na żywo o pojedynczej szybkości transmisji bitów do kanału usługi AMS [Konfigurowanie FMLE](media-services-configure-fmle-live-encoder.md).

## <a name="haivision-kb-encoder"></a>Koder Haivision KB
Aby uzyskać informacje na temat konfigurowania [Haivision KB koder](https://www.haivision.com/products/kb-series/) Zobacz kodera do wysyłania strumienia na żywo o pojedynczej szybkości transmisji bitów do kanału usługi AMS [Konfigurowanie z koder Haivision KB](media-services-configure-kb-live-encoder.md).

## <a name="telestream-wirecast"></a>Telestream Wirecast
Aby uzyskać informacje na temat konfigurowania [Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm) Zobacz kodera do wysyłania strumienia na żywo o pojedynczej szybkości transmisji bitów do kanału usługi AMS [Konfigurowanie Wirecast](media-services-configure-wirecast-live-encoder.md).

## <a name="newtek-tricaster"></a>Koder NewTek TriCaster
Aby uzyskać informacje na temat konfigurowania [Tricaster](http://newtek.com/products/tricaster-40.html) Zobacz kodera do wysyłania strumienia na żywo o pojedynczej szybkości transmisji bitów do kanału usługi AMS [Konfigurowanie Tricaster](media-services-configure-tricaster-live-encoder.md).

## <a name="elemental-live"></a>Elemental Live
Aby uzyskać więcej informacji, zobacz [Elemental Live](http://www.elementaltechnologies.com/products/elemental-live).

## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>Kolejne kroki

[Transmisja strumieniowa przy użyciu usługi Azure Media Services do tworzenia strumieni o różnej szybkości transmisji na żywo](media-services-manage-live-encoder-enabled-channels.md).

