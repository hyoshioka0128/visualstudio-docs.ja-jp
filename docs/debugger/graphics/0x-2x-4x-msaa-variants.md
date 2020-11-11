---
title: 0x-2x-4x MSAA バリアント | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 668a6603-5082-4c78-98e6-f3dc871aa55b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e77c0d7b5cbba2faf73fcca85ffcd0db063d618e
ms.sourcegitcommit: 023f52f10fb91850824558478cbfd2ec965054f0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/10/2020
ms.locfileid: "94407550"
---
# <a name="0x2x4x-msaa-variants"></a>0x/2x/4x MSAA バリアント
すべてのレンダー ターゲットおよびスワップ チェーン上で multi-sample anti-aliasing (MSAA) の設定をオーバーライドします。

## <a name="interpretation"></a>解釈
 Multi-sample anti-aliasing は、各ピクセルにおいて複数の場所でサンプルを取得することによって表示品質を向上させます。MSAA のレベルを高くするとより多くのサンプルが必要になります。MSAA を使用しない場合は、ピクセルの中央から 1 つのサンプルのみを取得します。 アプリケーションで MSAA を有効にすると通常、レンダリング パフォーマンスで (高額ではありませんが) 多少のコストがかかります。ただし、一定の負荷または一定の GPU のもとではほとんど影響はありません。

 アプリケーションですでに MSAA を有効にしている場合、低いレベルの MSAA バリアントは、既存の高いレベルの MSAA で発生する相対的なパフォーマンス コストを示します。 具体的には、0x MSAA バリアントは MSAA を使用しない場合のアプリケーションの相対パフォーマンスを示しています。

 アプリケーションでまだ MSAA を有効にしていない場合、2x MSAA および 4x MSAA のバリアントは、アプリケーション内でこれらの MSAA を有効にするための相対パフォーマンス コストを示しています。 コストが比較的安価な場合は、MSAA を有効にしてアプリケーションのイメージ品質を向上させることを検討します。

> [!NOTE]
> ご利用のハードウェアでは、MSAA をすべての形式で完全にサポートしていないことがあります。 いずれかのバリアントで、対処できないハードウェアの制限に直面した場合は、パフォーマンスのサマリー テーブルの該当する列が空白になり、エラー メッセージが生成されます。

## <a name="remarks"></a>Remarks
 これらのバリアントは、レンダー ターゲットを作成する `ID3DDevice::CreateTexture2D` への呼び出しが行われるときに sample count および sample-quality 引数をオーバーライドします。 具体的には、以下の場合にこれらのパラメーターがオーバーライドされます。

- `D3D11_TEXTURE2D_DESC` で渡される`pDesc` オブジェクトがレンダー ターゲットを記述する場合。つまり

  - BindFlags メンバーは、D3D11_BIND_TARGET フラグまたは D3D11_BIND_DEPTH_STENCIL フラグのいずれかを設定します。

  - Usage メンバーは D3D11_USAGE_DEFAULT に設定されます。

  - CPUAccessFlags メンバーは 0 に設定されます。

  - MipLevels メンバーは 1 に設定されます。

- デバイスは、要求されたレンダー ターゲット形式 (D3D11_TEXTURE2D_DESC::Format member) に対して、要求された sample count (0、2、または 4) および sample quality (0) を、`ID3D11Device::CheckMultisampleQualityLevels` で定義されているとおりにサポートします。

  D3D11_TEXTURE2D_DESC::BindFlags メンバーが D3D_BIND_SHADER_RESOURCE または D3D11_BIND_UNORDERED_ACCESS フラグを設定した場合、2 つのバージョンのテクスチャが作成されます。最初のバージョンは、レンダー ターゲットとして使用するためにフラグがクリアされています。もう 1 つのバージョンは非 MSAA テクスチャであり、最初のバージョンのリゾルブ バッファーとして機能するよう、フラグがそのまま保持されています。 MSAA テクスチャをシェーダー リソースとして使用すること、または非順序アクセスに対して使用することは妥当ではない (たとえば、MSAA テクスチャで機能するシェーダーは、非 MSAA テクスチャを予期しているため間違った結果が生成される) と思われるため、このしくみは必要です。 バリアントがセカンダリ非 MSAA テクスチャを作成すると、MSAA レンダー ターゲットがデバイス コンテキストから設定解除されるたびに、コンテキストが非 MSAA テクスチャに解決されます。 同様に、MSAA レンダー ターゲットをシェーダー リソースとしてバインドしなければならない場合、または順序指定されていないアクセス ビューで使用する場合は、解決された非 MSAA テクスチャが代わりにバインドされます。

  また、これらのバリアントは `IDXGIFactory::CreateSwapChain`、`IDXGIFactory2::CreateSwapChainForHwnd`、`IDXGIFactory2::CreateSwapChainForCoreWindow`、`IDXGIFactory2::CreateSwapChainForComposition`、および `ID3D11CreateDeviceAndSwapChain` を使用して作成したすべてのスワップ チェーン上の MSAA 設定をオーバーライドします。

  これらの変更の実際の影響として、すべてのレンダリングが 1 つの MSAA レンダー ターゲットに対して行われます。ただし、アプリケーションでこれらのレンダー ターゲットの 1 つ、またはスワップ チェーン バッファーをシェーダー リソース ビュー、または非順序アクセス ビューとして使用している場合、レンダー ターゲットの解決された非 MSAA コピーからデータ サンプルを取得します。

## <a name="restrictions-and-limitations"></a>制約と制限
 Direct3D11 では、MSAA テクスチャは非 MSAA テクスチャよりも制限が多くなります。 たとえば、MSAA テクスチャでは `ID3D11DeviceContext::UpdateSubresource` を呼び出しできません。また、ソース リソースと宛先リソースの sample count と sample quality が一致しない場合 (このバリアントが一方のリソースの MSAA 設定をオーバーライドしたのに、他方の設定をオーバーライドしていない場合に、このような状況が発生する可能性があります)、`ID3D11DeviceContext::CopySubresourceRegion` の呼び出しは失敗します。

 再生でこのような矛盾が見つかると、本来の正しい動作を複製するために出来る限りのことをしますが、結果を正確に適合させるのは不可能でしょう。 影響を正確に伝えていない方法で、これらのバリアントのパフォーマンスが影響を受けることは一般的ではありませんが、起こり得ることです (たとえば、あるピクセル シェーダーのフロー コントロールがテクスチャの正確なコンテンツによって決まる場合です)。複製されたテクスチャは同じコンテンツを持っていない可能性があるからです。

## <a name="example-1"></a>例 1
 これらのバリアントは、`ID3D11Device::CreateTexture2D` を使用して作成されたレンダー ターゲットに対して、次のようなコードを使用して再生することができます。

```cpp
D3D11_TEXTURE2D_DESC target_description;
target_description.BindFlags = D3D11_BIND_RENDER_TARGET;
target_description.SampleDesc.Count = 4; // 4x MSAA, can be 2 or 0 instead
target_description.SampleDesc.Quality = 0;
d3d_device->CreateTexture2D(&target_description, nullptr, &render_target);
```

## <a name="example-2"></a>例 2
 または、IDXGISwapChain::CreateSwapChain または D3D11CreateDeviceAndSwapChain を使用して作成されたスワップ チェーンに対して、次のようなコードを使用して再生することができます。

```cpp
DXGI_SWAP_CHAIN_DESC chain_description;
chain_description.SampleDesc.Count = 4; // 4x MSAA, can be 2 or 0 instead
chain_description.SampleDesc.Quality = 0;

// Call IDXGISwapChain::CreateSwapChain or D3D11CreateDeviceAndSwapChain, etc.
```
