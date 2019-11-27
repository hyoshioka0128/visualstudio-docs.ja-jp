---
title: ゲームまたはアプリでの 3-D アセットの使用 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.topic: conceptual
f1_keywords:
- VC.Project.ImageContentTask.ContentOutput
- VC.Project.MeshContentTask.ContentOutput
- VC.Project.ImageContentTask.GeneratePremultipliedAlpha
- VC.Project.ImageContentTask.Compress
- VC.Project.ShaderGraphContentTask.ContentOutput
- VC.Project.ImageContentTask.GenerateMips
ms.assetid: ea587909-e434-46a8-abf8-9b3e95a58b4f
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 6d838b7519b40d47b644a53befb91391fa30a664
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74293275"
---
# <a name="using-3-d-assets-in-your-game-or-app"></a>ゲームまたはアプリケーションでの 3-D アセットの使用
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ここでは、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] を使用して 3-D アセットを処理し、ビルドに含める方法について説明します。

 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] のツールを使用して 3-D アセットを作成したら、次の手順はアプリケーションでそれらを使用することです。 ただし、これらを使用する前に、DirectX が理解できる形式にアセットを変換する必要があります。 アセットを変換しやすいように、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] には、生成できるアセットの種類ごとにビルドのカスタマイズが用意されています。 アセットをビルドに含めるには、ビルドのカスタマイズを使用するようにプロジェクトを構成し、プロジェクトにアセットを追加し、正しいビルドのカスタマイズを使用するようにアセットを構成するだけです。 その後でアプリケーションにアセットを読み込み、他の DirectX アプリケーションと同様に DirectX リソースを作成して入力することにより、アセットを使用できます。

## <a name="configuring-your-project"></a>プロジェクトを構成する
 ビルドの一部として 3-D アセットを配置する前に、配置するアセットの種類について [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] が認識している必要があります。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] は、多くの一般的なファイルの種類を既に知っていますが、3d アセットを使用するのは特定の種類のアプリのみなので、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] プロジェクトでこれらの種類のファイルがビルドされるとは限りません。 アセットの種類ごとに用意されているビルドのカスタマイズを使用することによって、これらの種類のアセットをアプリケーションが使用することを [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] に指示できます。"*ビルドのカスタマイズ*" は、さまざまな種類のファイルを便利な方法で処理する方法を [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] に指示するファイルです。 これらのカスタマイズはプロジェクトごとに適用されるため、プロジェクトに適切なカスタマイズを追加するだけで済みます。

#### <a name="to-add-the-build-customizations-to-your-project"></a>プロジェクトにビルドのカスタマイズを追加するには

1. **ソリューション エクスプローラー**で、プロジェクトのショートカット メニューを開き、 **[ビルド依存関係]** 、 **[ビルドのカスタマイズ]** の順にクリックします。 **[Visual C++ ビルド カスタマイズ ファイル]** ダイアログ ボックスが表示されます。

2. **[使用できるビルド カスタマイズ ファイル]** で、次の表に示すように、プロジェクトで使用するアセットの種類に対応するチェック ボックスをオンにします。

    |アセットの種類|ビルドのカスタマイズの名前|
    |----------------|------------------------------|
    |テクスチャとイメージ|**ImageContentTask(.targets、.props)**|
    |3-D モデル|**MeshContentTask(.targets、.props)**|
    |シェーダー|**ShaderGraphContentTask(.targets、.props)**|

3. **[OK]** をクリックします。

## <a name="including-assets-in-your-build"></a>アセットをビルドに含める
 使用する 3-D アセットの種類をプロジェクトが認識できるようになったので、次に、3-D アセットがどのファイルに含まれ、どのような種類のアセットであるかを指示します。

#### <a name="to-add-an-asset-to-your-build"></a>アセットをビルドに追加するには

1. **ソリューション エクスプローラー**のプロジェクトで、アセットのショートカット メニューを開き、 **[プロパティ]** をクリックします。 アセットの **[プロパティ ページ]** ダイアログ ボックスが表示されます。

2. **[構成]** と **[プラットフォーム]** の各プロパティが、変更を適用する値に設定されていることを確認します。

3. **[構成プロパティ]** の **[全般]** をクリックし、プロパティ グリッドの **[全般]** で、 **[項目の種類]** プロパティを適切なコンテンツ パイプラインの項目の種類に設定します。 たとえば、イメージまたはテクスチャのファイルの場合、 **[Image Content Pipeline]\(イメージ コンテンツ パイプライン\)** を選びます。

   > [!IMPORTANT]
   > 既定では、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] は、多くの種類のイメージ ファイルが、**にビルドされている**[イメージ][!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 項目の種類を使用して分類する必要があることを前提としています。 したがって、イメージ コンテンツ パイプラインにより処理する各イメージの **[項目の種類]** プロパティを変更する必要があります。 3-D モデルおよび視覚シェーダー グラフィックスのその他の種類のコンテンツ パイプラインのソース ファイルの既定は、正しい **[項目の種類]** になります。

4. **[OK]** をクリックします。

   3 種類のコンテンツ パイプラインの項目の種類および関連のソース ファイルと出力ファイルの種類を、次に示します。

|アイテムの種類|ソース ファイルの種類|出力ファイル形式|
|---------------|-----------------------|------------------------|
|**イメージ コンテンツ パイプライン**|ポータブル ネットワーク グラフィックス (.png)<br /><br /> JPEG (.jpg、.jpeg、.jpe、.jfif)<br /><br /> DirectDraw Surface (dds)<br /><br /> グラフィックス インターチェンジ形式 (.gif)<br /><br /> ビットマップ (.bmp、.dib)<br /><br /> TIFF 形式 (.tif、.tiff)<br /><br /> Targa (.tga)|DirectDraw Surface (dds)|
|**メッシュ コンテンツ パイプライン**|AutoDesk FBX インターチェンジ ファイル (.fbx)<br /><br /> Collada DAE ファイル (.dae)<br /><br /> Wavefront OBJ ファイル (.obj)|3-D メッシュ ファイル (.cmo)|
|**シェーダー コンテンツ パイプライン**|視覚シェーダー グラフ (.dgsl)|コンパイル済みシェーダー出力 (.cso)|

## <a name="configuring-asset-content-pipeline-properties"></a>アセット コンテンツ パイプラインのプロパティを構成する
 特定の方法でビルドされるように、各アセット ファイルのコンテンツ パイプラインのプロパティを設定できます。

#### <a name="to-configure-content-pipeline-properties"></a>コンテンツ パイプラインのプロパティを構成するには

1. **ソリューション エクスプローラー**のプロジェクトで、アセット ファイルのショートカット メニューを開き、 **[プロパティ]** をクリックします。 アセットの **[プロパティ ページ]** ダイアログ ボックスが表示されます。

2. **[構成]** と **[プラットフォーム]** の各プロパティが、変更を適用する値に設定されていることを確認します。

3. **[構成プロパティ]** でコンテンツ パイプラインのノード、たとえばテクスチャおよびイメージのアセットの場合は **[Image Content Pipeline]\(イメージ コンテンツ パイプライン\)** を選び、プロパティのグリッドで、プロパティを適切な値に設定します。 たとえば、ビルド時に、テクスチャ アセットの MIPMAP を生成するには、 **[MIPS の生成]** プロパティを **[あり]** に設定します。

4. **[OK]** をクリックします。

### <a name="image-content-pipeline-configuration"></a>イメージ コンテンツ パイプラインの構成
 イメージ コンテンツ パイプライン ツールを使用してテクスチャ アセットをビルドする場合、さまざまな方法によるテクスチャの圧縮、ビルド時に MIPMAP レベルを生成するかどうかの指定、および出力ファイルの名前の変更を実行できます。

|プロパティ|説明|
|--------------|-----------------|
|**圧縮**|出力ファイルで使用される圧縮の種類を指定します。<br /><br /> 使用可能なオプションは次のとおりです。<br /><br /> -   **圧縮なし**<br />-   **BC1_UNORM 圧縮**<br />-   **BC1_UNORM_SRGB 圧縮**<br />-   **BC2_UNORM 圧縮**<br />-   **BC2_UNORM_SRGB 圧縮**<br />-   **BC3_UNORM 圧縮**<br />-   **BC3_UNORM_SRGB 圧縮**<br />-   **BC4_UNORM 圧縮**<br />-   **BC4_SNORM 圧縮**<br />-   **BC5_UNORM 圧縮**<br />-   **BC5_SNORM 圧縮**<br />-   **BC6H_UF16 圧縮**<br />-   **BC6H_SF16 圧縮**<br />-   **BC7_UNORM 圧縮**<br />-   **BC7_UNORM_SRGB 圧縮**<br /><br /> DirectX のさまざまなバージョンでサポートされている圧縮形式について詳しくは、「[Programming Guide for DXGI](https://go.microsoft.com/fwlink/p/?LinkId=246265)」(DXGI のプログラミング ガイド) をご覧ください。|
|Convert to pre-multiplied alpha format (前乗算されたアルファ形式に変換)|出力ファイルで前乗算されたアルファ形式に変換する場合は **[はい]** を、その他の場合は **[いいえ]** を選択します。 出力ファイルのみが変更され、ソース イメージは変更されません。|
|**MIPS の生成**|完全な MIPMAP チェーンをビルド時に生成し、出力ファイルに含める場合は、 **[あり]** 、それ以外は **[なし]** 。 **[なし]** をクリックすると、ソース ファイルに既に MIPMAP チェーンが含まれている場合は、出力ファイルに MIPMAP チェーンが含まれます。それ以外の場合は、出力ファイルに MIPMAP チェーンは含まれません。|
|**Content Output\(コンテンツ出力\)**|出力ファイルの名前を指定します。 **重要:**  出力ファイルのファイル名拡張子を変更しても、ファイル形式には影響しません。|

### <a name="mesh-content-pipeline-configuration"></a>メッシュ コンテンツ パイプラインの構成
 メッシュ コンテンツ パイプライン ツールを使用してメッシュ アセットをビルドする場合、出力ファイルの名前を変更できます。

|プロパティ|説明|
|--------------|-----------------|
|**Content Output\(コンテンツ出力\)**|出力ファイルの名前を指定します。 **重要:**  出力ファイルのファイル名拡張子を変更しても、ファイル形式には影響しません。|

### <a name="shader-content-pipeline-configuration"></a>シェーダー コンテンツ パイプラインの構成
 シェーダー コンテンツ パイプライン ツールを使用してシェーダー アセットをビルドする場合、出力ファイルの名前を変更できます。

|プロパティ|説明|
|--------------|-----------------|
|**Content Output\(コンテンツ出力\)**|出力ファイルの名前を指定します。 **重要:**  出力ファイルのファイル名拡張子を変更しても、ファイル形式には影響しません。|

## <a name="loading-and-using-3-d-assets-at-run-time"></a>実行時の 3-D アセットの読み込みおよび使用

### <a name="using-textures-and-images"></a>テクスチャおよびイメージを使用する
 Direct3D には、テクスチャ リソースを作成するための機能があります。 Direct3D 11 では、D3DX11 ユーティリティ ライブラリには、イメージ ファイルからテクスチャ リソースとリソース ビューを直接作成するための追加の機能が用意されています。 Direct3D 11 のテクスチャ リソースを作成する方法について詳しくは、「[Textures](https://go.microsoft.com/fwlink/p/?LinkID=246267)」(テクスチャ) をご覧ください。 D3DX11 ライブラリを使用してイメージ ファイルからテクスチャ リソースまたはリソース ビューを作成する方法について詳しくは、「[How to: Initialize a Texture From a File](https://go.microsoft.com/fwlink/p/?LinkId=246268)」(方法: ファイルからテクスチャを初期化する) をご覧ください。

### <a name="using-3-d-models"></a>3-D モデルを使用する
 Direct3D 11 には、3-D モデルからリソースを作成する機能がありません。 代わりに、3-D モデル ファイルを読み取るコードを記述し、3-D モデルおよびモデルが必要とするリソース (テクスチャ、シェーダーなど) を表す頂点バッファーとインデックス バッファーを作成する必要があります。

### <a name="using-shaders"></a>シェーダーを使用する
 Direct3D には、シェーダー リソースを作成してプログラム可能なグラフィックス パイプラインにバインドするための関数が用意されています。 Direct3D のシェーダー リソースを作成してパイプラインにバインドする方法について詳しくは、「[HLSL のプログラミング ガイド](https://go.microsoft.com/fwlink/p/?LinkID=261521)」をご覧ください。

 プログラミング可能なグラフィックス パイプラインでは、パイプラインの各ステージは、理解できる方法で書式設定された結果を、パイプラインの次のステージに渡す必要があります。 シェーダー デザイナーができることはピクセル シェーダーの作成のみであるため、受け取ったデータが要求する形式であることを確認するのはアプリケーションです。 複数のプログラミング可能なシェーダーのステージは、ピクセル シェーダー前に発生し、ジオメトリック変換 (頂点シェーダー、ハル シェーダー、ドメインのシェーダー、およびジオメトリ シェーダー) を実行します。 プログラミング不可能なテセレーション ステージもピクセル シェーダーの前に発生します。 ピクセル シェーダーの直前にどのステージがある場合でも、結果を以下の形式で渡す必要があります。

```hlsl

struct PixelShaderInput
{
    float4 pos : SV_POSITION;
    float4 diffuse : COLOR;
    float2 uv : TEXCOORD0;
    float3 worldNorm : TEXCOORD1;
    float3 worldPos : TEXCOORD2;
    float3 toEye : TEXCOORD3;
    float4 tangent : TEXCOORD4;
    float3 normal : TEXCOORD5;
};
```

 シェーダーで使用するシェーダー デザイナーのノードによっては、次の定義に従い、追加データを指定する必要がある場合もあります。

```

Texture2D Texture1 : register( t0 );
Texture2D Texture2 : register( t1 );
Texture2D Texture3 : register( t2 );
Texture2D Texture4 : register( t3 );
Texture2D Texture5 : register( t4 );
Texture2D Texture6 : register( t5 );
Texture2D Texture7 : register( t6 );
Texture2D Texture8 : register( t7 );

TextureCube CubeTexture1 : register( t8 );
TextureCube CubeTexture2 : register( t9 );
TextureCube CubeTexture3 : register( t10 );
TextureCube CubeTexture4 : register( t11 );
TextureCube CubeTexture5 : register( t12 );
TextureCube CubeTexture6 : register( t13 );
TextureCube CubeTexture7 : register( t14 );
TextureCube CubeTexture8 : register( t15 );

SamplerState TexSampler : register( s0 );

cbuffer MaterialVars : register (b0)
{
    float4 MaterialAmbient;
    float4 MaterialDiffuse;
    float4 MaterialSpecular;
    float4 MaterialEmissive;
    float MaterialSpecularPower;
};

cbuffer LightVars : register (b1)
{
    float4 AmbientLight;
    float4 LightColor[4];
    float4 LightAttenuation[4];
    float3 LightDirection[4];
    float LightSpecularIntensity[4];
    uint IsPointLight[4];
    uint ActiveLights;
}

cbuffer ObjectVars : register(b2)
{
    float4x4 LocalToWorld4x4;
    float4x4 LocalToProjected4x4;
    float4x4 WorldToLocal4x4;
    float4x4 WorldToView4x4;
    float4x4 UVTransform4x4;
    float3 EyePosition;
};

cbuffer MiscVars : register(b3)
{
    float ViewportWidth;
    float ViewportHeight;
    float Time;
};
```

## <a name="related-topics"></a>関連トピック

|タイトル|説明|
|-----------|-----------------|
|[方法: ミップマップを含むテクスチャをエクスポートする](../designers/how-to-export-a-texture-that-contains-mipmaps.md)|イメージ コンテンツ パイプラインを使用して、前計算された MIPMAP を含むテクスチャをエクスポートする方法について説明します。|
|[方法: 前乗算されたアルファを持つテクスチャをエクスポートする](../designers/how-to-export-a-texture-that-has-premultiplied-alpha.md)|イメージ コンテンツ パイプラインを使用して、前乗算されたアルファ値を含むテクスチャをエクスポートする方法について説明します。|
|[方法: Direct2D または Javascipt アプリで使用するためのテクスチャをエクスポートする](../designers/how-to-export-a-texture-for-use-with-direct2d-or-javascipt-apps.md)|イメージ コンテンツ パイプラインを使用して、Direct2D または JavaScript アプリで使用できるテクスチャをエクスポートする方法について説明します。|
|[ゲームとアプリ用の 3-D アセットの操作](../designers/working-with-3-d-assets-for-games-and-apps.md)|テクスチャとイメージ、3-D モデル、シェーダーを含む 3-D アセットを作成および操作するために Visual Studio に用意されている編集ツールについて説明します。|
|[方法: シェーダーをエクスポートする](../designers/how-to-export-a-shader.md)|シェーダー デザイナーからシェーダーをエクスポートする方法について説明します。|
