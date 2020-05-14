---
title: BC テクスチャ圧縮バリアント |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 2d0f5305-585b-4b01-bc9a-7a32d6e991da
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c5faf19632d746105deed3a36af6943627594175
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72736158"
---
# <a name="bc-texture-compression-variant"></a>BC テクスチャ圧縮バリアント
B8G8R8X8、B8G8R8A8、または R8G8B8A8 のバリエーションであるピクセル形式を持つテクスチャで、ブロック圧縮を有効にします。

## <a name="interpretation"></a>解釈
 BC1、BC2、BC3 などのブロックベースの圧縮形式は、圧縮されていないイメージ形式に比べて占有するメモリが著しく少ないため、メモリ帯域幅の使用がかなり少なくなります。 1 ピクセルあたり 32 ビットを使用する非圧縮形式と比べると、BC1 (以前の DXT1) は 8 倍の圧縮率、BC3 (以前の DXT5) は 4 倍の圧縮率を実現します。 BC1 と BC3 の違いは、BC1 はアルファ チャネルをサポートしていないのに対して、BC3 はブロック圧縮のアルファ チャネルをサポートしていることです。 高い圧縮率を実現していますが、一般的なテクスチャについてはイメージの品質低下はごくわずかです。 ただし、特定の種類のテクスチャ (小さい領域に多数のカラー バリエーションを持つテクスチャなど) のブロック圧縮では、許容できない結果になることがあります。

 対象のテクスチャがブロックベースの圧縮に適していて、完全な色の忠実性が必要ない場合は、ブロック圧縮形式を使用してメモリの使用量を減らし、帯域幅の使用を減らすことを検討します。

## <a name="remarks"></a>Remarks
 ソース テクスチャを作成する `ID3DDevice::CreateTexture2D` への呼び出しのたびに、ブロックベースの圧縮形式を使用してテクスチャを圧縮します。 具体的には、以下の場合にテクスチャが圧縮されます。

- `D3D11_TEXTURE2D_DESC` で渡される`pDesc` オブジェクトが、不変のシェーダー リソースを記述する場合、つまり

  - BindFlags メンバーは D3D11_BIND_SHADER_RESOURCE フラグを設定するだけです。

  - Usage メンバーは、D3D11_USAGE_DEFAULT または D3D11_USAGE_IMMUTABLE に設定されます。

  - CPUAccessFlags メンバーは 0 に設定されます(CPU アクセスなし)。

  - SamplerDesc メンバーは自身の Count メンバーを 1 に設定します (Multi-Sample Anti-Aliasing (MSAA) なし)。

- `CreateTexture2D` への呼び出しに対して初期データが提供される場合。

  サポートされているソース形式と、ブロック圧縮形式は以下のとおりです。

|元の形式 (from)|圧縮先の形式 (to)|
|------------------------------|------------------------------|
|`DXGI_FORMAT_B8G8R8X8_UNORM`|BC1 (以前の DXT1)|
|`DXGI_FORMAT_B8G8R8X8_UNORM_SRGB`|BC1|
|`DXGI_FORMAT_B8G8R8X8_TYPELESS`|BC1|
|`DXGI_FORMAT_B8G8R8A8_UNORM`|BC3 (以前の DXT5)|
|`DXGI_FORMAT_B8G8R8A8_UNORM_SRGB`|BC3|
|`DXGI_FORMAT_B8G8R8A8_TYPELESS`|BC3|
|`DXGI_FORMAT_R8G8B8A8_UNORM`|BC3|
|`DXGI_FORMAT_R8G8B8A8_UNORM_SRGB`|BC3|
|`DXGI_FORMAT_R8G8B8A8_TYPELESS`|BC3|

 使用しているテクスチャに、上記に記載されていない形式が含まれている場合、そのテクスチャは修正できません。

## <a name="restrictions-and-limitations"></a>制約と制限
 B8G8R8A8 または R8G8B8A8 イメージ形式のバリエーションで作成されたテクスチャは、実際にはアルファ チャネルを使用しないことがありますが、バリアントでアルファ チャネルが使用されているかどうかを知る方法はありません。 アルファ チャネルが使用されている場合に正確さを保持するために、バリアントは常にこれらの形式を、効率的には多少劣る BC3 形式にエンコードします。 バリアントでより効率のよい BC1 形式を使用できるようにアルファ チャネルを使用していない場合に、B8G8R8X8 のイメージ形式のバリエーションを使用すると、グラフィックス フレーム分析が、このバリアントでのアプリケーションの潜在的なレンダリング パフォーマンスを理解しやすいようにすることができます。

## <a name="example"></a>例
 このバリアントは、`CreateTexture2D` への呼び出しを行う前に、実行時にテクスチャをブロック圧縮します。 実行コードについては、このアプローチは推奨されません。圧縮されていないテクスチャはより多くのディスク容量を使用し、ブロックベースの圧縮では大量のコンピューティング リソースをエンコードする必要があり、追加のステップによってアプリケーションのロード時間が非常に長くなることがあるためです。 代わりに、イメージ エディタ、またはビルド パイプラインの一部であるイメージ プロセッサを使用して、テクスチャをオフラインで圧縮することを推奨しています。 これらのアプローチではディスク容量の要件が減り、アプリケーションのランタイム オーバーヘッドが排除され、処理時間に余裕があるため、最適なイメージ品質を保持することができます。

## <a name="see-also"></a>関連項目
- [ハーフ/クォーター テクスチャ ディメンション バリアント](half-quarter-texture-dimensions-variant.md)
