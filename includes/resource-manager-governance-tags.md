---
title: Plik dyrektywy include
description: Plik dyrektywy include
services: azure-resource-manager
author: tfitzmac
ms.service: azure-resource-manager
ms.topic: include
ms.date: 11/20/2018
ms.author: tomfitz
ms.custom: include file
ms.openlocfilehash: f411504b0f4b7872e92a64c57fecbde863f532c6
ms.sourcegitcommit: fa758779501c8a11d98f8cacb15a3cc76e9d38ae
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/20/2018
ms.locfileid: "52271642"
---
Stosowanie tagów do Twoich zasobów platformy Azure, zapewniając metadanych umożliwia ich logiczne zorganizowanie w taksonomii. Każdy tag składa się z nazwy i pary wartości. Na przykład można zastosować nazwę „Środowisko” i wartość „Produkcyjne” do wszystkich zasobów w środowisku produkcyjnym.

Po zastosowaniu tagów można pobrać wszystkie zasoby w subskrypcji o nazwie i wartości konkretnego tagu. Tagi umożliwiają pobranie powiązanych zasobów z różnych grup zasobów. To pomocne rozwiązanie, gdy trzeba zorganizować zasoby w celach rozliczeniowych lub zarządzania.

Taksonomii należy wziąć pod uwagę samoobsługi metadane tagowania strategii oprócz strategii znakowanie automatycznie w celu zmniejszenia obciążenia użytkowników i zwiększyć dokładność.

Tagi mają następujące ograniczenia:

* Nie wszystkie typy zasobów obsługują tagów. Aby określić, jeśli tag można zastosować do typu zasobu, zobacz [obsługę dla zasobów platformy Azure tagów](../articles/azure-resource-manager/tag-support.md).
* Każdy zasób lub grupa zasobów może mieć co najwyżej 15 par nazwa/wartość tagu. To ograniczenie dotyczy tylko tagów stosowanych bezpośrednio do grupy zasobów lub zasobu. Grupa zasobów może zawierać wiele zasobów, z których każdy może mieć 15 par nazwa/wartość tagu. Jeśli masz więcej niż 15 wartości, które należy skojarzyć z zasobem, użyj ciągu JSON jako wartości tagu. Ciąg JSON może zawierać wiele wartości, które są stosowane do jednej nazwy tagu. W tym artykule przedstawiono przykład przypisywania ciągu JSON do tagu.
* Nazwa tagu może zawierać maksymalnie 512 znaków, a wartość tagu jest ograniczona do 256 znaków. W przypadku kont magazynu nazwa tagu jest ograniczona do 128 znaków, a wartość tagu jest ograniczona do 256 znaków.
* Maszyny wirtualne są może zawierać maksymalnie 2048 znaków, aby uzyskać wszystkie nazwy i wartości tagów.
* Tagi zastosowane do grupy zasobów nie są dziedziczone przez zasoby należące do tej grupy.
* Nie można zastosować znaczniki do klasycznych zasobów, takich jak usługi w chmurze.
* Nazwy tagów nie może zawierać następujących znaków: `<`, `>`, `%`, `&`, `\`, `?`, `/`
