---
title: 図形とパスの描画 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: d5378c59-e2e5-49f0-91f1-aa82d984a33c
caps.latest.revision: 12
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: e9eba4e5bfef052f7a82c3148f5628eff9413180
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85542208"
---
# <a name="draw-shapes-and-paths"></a>図形とパスの描画
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

XAML デザイナーでは、 *図形* はまさに期待どおりのものです。 たとえば、四角形、円、楕円などです。 *パス* は、より柔軟なバージョンの図形です。 図形の形状を変更したり、図形を結合して新しい図形を形成するといった操作ができます。

 図形とパスではベクター グラフィックスを使用するため、高解像度表示に対応して拡大縮小できます。 ベクター グラフィックスの詳細については、 [ベクター グラフィックスに関するビデオ](https://www.youtube.com/watch?v=MoCSwF0n-io) や [ベクター グラフィックスに関するページ](https://www.webopedia.com/TERM/V/vector_graphics.html)を参照してください。

 **このトピックの内容:**

- [図形の描画](#Shape)

- [パスの描画](#Path)

- [図形をパスに変換する](#Convert)

- [パスの結合](#Combine)

- [複合パスを作成する](#Compound)

- [クリッピングパスを作成する](#Clipping)

## <a name="draw-a-shape"></a><a name="Shape"></a> 図形の描画
 図形は **[アセット]** パネルにあります。

 ![[アセット] パネルの [図形] カテゴリ](../designers/media/b4-shapes-assetspanel.png "b4_Shapes_AssetsPanel")

 目的の図形をアートボードにドラッグします。 次に、図形にあるハンドルを使用して、図形の拡大縮小、回転、移動、または傾斜を行います。

 ![](../designers/media/84261e83-3091-4490-ab58-4218b188439e.png "84261e83-3091-4490-ab58-4218b188439e")

## <a name="draw-a-path"></a><a name="Path"></a> パスを描画する
 パスは、直線と曲線が連結して一続きになったものです。 パスを使用すると、 **[アセット]** パネルでは使用できない面白い図形を作成できます。

 パスの描画には直線、ペン、または鉛筆を使用します。 これらのツールは **[ツール]** パネルにあります。

 ![](../designers/media/717956a8-b6a5-4e37-8af3-70bcfc78c82a.png "717956a8-b6a547 e378-8af3-70bcfc78c82a") ![](../designers/media/8fbbbb21-be83-4cf6-903b-3a49f00c9860.png "8fbbbb21-be8347 cf6-903b8-3a49f00c9860")

### <a name="draw-a-straight-line"></a>直線の描画
 **[ペン]** ツール ![](../designers/media/894f8612-e0ed-4e00-84cf-a9bc8f38fc54.png "894f8612-e0ed-4e00-84cf-a9bc8f38fc54")または **[直線]** ツール ![](../designers/media/eb618397-5283-48be-8396-3449be7b6fbf.png "eb618397-5283-48be-8396-3449be7b6fbf")を使用します。

 **ペンツールの使用**![](../designers/media/894f8612-e0ed-4e00-84cf-a9bc8f38fc54.png "894f8612-e0ed-4e00-84cf-a9bc8f38fc54")

 アートボード上で 1 回クリックし、始点を定義します。次に、再度クリックして直線の終わりを定義します。

 **直線ツールの使用**![](../designers/media/eb618397-5283-48be-8396-3449be7b6fbf.png "eb618397-5283-48be-8396-3449be7b6fbf")

 アートボード上で、直線の始点からドラッグして、終点でマウス ボタンを放します。

### <a name="draw-a-curve"></a>曲線の描画
 **[ペン]** ツール ![](../designers/media/894f8612-e0ed-4e00-84cf-a9bc8f38fc54.png "894f8612-e0ed-4e00-84cf-a9bc8f38fc54")を使用します。

 アートボード上で 1 回クリックして、直線の始点を定義してから、ポインターをクリックし、ドラッグして目的の曲線を作成します。

 パスを閉じる場合は、線上の最初の点をクリックします。

### <a name="change-the-shape-of-a-curve"></a>曲線のシェイプの変更
 **[個別選択]** ツール ![](../designers/media/6dd6571f-c116-451d-8dd2-1f88b8406362.png "6dd6571f-c116-451d-8dd2-1f88b8406362")を使用します。

 図形をクリックしてから、図形の任意のポイントをドラッグして曲線の形状を変更します。

### <a name="draw-a-free-form-path"></a>フリーハンドのパスの描画
 **[鉛筆]** ツール ![](../designers/media/509dc167-734f-46c9-b012-987ee63450cd.png "509dc167-734f47 6c012-987ee63450cd")を使用します。

 アートボード上で、実際の鉛筆のように自由にパスを描画できます。

### <a name="remove-part-of-a-path"></a>パスの一部の削除
 **[個別選択]** ツール ![](../designers/media/6dd6571f-c116-451d-8dd2-1f88b8406362.png "6dd6571f-c116-451d-8dd2-1f88b8406362")を使用します。

 削除する部分を含むパスを選択して、 **[削除]** ボタンをクリックします。

### <a name="remove-a-point-in-a-path"></a>パス内のポイントの削除
 **[選択]** ツール  ![](../designers/media/2ff91340-477e-4efa-a0f7-af20851e4daa.png "2ff91340-477e-4efa-a0f7-af20851e4daa")および **[ペン]** ツール ![](../designers/media/894f8612-e0ed-4e00-84cf-a9bc8f38fc54.png "894f8612-e0ed-4e00-84cf-a9bc8f38fc54")を使用します。

 [ **選択内容** ] ツールを使用し  ![](../designers/media/2ff91340-477e-4efa-a0f7-af20851e4daa.png "2ff91340-477e-4efa-a0f7-af20851e4daa") てパスを選択します。 次に、 **ペン** ツールを使用して、 ![](../designers/media/894f8612-e0ed-4e00-84cf-a9bc8f38fc54.png "894f8612-e0ed-4e00-84cf-a9bc8f38fc54") 削除するポイントをクリックします。

### <a name="add-a-point-to-a-path"></a>パスへのポイントの追加
 **[選択]** ツール  ![](../designers/media/2ff91340-477e-4efa-a0f7-af20851e4daa.png "2ff91340-477e-4efa-a0f7-af20851e4daa")および **[ペン]** ツール ![](../designers/media/894f8612-e0ed-4e00-84cf-a9bc8f38fc54.png "894f8612-e0ed-4e00-84cf-a9bc8f38fc54")を使用します。

 [ **選択内容** ] ツールを使用し  ![](../designers/media/2ff91340-477e-4efa-a0f7-af20851e4daa.png "2ff91340-477e-4efa-a0f7-af20851e4daa") てパスを選択します。 **ペン**ツールを使用して、 ![](../designers/media/894f8612-e0ed-4e00-84cf-a9bc8f38fc54.png "894f8612-e0ed-4e00-84cf-a9bc8f38fc54") ポイントを追加するパス上の任意の場所をクリックします。

## <a name="convert-a-shape-to-a-path"></a><a name="Convert"></a> 図形をパスに変換する
 パスを変更するのと同じ方法で図形を変更するには、図形をパスに変換します。

 **短いビデオを見る:** ![インストール済みフィーチャーの構成](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [パスの作業: 図形をパスに変換する](https://www.youtube.com/watch?v=Io5bC0-nH6Q#t=147)。

## <a name="combine-paths"></a><a name="Combine"></a> パスの結合
 パスと図形を結合して 1 つのパスにすることができます。

 ![](../designers/media/2df17a5d-a338-4ef4-96c5-dae51cc1ca8a.png "2df17a5d-a338-4ef4-96c5-dae51cc1ca8a")

|Image|説明|Image|説明|
|-|-|-|-|
|![](../designers/media/b1-1.png "B1_1")|結合前の 2 つの図形|![](../designers/media/b1-4.png "B1_4")|交差|
|![](../designers/media/b1-2.png "B1_2")|合算|![](../designers/media/b1-5.png "B1_5")|重複部分を除外|
|![](../designers/media/b1-3.png "B1_3")|除算|![](../designers/media/b1-6.png "B1_6")|減算|

 **短いビデオを見る:** ![インストール済みフィーチャーの構成](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [パスの作業: パスを結合する](https://www.youtube.com/watch?v=Io5bC0-nH6Q#t=195)。

## <a name="create-a-compound-path"></a><a name="Compound"></a> 複合パスを作成する
 複合パスを作成するときは、パスの交差している部分が減算されます。複合後のパスのビジュアル プロパティは、最背面にあったパスと同じになります。

 複合パスは、作成後はいつでも分離できます。

 ![](../designers/media/2157a8aa-d9a7-4de4-8de5-b10d28f08a84.png "2157a8aa-d9a7-4de4-8de5-b10d28f08a84")

 **短いビデオを見る:** ![インストール済みフィーチャーの構成](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [パスの作業: 複合パスを作成する](https://www.youtube.com/watch?v=Io5bC0-nH6Q)。

## <a name="create-a-clipping-path"></a><a name="Clipping"></a> クリッピングパスを作成する
 クリッピング パスは、別のオブジェクトに適用するパスまたは図形です。クリッピング パスの外側のオブジェクトがマスクされて非表示になります。

 ![](../designers/media/22471e98-a841-4f39-a3ef-36090cf5a625.png "22471e98-a841-4f39-a3ef-36090cf5a625")

 **短いビデオを見る:** ![インストール済みフィーチャーの構成](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [パスの作業: クリッピング パスを作成する](https://www.youtube.com/watch?v=Io5bC0-nH6Q#t=232)。

## <a name="see-also"></a>参照
 [Blend for Visual Studio を使用して UI を作成する](../designers/creating-a-ui-by-using-blend-for-visual-studio.md)
