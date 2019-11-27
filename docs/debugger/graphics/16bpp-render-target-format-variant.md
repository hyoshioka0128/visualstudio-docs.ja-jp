---
title: 16bpp レンダーターゲット形式 Variant |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 24b22ad9-5ad0-4161-809a-9b518eb924bf
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8a63261a4ef8a6304bec8c2bdde1d9ec9113405e
ms.sourcegitcommit: 8530d15aa72fe058ee3a3b4714c36b8638f8b494
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/19/2019
ms.locfileid: "74188588"
---
# <a name="16-bpp-render-target-format-variant"></a>16 bpp レンダーターゲットフォーマットバリアント
すべてのレンダー ターゲットおよびバック バッファーに対して、ピクセル形式を DXGI_FORMAT_B5G6R5_UNORM に設定します。

## <a name="interpretation"></a>意味
 レンダーターゲットまたはバックバッファーは、通常、B8G8R8A8_UNORM などの 32 bpp (32 ビット/ピクセル) 形式を使用します。 32-bpp 形式では、大量のメモリ帯域幅を消費する可能性があります。 B5G6R5_UNORM 形式は、32ビット形式のサイズの半分である 16 bpp 形式であるため、これを使用するとメモリ帯域幅の負荷が軽減されますが、色の忠実性は低下します。

 このバリアントによりパフォーマンスが大幅に向上する場合は、おそらくアプリケーションで使用しているメモリ帯域幅が多すぎることを示しています。 特に、プロファイルされたフレームに大量のオーバードローやアルファブレンドがあった場合は、パフォーマンスを大幅に向上させることができます。

16 bpp のレンダーターゲット形式では、アプリケーションに次のような状況がある場合に使用されるメモリ帯域を減らすことができます。
- 忠実度の高い色の再現は必要ありません。
- アルファチャネルは必要ありません。
- では、滑らかなグラデーションが使用されることはよくありません (色の忠実性が低下した場合、バンドアイテムの影響を受けやすい)。

メモリ帯域幅を減らすには、次のような方法があります。
- オーバードローまたはアルファブレンドの量を減らします。
- フレームバッファーの大きさを小さくします。
- テクスチャリソースの大きさを減らします。
- テクスチャリソースの圧縮を減らします。

これらの方法のいずれかを最適化することとイメージの品質を保持することは背反するため、通常と同じように両者のバランスを考慮する必要があります。

スワップチェーンの一部であるアプリケーションには、16 bpp をサポートしていないバックバッファー形式 (DXGI_FORMAT_B5G6R5_UNORM) があります。 これらのスワップチェーンは、`D3D11CreateDeviceAndSwapChain` または `IDXGIFactory::CreateSwapChain`を使用して作成されます。 この制限を回避するには、次の手順を実行します。
1. `CreateTexture2D` を使用し、そのターゲットにレンダリングして、B5G6R5_UNORM 形式のレンダーターゲットを作成します。
2. レンダーターゲットをソーステクスチャとして使用して、全画面表示のクワッドを描画して、レンダーターゲットをスワップチェーン backbuffer にコピーします。
3. スワップチェーンでを呼び出します。

   この戦略では、レンダーターゲットをスワップチェーン backbuffer にコピーすることによって消費される帯域幅を節約するため、レンダリングのパフォーマンスが向上します。

   タイル表示技法を使用する GPU アーキテクチャでは、16 bpp フレームバッファー形式を使用することによって、パフォーマンス上の大きな利点が得られます。 この機能強化は、フレームバッファーの大きな部分が各タイルのローカルフレームバッファーキャッシュに収めることができるためです。 タイル型のレンダリング アーキテクチャは、携帯電話機やタブレット コンピューターの GPU で使用されています。これらの市場以外で使用されることはほとんどありません。

## <a name="remarks"></a>コメント
 レンダー ターゲット形式は、レンダー ターゲットを作成する `ID3D11Device::CreateTexture2D` への呼び出しのたびに、DXGI_FORMAT_B5G6R5_UNORM にリセットされます。 具体的には、pDesc で渡される D3D11_TEXTURE2D_DESC オブジェクトがレンダー ターゲットを記述するときに、この形式はオーバーライドされます。つまり、

- BindFlags メンバーは、D3D11_BIND_REDNER_TARGET フラグを設定します。

- BindFlags メンバーは D3D11_BIND_DEPTH_STENCIL フラグを解除します。

- Usage メンバーは D3D11_USAGE_DEFAULT に設定されます。

## <a name="restrictions-and-limitations"></a>制約と制限
 B5G6R5 形式ではアルファ チャネルを持たないため、アルファ コンテンツはこのバリアントでは保存されません。 アプリケーションのレンダリングで、レンダー ターゲットのアルファ チャネルが必要な場合、B5G6R5 形式に切り替えることはできません。

## <a name="example"></a>例
 **16 Bpp レンダーターゲットフォーマット**バリアントは、次のようなコードを使用して `CreateTexture2D` を使用して作成されたレンダーターゲットに対して再現できます。

```cpp
D3D11_TEXTURE2D_DESC target_description;

target_description.BindFlags = D3D11_BIND_RENDER_TARGET;
target_description.Format = DXGI_FORMAT_B5G6R5_UNORM;
d3d_device->CreateTexture2D(&target_description, nullptr, &render_target);
```
