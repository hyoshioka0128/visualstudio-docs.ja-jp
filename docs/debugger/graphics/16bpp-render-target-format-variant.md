---
title: 16 bpp レンダリング ターゲット フォーマット バリアント | Microsoft Docs
description: すべてのレンダー ターゲットとバック バッファーを対象にピクセル形式を DXGI_FORMAT_B5G6R5_UNORM に設定することで、16 bpp (ピクセルあたりビット数) レンダー ターゲット フォーマット バリアントを適用します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 24b22ad9-5ad0-4161-809a-9b518eb924bf
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 6d0f43e2b004272b6882ff4a19e62fa99c998e53
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99874627"
---
# <a name="16-bpp-render-target-format-variant"></a>16 bpp レンダリング ターゲット フォーマット バリアント
すべてのレンダー ターゲットおよびバック バッファーに対して、ピクセル形式を DXGI_FORMAT_B5G6R5_UNORM に設定します。

## <a name="interpretation"></a>解釈
 レンダリング ターゲットまたはバック バッファーは通常、B8G8R8A8_UNORM などの 32 bpp (32 ビット (ピクセルあたり)) フォーマットを使用します。 32-bpp フォーマットは、大容量のメモリ帯域幅を消費します。 B5G6R5_UNORM フォーマットは 32-bpp フォーマットの半分の 16-bpp フォーマットであるため、これを使用してメモリ帯域幅における消費を緩和することができますが、色の忠実性は低下します。

 このバリアントによりパフォーマンスが大幅に向上する場合は、おそらくアプリケーションで使用しているメモリ帯域幅が多すぎることを示しています。 特に、プロファイルされたフレームに大量のオーバードローやアルファブレンドがあった場合は、パフォーマンスを大幅に向上させることができます。

16-bpp のレンダリング ターゲット フォーマットでは、アプリケーションに次のような状況がある場合に使用されるメモリ帯域を減らすことができます。
- 忠実度の高い色の再現が必要ない。
- アルファ チャネルが必要ない。
- 滑らかなグラデーション (色の忠実度が低い場合にバンディング アーティファクトが発生しやすい) があまり使用されない。

メモリ帯域幅を減らすその他の方法を次に示します。
- オーバードローまたはアルファ ブレンドの量を減らす。
- フレーム バッファーのディメンションを減らす。
- テクスチャ リソースのディメンションを減らす。
- テクスチャ リソースの圧縮を減らす。

これらの方法のいずれかを最適化することとイメージの品質を保持することは背反するため、通常と同じように両者のバランスを考慮する必要があります。

スワップ チェーンに含まれるアプリケーションには、16 bpp がサポートされないバック バッファー フォーマット (DXGI_FORMAT_B5G6R5_UNORM) があることがあります。 これらのスワップチェーンは、`D3D11CreateDeviceAndSwapChain` または `IDXGIFactory::CreateSwapChain` を使用して作成されます。 この制約を回避するには、次のステップを実行します。
1. `CreateTexture2D` を使用して B5G6R5_UNORM フォーマットのレンダリング ターゲットを作成し、そのターゲットにレンダリングします。
2. レンダリング ターゲットをソース テクスチャとしてフルスクリーン クアッドを描画して、スワップ チェーンのバック バッファー上にレンダリング ターゲットをコピーします。
3. スワップ チェーンで Present を呼び出します。

   この戦略で、レンダリング ターゲットのスワップ チェーン バックバッファーへのコピーで消費される帯域幅よりも節約できれば、レンダリングのパフォーマンスが向上します。

   タイル型レンダリング技法を使用する GPU アーキテクチャでは、16 bpp フレーム バッファー フォーマットを使用することによって、パフォーマンス上の大きな利点が得られます。 このように機能が強化されるのは、各タイルのローカル フレーム バッファー キャッシュに収めることができるフレーム バッファーの部分が大きくなるためです。 タイル型のレンダリング アーキテクチャは、携帯電話機やタブレット コンピューターの GPU で使用されています。これらの市場以外で使用されることはほとんどありません。

## <a name="remarks"></a>Remarks
 レンダー ターゲット形式は、レンダー ターゲットを作成する `ID3D11Device::CreateTexture2D` への呼び出しのたびに、DXGI_FORMAT_B5G6R5_UNORM にリセットされます。 具体的には、pDesc で渡される D3D11_TEXTURE2D_DESC オブジェクトがレンダー ターゲットを記述するときに、この形式はオーバーライドされます。つまり、

- BindFlags メンバーは、D3D11_BIND_REDNER_TARGET フラグを設定します。

- BindFlags メンバーは D3D11_BIND_DEPTH_STENCIL フラグを解除します。

- Usage メンバーは D3D11_USAGE_DEFAULT に設定されます。

## <a name="restrictions-and-limitations"></a>制約と制限
 B5G6R5 形式ではアルファ チャネルを持たないため、アルファ コンテンツはこのバリアントでは保存されません。 アプリケーションのレンダリングで、レンダー ターゲットのアルファ チャネルが必要な場合、B5G6R5 形式に切り替えることはできません。

## <a name="example"></a>例
 次のようなコードにより `CreateTexture2D` を使用して作成したレンダリング ターゲットに対して、**16 bpp レンダリング ターゲット フォーマット** バリアントを再現することができます。

```cpp
D3D11_TEXTURE2D_DESC target_description;

target_description.BindFlags = D3D11_BIND_RENDER_TARGET;
target_description.Format = DXGI_FORMAT_B5G6R5_UNORM;
d3d_device->CreateTexture2D(&target_description, nullptr, &render_target);
```
