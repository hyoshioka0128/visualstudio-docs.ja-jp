---
title: シェーダーの操作 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: 6b2ea1ed-b995-4e75-af19-c68fd37a3bc5
caps.latest.revision: 10
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 3a22be61d5f4c05720a5ff223806f2e14a8bfbc0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72663946"
---
# <a name="working-with-shaders"></a>シェーダーの操作
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] のグラフ ベースのシェーダー デザイナーを利用し、自分だけのシェーダー効果をデザインできます。 自分でデザインしたシェーダーは、DirectX ベースのゲームやアプリで利用できます。

## <a name="shaders"></a>シェーダー
 *シェーダー*は、頂点変換やピクセル色付けなど、グラフィックス計算を実行するコンピューター プログラムです。通常、CPU ではなく、グラフィック処理装置 (GPU) で実行されます。 従来の固定関数グラフィックスのパイプラインのほとんどの段階がシェーダー プログラムで実行されるようになったため、アプリのニーズに合ったパイプラインをシェーダー プログラムで作成できます。

 最も一般的なシェーダーが*頂点シェーダー*と*ピクセル シェーダー*です。頂点シェーダーは頂点ごとに計算を実行し、プログラムできないグラフィックス ハードウェアにおいて、固定関数変換や照明回路構成に取って代わります。ピクセル シェーダーはピクセルの色を決定する計算をピクセルごとに実行し、プログラムできないグラフィックス ハードウェアにおいて、固定関数カラー結合回路構成に取って代わります。 現代的なグラフィックス ハードウェアの登場で、さまざまなシェーダーが可能になりました。*ハル シェーダー*、*ドメイン シェーダー*、*ジオメトリ シェーダー*はグラフィックス計算に使用されます。*計算シェーダー*はグラフィックス以外の計算処理に使用されます。 これらの段階はいずれも、プログラムできないグラフィックス ハードウェアでは利用できません。 シェーダーはもともと、データ並列 (SIMD) 指示やグラフィックス中心 (ドット積) 指示を与えたアセンブリ タイプの言語を利用して作られました。 現在、シェーダーは通常、HLSL (High Level Shader Language) のようなハイレベルな、C に近い言語で作られています。

 コードを入力し、コンパイルする代わりに、シェーダー デザイナーを利用してピクセル シェーダーを対話方式で作成できます。 シェーダー デザイナーでは、シェーダーは、データと演算を表すさまざまなノードと、データ値のフローとシェーダー全体の中間結果を表すノード間の接続で定義されます。 この手法とシェーダー デザイナーのリアルタイム プレビューを利用し、シェーダーの実行を簡単に視覚化し、実験を通してシェーダーの面白い変化を "発見" できます。

## <a name="dgsl-documents"></a>DGSL ドキュメント
 シェーダー デザイナーは Directed Graph Shader Language (DGSL) 形式でシェーダーを保存します。これは、Directed Graph Markup Language (DGML) を基盤とする XML 形式です。 モデル エディターで、3-D モデルに DGSL シェーダーを直接適用できます。 ただし、アプリで DGSL シェーダーを使用するには、DirectX が認識できる形式にシェーダーをエクスポートする必要があります。

 DGSL と DGML には互換性があるため、DGML ドキュメントを解析するために設計されたツールを利用して DGSL シェーダーを解析できます。 DGML の詳細については、「[Directed Graph Markup Language (DGML) について](https://msdn.microsoft.com/library/ee842619.aspx)」を参照してください。

## <a name="related-topics"></a>関連トピック

|タイトル|[説明]|
|-----------|-----------------|
|[シェーダー デザイナー](../designers/shader-designer.md)|[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] シェーダー デザイナーを使用してシェーダーを操作する方法について説明します。|
|[シェーダーデザイナーノード](../designers/shader-designer-nodes.md)|グラフィックス効果を得るためのシェーダー デザイナー ノードについて説明します。|
|[シェーダーデザイナーの例](../designers/shader-designer-examples.md)|シェーダー デザイナーを利用して一般的なグラフィックス効果を得る方法を示すトピックのリンクを提供します。|
