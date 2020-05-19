---
title: ポイント、バイリニア、トリリニア、およびアニソトロピック テクスチャ フィルタリング バリアント
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 57d14fc9-b5f7-45ee-9717-48086886742d
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 314ec61da7ed61cc8bdd573e201d98a53862a32c
ms.sourcegitcommit: 117ece52507e86c957a5fd4f28d48a0057e1f581
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/28/2019
ms.locfileid: "66262930"
---
# <a name="point-bilinear-trilinear-and-anisotropic-texture-filtering-variants"></a>ポイント、バイリニア、トリリニア、およびアニソトロピック テクスチャ フィルタリング バリアント
適切なテクスチャのサンプラーでフィルタリング モードをオーバーライドします。

## <a name="interpretation"></a>解釈
 テクスチャ サンプリングにはさまざまなメソッドがありますが、それぞれパフォーマンス コストとイメージ品質が異なります。 次に、コストと表示品質の低い順からフィルター モードを示します。

1. Point フィルタリング (最も安価、表示品質は一番低い)

2. Bilinear フィルタリング

3. Trilinear フィルタリング

4. Anisotropic フィルタリング (最も高価、表示品質は一番高い)

   各バリアントのパフォーマンス コストが重要である、またはより強力なフィルタリング モードを使用してパフォーマンス コストを強化する場合は、表示品質に対してコストに重点をおくことができます。 自身の評価に基づいて、パフォーマンス コストを追加して表示品質を向上させる、表示品質を落としてフレームレートの数を多くする、他の方法で使用できるようにパフォーマンスを改善する、といったことが可能です。

   パフォーマンス コストがごくわずかであるか、またはフィルタリング モードに関係なく一定である (たとえば、ターゲットの GPU に大量のシェーダー スループットおよびメモリ帯域幅がある) 場合には、異方性フィルタリングを使用してアプリケーションで最高のイメージ品質を実現することを検討してください。

## <a name="remarks"></a>Remarks
 これらのバリアントは、アプリケーションが提供したサンプラーのフィルター モードが以下のいずれかの場合に、`ID3D11DeviceContext::PSSetSamplers` への呼び出しが行われたときにサンプラーの状態をオーバーライドします。

- `D3D11_FILTER_MIN_MAG_MIP_POINT`

- `D3D11_FILTER_MIN_MAG_POINT_MIP_LINEAR`

- `D3D11_FILTER_MIN_POINT_MAG_LINEAR_MIP_POINT`

- `D3D11_FILTER_MIN_POINT_MAG_MIP_LINEAR`

- `D3D11_FILTER_MIN_LINEAR_MAG_MIP_POINT`

- `D3D11_FILTER_MIN_LINEAR_MAG_POINT_MIP_LINEAR`

- `D3D11_FILTER_MIN_MAG_LINEAR_MIP_POINT`

- `D3D11_FILTER_MIN_MAG_MIP_LINEAR`

- `D3D11_FILTER_ANISOTROPIC`

  **Point Texture Filtering** バリアントでは、アプリケーションが提供したフィルター モードが `D3D11_FILTER_MIN_MAG_MIP_POINT` に置き換えられます。**Bilinear Texture Filtering** バリアントでは、`D3D11_FILTER_MIN_MAG_LINEAR_MIP_POINT` に置き換えられ、**Trilinear Texture Filtering** バリアントでは `D3D11_FILTER_MIN_MAG_MIP_LINEAR` に置き換えられます。

  **Anisotropic Texture Filtering** バリアントでは、アプリケーションが提供したフィルター モードは `D3D11_FILTER_ANISOTROPIC` に置き換えられ、Max Anisotropy は 16 に設定されます。

## <a name="restrictions-and-limitations"></a>制約と制限
 Direct3D では機能レベル 9.1 は、最大異方性が 2x であることを表します。 **Anisotropic Texture Filtering** バリアントは 16x の異方性のみを使おうとするため、機能レベル 9.1 のデバイス上でフレーム分析を実行すると再生は失敗します。 この制約の影響を受ける現在のデバイスには、ARM ベースの Surface RT、および Surface 2 Windows タブレットが含まれています。 コンピューターの中には古い GPU が存在している可能性があり、これらの GPU も影響を受けます。ただし、これらは一般的には使われておらず、問題にならなくなっています。

## <a name="example"></a>例
 **ポイント テクスチャ フィルタリング** バリアントは、次のようなコードを使用して再現することができます。

```cpp
D3D11_SAMPLER_DESC sampler_description;

// ... other sampler description setup ...

sampler_description.Filter = D3D11_FILTER_MIN_MAG_MIP_POINT;

d3d_device->CreateSamplerState(&sampler_desc, &sampler);
d3d_context->PSSetSamplers(0, 1, &sampler
```

## <a name="example"></a>例
 **バイリニア テクスチャ フィルタリング** バリアントは、次のようなコードを使用して再現することができます。

```cpp
D3D11_SAMPLER_DESC sampler_description;

// ... other sampler description setup ...

sampler_description.Filter = D3D11_FILTER_MIN_MAG_LINEAR_MIP_POINT;

d3d_device->CreateSamplerState(&sampler_desc, &sampler);
d3d_context->PSSetSamplers(0, 1, &sampler
```

## <a name="example"></a>例
 **トリリニア テクスチャ フィルタリング** バリアントは次のようなコードを使用して再現することができます。

```cpp
D3D11_SAMPLER_DESC sampler_description;

// ... other sampler description setup ...

sampler_description.Filter = D3D11_FILTER_MIN_MAG_MIP_LINEAR;

d3d_device->CreateSamplerState(&sampler_desc, &sampler);
d3d_context->PSSetSamplers(0, 1, &sampler
```

## <a name="example"></a>例
 **アニソトロピック テクスチャ フィルタリング** バリアントは、次のようなコードを使用して再現することができます。

```cpp
D3D11_SAMPLER_DESC sampler_description;

// ... other sampler description setup ...

sampler_description.Filter = D3D11_FILTER_ANISOTROPIC;
sampler_description.MaxAnisotropy = 16;

d3d_device->CreateSamplerState(&sampler_desc, &sampler);
d3d_context->PSSetSamplers(0, 1, &sampler
```
