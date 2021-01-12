---
title: 1x1 ビューポイント サイズ バリアント | Microsoft Docs
description: 1x1 ビューポート サイズ バリアントを適用し、すべてのレンダー ターゲットのビューポート ディメンションを 1x1 ピクセルまで減らします。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 3dbc3247-00f5-4644-8ff9-72e9febcf09a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d1041f3a8016500a6e1f217849654d9710a508d8
ms.sourcegitcommit: fcfd0fc7702a47c81832ea97cf721cca5173e930
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/22/2020
ms.locfileid: "97726489"
---
# <a name="1x1-viewport-size-variant"></a>1x1 ビューポイント サイズ バリアント
すべてのレンダー ターゲットでビューポートのディメンションを 1x1 ピクセルに減らします。

## <a name="interpretation"></a>解釈
 ビューポートを小さくすると、網かけするピクセル数を減らすことができます。 しかし、ビューポートが小さくなっても、処理する頂点の数が減ることはありません。 ビューポートのディメンションを 1x1 ピクセルに設定すると、アプリケーションでピクセルのシェーディングを効果的に除去することができます。

 このバリアントによりパフォーマンスが大幅に向上する場合は、アプリで使用されているフィル レートが多すぎることを示しています。 さらに、解像度がターゲット プラットフォームに対して高すぎる、またはアプリで、後に上書き ("*範囲を超えて描画*") されるピクセルのシェーディングに多くの時間を消費している場合もあります。 フレーム バッファーを小さくするか、範囲を超えて描画される量を減らすと、アプリのパフォーマンスが向上します。

## <a name="remarks"></a>Remarks
 `ID3D11DeviceContext::OMSetRenderTargets` または `ID3D11DeviceContext::RSSetViewports` への呼び出しが行われるたびに、ビューポートのディメンションは 1x1 ピクセルにリセットされます。

## <a name="example"></a>例
 このバリアントは次のコードを使用して再現することができます。

```cpp
D3D11_VIEWPORT viewport;
viewport.TopLeftX = 0;
viewport.TopLeftY = 0;
viewport.Width = 1;
viewport.Height = 1;
d3d_context->RSSetViewports(1, &viewport);
```
