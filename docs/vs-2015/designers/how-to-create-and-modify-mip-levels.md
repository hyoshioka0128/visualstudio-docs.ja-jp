---
title: '方法: MIP レベルを作成および変更する | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: f64d4369-2307-4175-a39a-2e45506f7fa1
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 99d2b07a64781929962ff37823ddcbf219598331
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72664478"
---
# <a name="how-to-create-and-modify-mip-levels"></a>方法: MIP レベルを作成および変更する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このドキュメントでは、**イメージ エディター**を使用して、テクスチャ空間詳細レベル (LoD) の *MIPMAP レベル*を作成および変更する方法を示します。

## <a name="generating-mip-levels"></a>MIPMAP レベルの生成
 *MIPMAP* は、さまざまなサイズのテクスチャの複数のコピーを事前計算して格納することでレンダリングを高速化し、テクスチャ オブジェクトに対するエイリアシング効果を減らすために使用される手法です。 これらの各コピーは MIPMAP レベルと呼ばれ、それぞれの幅と高さは前のコピーの半分になっています。 テクスチャがオブジェクトの表面に表示されると、テクスチャのサーフェイスの画面スペース領域にほぼ一致する MIPMAP レベルが自動的に選択されます。 これは、一貫した表示画質を保持するために、グラフィックス ハードウェアが特大テクスチャをフィルター処理する必要がないことを意味します。 MIPMAP レベルを格納するためのメモリ消費は、元のテクスチャのみ格納するときよりも約 33% 増えますが、パフォーマンスとイメージの品質は向上します。

#### <a name="to-generate-mip-levels"></a>MIPMAP レベルを生成するには

1. 「[方法: 基本テクスチャを作成する](../designers/how-to-create-a-basic-texture.md)」の説明に従って、基本テクスチャから始めます。 最適な結果を得るには、テクスチャの高さと幅のサイズは、2 の累乗 (256、512、1024 など) に指定します。

2. MIPMAP レベルを生成します。 **[イメージ エディターのモード]** ツール バーで、 **[詳細設定]** 、 **[ツール]** 、 **[MIPS の生成]** の順にクリックします。

     **[Go to Next MIP Level]** (次の MIPMAP レベルに移動) および **[Go to Previous MIP Level]** (前の MIPMAP レベルに移動) ボタンが **[イメージ エディターのモード]** ツール バーに表示されていることに注意してください。 **[プロパティ]** ウィンドウが表示されている場合は、読み取り専用プロパティである **[MIPMAP レベル]** と **[MIPMAP レベル数]** がイメージのプロパティに表示されていることにも注意してください。

## <a name="modifying-mip-levels"></a>MIPMAP レベルの変更
 特殊効果を実現したり、特定の詳細レベルでイメージの品質を向上させたりするためには、各 MIPMAP レベルを個別に変更します。 たとえば、テクスチャ オブジェクトに距離を指定して外観が異なるようにしたり (距離が離れるほど、MIPMAP レベルは小さくなります)、テキストまたはシンボルを含むテクスチャについて小さい MIPMAP レベルでも読みやすくしたりすることができます。

#### <a name="to-modify-an-individual-mip-level"></a>MIPMAP レベルを個別に変更するには

1. 変更する MIPMAP レベルを選択します。 **[イメージ エディターのモード]** ツール バーで、 **[Go to Next MIP Level]** (次の MIPMAP レベルに移動) および **[Go to Previous MIP Level]** (前の MIPMAP レベルに移動) を使用し、MIPMAP レベルの間で移動します。

2. 変更する MIPMAP レベルを選択した後、描画ツールを使用して、他の MIPMAP レベルの内容を変更せずに、その MIPMAP レベルの内容のみ変更できます。 描画ツールは**イメージ エディター**のツール バーで使用できます。 ツールを選択した後は、 **[プロパティ]** ウィンドウでそのツールのプロパティを変更できます。 描画ツールとそれらのプロパティの詳細については、「[イメージ エディター](../designers/image-editor.md)」を参照してください。

> [!NOTE]
> 各 MIPMAP レベルの内容を変更する必要がない場合 (特定の効果を得るためになど)、ビルド時にソース テクスチャから MIPMAP を生成することをお勧めします。 これは、MIPMAP レベルがソース テクスチャと確実に同期するために役立ちます。1 つの MIPMAP レベルに対する変更がその他の MIPMAP レベルに自動的に反映されないためです。 ビルド時に mipmap を生成する方法については、「[方法: ミップマップを含むテクスチャをエクスポートする](../designers/how-to-export-a-texture-that-contains-mipmaps.md)」を参照してください。

## <a name="see-also"></a>参照
 [方法: 基本テクスチャを作成する](../designers/how-to-create-a-basic-texture.md)
