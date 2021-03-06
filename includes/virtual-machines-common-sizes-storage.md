---
title: Plik dyrektywy include
description: Plik dyrektywy include
services: virtual-machines
author: jonbeck7
ms.service: virtual-machines
ms.topic: include
ms.date: 07/06/2018
ms.author: azcspmt;jonbeck;cynthn
ms.custom: include file
ms.openlocfilehash: b4de9efbe85d5ab497bccd1742df23ddc1b3af43
ms.sourcegitcommit: a1cf88246e230c1888b197fdb4514aec6f1a8de2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/16/2019
ms.locfileid: "54354663"
---
Magazyn zoptymalizowanych rozmiarów maszyn wirtualnych zapewniają Wysoka przepływność dysku i we/wy oraz idealnie nadają się do obsługi dużych ilości danych, SQL, NoSQL baz danych, magazynowanie danych i dużych transakcyjnych baz danych.  Przykłady obejmują bazy danych Cassandra, MongoDB, Cloudera i Redis. Ten artykuł zawiera informacje o liczbie procesorów wirtualnych, dysków z danymi i kart sieciowych, a także przepustowość przepływności i sieć magazynu lokalnego dla każdego rozmiaru zoptymalizowane.

Lsv2 serii funkcje wysokiej przepływności, małego opóźnienia, jest bezpośrednio zamapowany Magazyn lokalny NVMe systemem [AMD EPYC &trade; 7551 procesora](https://www.amd.com/en/products/epyc-7000-series) ze wszystkich rdzeni zwiększanie wyniku 2.55 GHz, a maksymalna boost GHz 3.0. Maszyny wirtualne z serii Lsv2 są dostępne w rozmiarach od 8 do 80 procesorów wirtualnych w konfiguracji jednoczesnej wielowątkowości.  Dostępnych jest 8 GiB pamięci na każdy procesor wirtualny i jedno urządzenie NVMe SSD M.2 o pojemności 1,92 TB na każde 8 procesorów wirtualnych, a w przypadku serii L80s v2 19,2 TB (10x1,92 TB).

Maszyny wirtualne serii Ls oferują do 32 procesorów wirtualnych vCPU — procesor [Intel® Xeon® z rodziny E5 v3](http://www.intel.com/content/www/us/en/processors/xeon/xeon-e5-solutions.html). Wydajność procesora CPU dla serii Ls jest taka sama jak w przypadku maszyn wirtualnych serii G/GS. Na procesor wirtualny vCPU przypada pamięć o pojemności 8 GiB.

> [!NOTE]
> Maszyny wirtualne z serii Lsv2 są zoptymalizowane pod kątem używania lokalnego dysku w węźle podłączony bezpośrednio do maszyny Wirtualnej, a nie korzystają z dysków danych trwałych.  Pozwala to na większą operacje We/Wy / przepływność dla obciążeń.  Lsv2 i serii Ls nie obsługują tworzenia lokalnej pamięci podręcznej w celu zwiększenia operacje We/Wy osiągalna dysków danych trwałych. Wysoka przepływność i operacje We/Wy dysku lokalnego sprawia, że Lsv2 i maszyny wirtualne z serii Ls idealnym rozwiązaniem dla magazynów NoSQL, takie jak bazy danych Apache Cassandra i bazy danych MongoDB, które replikowanie danych między wieloma maszynami wirtualnymi do osiągnięcia trwałości w przypadku awarii jednej maszyny Wirtualnej. 

## <a name="lsv2-series"></a>Seria Lsv2
ACU: 150-175

Magazyn w warstwie Premium: Obsługiwane

Buforowanie Premium Storage: Nieobsługiwane

| Rozmiar          | Procesor wirtualny | Pamięć (GiB) | Dysku tymczasowego<sup>1</sup> (GiB) | NVMe Disks | Przepływność dysków NVMe<sup>2</sup> (odczytu na SEKUNDĘ / MB/s) | Rozmiar pamięci podręcznej hosta<sup>3</sup> | Dyski z danymi maksymalna | Maksymalna liczba kart sieciowych / oczekiwana przepustowość sieci (MB/s) | 
|---------------|-----------|-------------|--------------------------|----------------|---------------------------------------------------|-------------------------------------------|------------------------------|------------------------------| 
| Standard_L8s_v2   |  8 |  64 |  80 |  1x1.92 TB  | 340,000 / 2,000 | ND | 16 | 2 / 3,200  | 
| Standard_L16s_v2  | 16 | 128 | 160 |  2x1.92 TB  | 680,000 / 4,500 | ND | 32 | 4 / 6,400  | 
| Standard_L32s_v2  | 32 | 256 | 320 |  4x1.92 TB  | 1.4 M / 9000    | ND | 32 | 8 / 12,800 | 
| Standard_L64s_v2  | 64 | 512 | 640 |  8x1.92 TB  | 2.7 M / 18,000   | ND | 32 | 8 / 25,600 |
| Standard_L80s_v2  | 80 | 640 | 800 | 10x1.92TB   | 3.4 M / 22 000   | ND | 32 | 8 / 32,000 |
 
<sup>1</sup> maszyny wirtualne z serii Lsv2 ma standardowy dysk na podstawie zasobów temp SCSI dla użycie pliku stronicowania/wymiany systemu operacyjnego (D: na Windows, /dev/sdb w systemie Linux). Ten dysk zapewnia 80 GiB pamięci, 4000 operacje We/Wy i 80 MB/s transferu kurs co 8 wirtualnych procesorów CPU (np. Standard_L80s_v2 zapewnia 800 GiB 40 000 operacji We/Wy i 800 MB/s). Gwarantuje to, że dyski NVMe, które mogą być w pełni przeznaczone do użycia w aplikacji.

<sup>2</sup> technologii bezpośredniego NVMe funkcji Hyper-V udostępnia bez ograniczania dostępu do dysków NVMe bezpiecznie mapowane na miejsce maszyny Wirtualnej gościa.  Osiągnięcie maksymalnej wydajności wymaga, przy użyciu najnowszej kompilacji WS2019 lub Ubuntu 18.04 lub 16.04 w portalu Azure Marketplace.  Wydajność zapisu zależy od rozmiaru operacji We/Wy, obciążenia dysku i wykorzystanie pojemności.

<sup>3</sup> maszyny wirtualne z serii Lsv2 nie są oferowane pamięci podręcznej hosta dla dysku z danymi, ponieważ nie korzysta obciążeń Lsv2.  Jednak Lsv2 maszyn wirtualnych może obsłużyć opcji dysku Efemeryczne system operacyjny maszyny Wirtualnej platformy Azure (maksymalnie 30 GiB). 



## <a name="ls-series"></a>Seria Ls
ACU: 180-240

Magazyn w warstwie Premium:  Obsługiwane

Buforowanie Premium Storage:  Nieobsługiwane
 
| Rozmiar          | Procesor wirtualny | Pamięć (GiB) | Magazynu tymczasowego (GiB) | Maks. liczba dysków danych | Maksymalna przepływność magazynu tymczasowego (na SEKUNDĘ / MB/s) | Maksymalna przepływność niebuforowanych dysków (na SEKUNDĘ / MB/s) | Maksymalna liczba kart sieciowych / oczekiwana przepustowość sieci (MB/s) | 
|----------------|-----------|-------------|--------------------------|----------------|-------------------------------------------------------------|-------------------------------------------|------------------------------| 
| Standardowa_L4s   | 4  | 32  | 678   | 16 | 20,000 / 200 | 5000 / 125  | 2 / 4,000  | 
| Standardowa_L8s   | 8  | 64  | 1,388 | 32 | 40,000 / 400 | 10 000 / 250 | 4 / 8,000  | 
| Standardowa_L16s  | 16 | 128 | 2,807 | 64 | 80,000 / 800 | 20 000 / 500 | 8 / 16,000 | 
| Standard_L32s <sup>1</sup> | 32   | 256  | 5,630 | 64   | 160,000 / 1,600   | 40 000 / 1000     | 8 / 20,000 | 
 

Maksymalna przepływność dysków możliwa przy użyciu maszyn wirtualnych serii Ls może być ograniczona przez liczbę, rozmiar i rozłożenie wszelkich dołączonych dysków. Aby uzyskać więcej informacji, zobacz [usługi Premium Storage: Magazyn o wysokiej wydajności dla obciążeń maszyn wirtualnych platformy Azure](../articles/virtual-machines/windows/premium-storage.md).

<sup>1</sup> wystąpienie jest izolowane do sprzętu dedykowanego pojedynczemu klientowi.

## <a name="size-table-definitions"></a>Definicje tabel rozmiaru

- Pojemność magazynu jest podawana w jednostkach GiB (1024^3 bajtów). Podczas porównywania dysków mierzonych w GB (1000^3 bajtów) z dyskami mierzonymi w GiB (1024^3 bajtów) należy pamiętać, że pojemność podawana w GiB może wydawać się mniejsza. Na przykład 1023 GiB = 1098,4 GB.
- Przepływność dysku mierzona jest jako liczba operacji wejścia/wyjścia na sekundę i MB/s, gdzie 1 MB/s = 10^6 bajtów/s.
- Jeśli chcesz uzyskać najlepszą wydajność dla maszyn wirtualnych, należy ograniczyć liczbę dysków z danymi na 2 dyski na procesor wirtualny vCPU.
- **Oczekiwano przepustowość sieci** maksymalną mają charakter [przydzielonej dla typu maszyny Wirtualnej przepustowości](../articles/virtual-network/virtual-machine-network-throughput.md) we wszystkich kartach sieciowych, dla wszystkich miejsc docelowych. Górne limity nie są gwarantowane, ale mają stanowić wskazówkę do wybierania właściwego typu maszyny wirtualnej dla planowanej aplikacji. Rzeczywista wydajność sieci będzie zależeć od wielu czynników, takich jak przeciążenie sieci, obciążenie aplikacji oraz ustawienia sieci. Aby uzyskać informacje na temat optymalizowania przepływności sieci, zobacz [Optimizing network throughput for Windows and Linux (Optymalizowanie przepływności sieci dla systemów Windows i Linux)](../articles/virtual-network/virtual-network-optimize-network-bandwidth.md). Aby uzyskać oczekiwaną wydajność sieci w systemie Linux lub Windows, konieczne może być wybranie konkretnej wersji maszyny wirtualnej lub jej zoptymalizowanie. Aby uzyskać więcej informacji, zobacz [How to reliably test for virtual machine throughput (Jak wiarygodnie przetestować przepływność maszyny wirtualnej)](../articles/virtual-network/virtual-network-bandwidth-testing.md).
