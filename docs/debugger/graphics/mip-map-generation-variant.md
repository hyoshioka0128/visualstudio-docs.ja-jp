---
title: ミップマップ生成バリアント | Microsoft Docs
description: ミップマップ生成でパフォーマンスが大幅に向上する場合、それはミップマップを有効にしないでテクスチャを使用しており、テクスチャのキャッシュを最大限に利用できていないことを示しています。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 3b4b3583-0b01-4f5d-aacb-3f96d19111d9
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: dc2e377c0313fffda88bf14c0c7304ff084f3275
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99904436"
---
# <a name="mip-map-generation-variant"></a>ミップマップ生成バリアント
レンダー ターゲットではないテクスチャで MIP マップを有効にします。

## <a name="interpretation"></a>解釈
MIP マップは主に、テクスチャの小さいバージョンを事前に計算することにより、縮小時にテクスチャでエイリアシング効果を除去する目的で使用されます。 これらの追加のテクスチャは (オリジナルのテクスチャよりも 33% 増の) GPU メモリを消費しますが、効率も良くなります。これは、より多くの表面が GPU テクスチャ キャッシュに適合し、そのコンテンツで高い使用率を実現するためです。

3-D シーンでは、追加のテクスチャを格納するメモリが使用できる場合は、レンダリング パフォーマンスとイメージの品質の両方が向上するため、MIP マップを推奨します。

このバリアントでパフォーマンスが大幅に向上する場合は、MIP マップを有効にしないでテクスチャを使用いるため、テクスチャのキャッシュを最大限に利用できていないことを示しています。

## <a name="remarks"></a>Remarks
MIP マップの生成は、ソース テクスチャを作成する `ID3D11Device::CreateTexture2D` への呼び出しがあるたびに強制的に行われます。 具体的には、`pDesc` に渡された D3D11_TEXTURE2D_DESC オブジェクトで、不変のシェーダー リソースが記述される場合に、MIP マップの生成が強制的に実行されます。

- BindFlags メンバーは D3D11_BIND_SHADER_RESOURCE フラグを設定するだけです。

- Usage メンバーは、D3D11_USAGE_DEFAULT または D3D11_USAGE_IMMUTABLE に設定されます。

- CPUAccessFlags メンバーは 0 に設定されます(CPU アクセスなし)。

- SampleDesc メンバーは自身の Count メンバーを 1 に設定します (Multi-Sample Anti-Aliasing (MSAA) なし)。

- MipLevels メンバーは 1 に設定されます (既存の MIP マップなし)。

  アプリケーションによって初期データが提供されたときに、テクスチャ形式は、D3D11_FORMAT_SUPPORT_MIP_AUTOGEN で定義されているように自動の MIP マップ生成をサポートしている必要があります (ただし、形式が BC1、BC2、または BC3 の場合は除きます)。サポートしていない場合はテクスチャは修正できず、初期データが提供されたときに MIP マップは生成されません。

  テクスチャに対して MIP マップが自動的に生成された場合は、再生中に `ID3D11Device::CreateShaderResourceView` に対する呼び出しが修正され、テクスチャのサンプリング中に MIP チェーンを使用できるようになります。

## <a name="example"></a>例
**Mip-map Generation** バリアントは、次のようなコードを使用して再現することができます。

```cpp
D3D11_TEXTURE2D_DESC texture_description;

// ...

texture_description.MipLevels = 0; // generate a full mipchain

std::vector<D3D11_SUBRESOURCE_DATA> initial_data(num_mips);

for (auto&& mip_level : initial_data)
{
    // fill mip_level with the application-supplied initial data
}

d3d_device->CreateTexture2D(&texture_description, initial_data.data(), &texture)
```

完全な MIP チェーンを持つテクスチャを作成するには、`D3D11_TEXTURE2D_DESC::MipLevels` を 0 に設定します。 完全な MIP チェーンの MIP レベルの数は floor(log2(n) + 1) となります。この n はテクスチャの最大のディメンションです。

`CreateTexture2D` に初期データを提供する場合は、各 MIP レベルに D3D11_SUBRESOURCE_DATA オブジェクトを提供しなければならないことに注意してください。

> [!NOTE]
> MIP レベルを自動的に生成する代わりに独自の MIP レベル コンテンツを提供する場合は、MIP マップ テクスチャをサポートしているイメージ エディターを使用してテクスチャを作成し、ファイルをロードして、MIP レベルを `CreateTexture2D` へ渡す必要があります。

## <a name="see-also"></a>関連項目
[ハーフ/クォーター テクスチャ ディメンション バリアント](half-quarter-texture-dimensions-variant.md)
