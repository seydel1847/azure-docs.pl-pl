---
title: Dodaj warstwę Symbol do usługi Azure Maps | Dokumentacja firmy Microsoft
description: Jak dodać symboli do mapy Javascript
author: rbrundritt
ms.author: richbrun
ms.date: 12/2/2018
ms.topic: conceptual
ms.service: azure-maps
services: azure-maps
manager: ''
ms.custom: codepen
ms.openlocfilehash: 718a679418790a6bf1207a96e5c204f7962de239
ms.sourcegitcommit: 82cdc26615829df3c57ee230d99eecfa1c4ba459
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/19/2019
ms.locfileid: "54411258"
---
# <a name="add-a-symbol-layer-to-a-map"></a>Dodaj warstwę symbol do mapy

W tym artykule dowiesz się, jak można renderować punktu danych ze źródła danych jako warstwa symboli na mapie. Symbol warstwy są renderowane przy użyciu WebGL i obsługuje znacznie większa liczba punktów danych niż znaczników HTML, ale nie obsługują tradycyjnych elementy CSS i HTML do określania stylu.  

> [!TIP]
> Symbol warstwy domyślnie będą renderowane współrzędne wszystkich geometrii w źródle danych. Aby ograniczyć warstwy w taki sposób, że tylko renderuje geometrii punktu funkcje zestawu `filter` właściwości warstwy `['==', '$type', 'Point']`

## <a name="add-a-symbol-layer"></a>Dodawanie warstwy symboli

<iframe height='500' scrolling='no' title='Przełącznik Przypnij lokalizację' src='//codepen.io/azuremaps/embed/ZqJjRP/?height=500&theme-id=0&default-tab=js,result&embed-version=2&editable=true' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>Zobacz pióra <a href='https://codepen.io/azuremaps/pen/ZqJjRP/'>przełącznika Przypnij lokalizację</a> przez usługi Azure Maps (<a href='https://codepen.io/azuremaps'>@azuremaps</a>) na <a href='https://codepen.io'>funkcji codepen można</a>.
</iframe>

Pierwszy blok powyższy kod tworzy obiekt mapy. Możesz zobaczyć [Utwórz mapę](./map-create.md) instrukcje.

W drugim bloku kodu obiektu źródła danych jest tworzony przy użyciu [DataSource](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.source.datasource?view=azure-iot-typescript-latest) klasy. [Funkcja] nadrzędnym [punktu](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.data.point?view=azure-iot-typescript-latest) geometrii jest otoczony przez [kształt](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.shape?view=azure-iot-typescript-latest) klasy, aby ułatwić zaktualizować, a następnie utworzony i dodany do źródła danych.

Trzeci bloku kodu tworzy [odbiornik zdarzeń](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest#events) i aktualizacje współrzędne punktu od myszy, kliknij przycisk za pomocą klasy kształt [setCoordinates](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.shape?view=azure-iot-typescript-latest) metody.

A [warstwy symbol](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.layer.symbollayer?view=azure-iot-typescript-latest) używa tekstu lub ikony do renderowania oparta na punkcie danych, w [DataSource](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.source.datasource?view=azure-iot-typescript-latest) jako symbole na mapie.  Źródła danych, kliknij odbiornik zdarzeń i warstwy symboli są tworzone i dodawane do mapy w ramach [odbiornik zdarzeń](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest#events) funkcję, aby upewnić się, że punkt jest wyświetlany po mapy ładuje pełni.

## <a name="add-a-custom-icon-to-a-symbol-layer"></a>Dodać niestandardową ikonę do warstwy symboli

Symbol warstwy są renderowane przy użyciu WebGL. Jako takie wszystkie zasoby, takie jak obrazy ikon musi być ładowane do kontekstu WebGL. Ten przykład pokazuje, jak dodać ikonę custom — symbol do Mapowanie zasobów, a następnie użyć go do renderowania punktu danych przy użyciu niestandardowego symbolu na mapie. `textField` Właściwości warstwy symbol wymaga wyrażenia należy określić. W tym przypadku chcemy renderowania właściwość temperatury funkcji punktów jako wartości tekstowej. Można to osiągnąć przy użyciu tego wyrażenia: `['get', 'temperature']`. 

<br/>

<iframe height='500' scrolling='no' title='Ikona obrazu Custom — Symbol' src='//codepen.io/azuremaps/embed/WYWRWZ/?height=500&theme-id=0&default-tab=js,result&embed-version=2&editable=true' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>Zobacz pióra <a href='https://codepen.io/azuremaps/pen/WYWRWZ/'>ikona obrazu niestandardowego symbolu</a> przez usługi Azure Maps (<a href='https://codepen.io/azuremaps'>@azuremaps</a>) na <a href='https://codepen.io'>funkcji codepen można</a>.
</iframe>

## <a name="customize-a-symbol-layer"></a>Dostosowywanie warstwy symboli 

Warstwa symbol ma wiele opcji stylów. W tym miejscu to narzędzie do przetestowania są różne opcje stylu.

<br/>

<iframe height='700' scrolling='no' title='Opcje warstwy symboli' src='//codepen.io/azuremaps/embed/PxVXje/?height=700&theme-id=0&default-tab=result' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>Zobacz pióra <a href='https://codepen.io/azuremaps/pen/PxVXje/'>symboli opcje warstwy</a> przez usługi Azure Maps (<a href='https://codepen.io/azuremaps'>@azuremaps</a>) na <a href='https://codepen.io'>funkcji codepen można</a>.
</iframe>

## <a name="next-steps"></a>Kolejne kroki

Dowiedz się więcej na temat klasy i metody używane w tym artykule:

> [!div class="nextstepaction"]
> [SymbolLayer](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.layer.symbollayer?view=azure-iot-typescript-latest)

> [!div class="nextstepaction"]
> [SymbolLayerOptions](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.symbollayeroptions?view=azure-iot-typescript-latest)

> [!div class="nextstepaction"]
> [IconOptions](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.iconoptions?view=azure-iot-typescript-latest)

> [!div class="nextstepaction"]
> [TexTOptions](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.textoptions?view=azure-iot-typescript-latest)

Zobacz następujące artykuły, aby uzyskać więcej przykładów kodu dodać do map:

> [!div class="nextstepaction"]
> [Dodawanie menu podręcznego](./map-add-popup.md)

> [!div class="nextstepaction"]
> [Dodawanie kształtu](./map-add-shape.md)

> [!div class="nextstepaction"]
> [Dodaj warstwę bąbelkowych](./map-add-bubble-layer.md)

> [!div class="nextstepaction"]
> [Dodaj osoby podejmujące decyzje HTML](./map-add-bubble-layer.md)
