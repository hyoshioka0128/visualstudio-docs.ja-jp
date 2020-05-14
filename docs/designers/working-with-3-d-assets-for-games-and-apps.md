---
title: ゲームとアプリ用の 3D アセットの操作
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.graphics
ms.assetid: 910d673b-c884-4eeb-9928-0e89f3d38cb6
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: aa9fc04df3e817730492353e54d74c1e46c3775e
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "75589800"
---
# <a name="work-with-3d-assets-for-games-and-apps"></a>ゲームとアプリ用の 3D アセットを操作する

この記事では、DirectX ベースのゲームおよびアプリケーション向けの 3D モデル、テクスチャ、シェーダーの作成または変更に使用できる、Visual Studio のツールについて説明します。

## <a name="directx-app-development-in-visual-studio"></a>Visual Studio における DirectX アプリケーションの開発

DirectX アプリケーションは、通常、プログラミング ロジック、DirectX API、および HLSL (High Level Shading Language) プログラムを、オーディオおよび 3D ビジュアル アセットと組み合わせることによって、リッチで対話型のマルチメディア エクスペリエンスを提供します。 Visual Studio には、イメージとテクスチャ、3D モデル、シェーダーなどの操作を行うために使用できるツールが用意されています。そのため、別のツールを使用するために IDE を終了する必要がありません。 Visual Studio のツールは、*プレースホルダー* アセットの作成に特に適しています。プレースホルダーを使用すると、稼動準備のできたアセットをコミッションする前にコードのテストやプロトタイプの構築を行ったり、稼動準備のできたアセットをアプリケーションのデバッグ時に検査および変更したりすることができます。

Visual Studio で使用できるアセットの種類に関する詳細を以下に示します。

### <a name="images-and-textures"></a>イメージおよびテクスチャ

イメージとテクスチャは、ゲームやアプリケーションに色と視覚的なディテールを与えます。 3D グラフィックスでは、さまざまな用途に対応した、さまざまな形式、種類、および形状のテクスチャが使用されます。 たとえば、通常のマップには、3D モデルの精細な光源を生成するためのピクセル単位の表面法線があり、キューブ マップには、スカイボックス化、反射、球状テクスチャ マッピングなどのための全方向テクスチャがあります。 テクスチャは、さまざまな精細度のレンダリングを効率的に行うための MIP マップを備えており、さまざまなチャネルと順序の色をサポートしています。 テクスチャはさまざまな圧縮形式で格納できます。圧縮形式は専用グラフィックス メモリの占有率が低いため、GPU はテクスチャに効率的にアクセスできるようになります。

Visual Studio のイメージ エディターを使用すると、さまざまな一般的な種類や形式のイメージとテクスチャを操作できます。

### <a name="3d-models"></a>3D モデル

3D モデルは、ゲームやアプリケーションで空間と図形を作成します。 3D モデルでは、3D 空間内の各ポイント (*頂点*とも呼ばれる) の位置をインデックス化データと共にエンコードするなどして、そのモデルの形状を表す線や三角形が定義されます。 これらの頂点には、色の情報、法線ベクター、アプリケーションに固有の属性など、追加のデータを関連付けることができます。 オブジェクトのサーフェイスの外観を計算するためにどのシェーダーを使用し、どのテクスチャを適用するかなど、オブジェクト全体の属性もモデルごとに定義できます。

Visual Studio のモデル エディターを使用すると、さまざまな一般的な形式の 3D モデルを操作できます。

### <a name="shaders"></a>シェーダー

シェーダーとは、グラフィックス プロセッシング ユニット (GPU) 上で実行される、ドメインに固有の小容量プログラムのことです。 シェーダーは、3D モデルを画面上の図形に変換する方法と、それらの図形を構成する各ピクセルに色を指定する方法を決定します。 シェーダーを作成して、ゲームまたはアプリケーション内のオブジェクトに適用することにより、そのオブジェクトに独自の外観を持たせることができます。

グラフ ベースのシェーダー デザイン ツールである Visual Studio のシェーダー デザイナーを使用すると、HLSL プログラミングに関する知識がなくてもカスタムの視覚効果を作成できます。

> [!NOTE]
> DirectX プログラミングの開始方法について詳しくは、[DirectX](/windows/win32/directx) に関するページをご覧ください。 DirectX ベースのアプリをデバッグする方法について詳しくは、「[グラフィックス診断 (DirectX グラフィックスのデバッグ)](../debugger/graphics/visual-studio-graphics-diagnostics.md)」をご覧ください。

## <a name="directx-version-compatibility"></a>DirectX のバージョンの互換性

Visual Studio では、DirectX を使用して 2D アセットおよび 3D アセットをレンダリングします。 DirectX 11 のレンダラーと Windows Advanced Rasterization Platform (WARP) ソフトウェアのレンダラーのいずれかを選択できます。 DirectX 11 のレンダラーを使用すると、DirectX 11 および DirectX 10 の各 GPU 上でハードウェア アクセラレータによる高性能レンダリングを実行できます。 WARP レンダラーを使用すると、最新式のグラフィックス ハードウェアを搭載していないコンピューターからグラフィックス ハードウェアを内蔵しているコンピューターまで、多様な種類のコンピューターとアセットが確実に連動するようになります。 WARP について詳しくは、「[Windows Advanced Rasterization Platform (WARP) Guide](/windows/win32/direct3darticles/directx-warp)」(Windows Advanced Rasterization Platform (WARP) ガイド) をご覧ください。

## <a name="related-topics"></a>関連トピック

|タイトル|[説明]|
|-----------|-----------------|
|[テクスチャおよびイメージの使用](../designers/working-with-textures-and-images.md)|Visual Studio を使用してイメージとテクスチャを操作する方法について説明します。|
|[3D モデルの操作](../designers/working-with-3-d-models.md)|Visual Studio を使用して 3D モデルを操作する方法について説明します。|
|[シェーダーの操作](../designers/working-with-shaders.md)|Visual Studio のシェーダー デザイナーを使用してカスタム シェーダー効果を作成および変更する方法について説明します。|
|[ゲームまたはアプリでの 3D アセットの使用](../designers/using-3-d-assets-in-your-game-or-app.md)|イメージ エディター、モデル エディター、またはシェーダー デザイナーを使用して作成したアセットをゲームまたはアプリケーションで使用する方法について説明します。|
