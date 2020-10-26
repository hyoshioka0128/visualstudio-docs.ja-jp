---
title: ワークフローデザイナーシェルの機能 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- WFDShellFeatures.UI
ms.assetid: 14bfe312-9592-408e-92ce-e98585ad16e7
caps.latest.revision: 6
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 2c59dc8232713d4126b2c37693a1e241735eb163
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72606600"
---
# <a name="workflow-designer-shell-features"></a>ワークフロー デザイナーのシェルの機能
[!INCLUDE[wfd1](../includes/wfd1-md.md)] は、デザイナー画面、その上の階層リンクバー、およびその下のシェルの3つの主要な UI 領域で構成されています。 階層リンク バーは画面の上部に位置し、現在のルート アクティビティの先祖の一覧を表示するために使用されます。 [!INCLUDE[crdefault](../includes/crdefault-md.md)][方法: 階層リンクナビゲーションを使用](../workflow-designer/how-to-use-breadcrumb-navigation.md)する。 デザイナー画面は画面の中央に位置し、ワークフローを作成するために使用されます。 シェルは画面の下部に位置しており、ここには、現在のビューを管理するためのさまざまなボタンが含まれています。

## <a name="shell-features"></a>シェルの機能
 シェルのバーの右側にあるボタンを使用して、ワークフローのズームインとズームアウト、画面のサイズに合わせたワークフローの内容の調整、および概要マップの表示/非表示の切り替えを行うことができます。 ワークフローのズームインとズームアウトは、キーボード ショートカットでも実行できます。Ctrl キーを押しながら、+ キーを押すとズームインし、- キーを押すとズームアウトします。

## <a name="overview-map"></a>概要マップ
 概要マップには、現在の階層リンク ルートでのアクティビティ全体が縮小表示されます。これには、すべての子、およびその展開された子のすべてが含まれます。 オレンジ色の罫線に囲まれた四角形のビューポートによって、エディター内で現在表示されているアクティビティの一部が示されます。 この四角形を概要マップ内でドラッグすると、ワークフロー デザイナーがスクロールされ、エディターのビューが変化します。

> [!NOTE]
> [!INCLUDE[wfd2](../includes/wfd2-md.md)] ユーザー インターフェイスは仮想化されています。 アクティビティ デザイナーは、必要なときにのみ表示されます。 デザイナー画面でワークフローの一部がまだ描画されていない場合は、その部分が概要マップで白く表示されます。 概要マップをスクロールすると、ワークフロー全体が描画されます。

## <a name="copying-or-saving-workflows-as-images"></a>ワークフローをイメージとしてコピーまたは保存
 ワークフローは、ビットマップ形式でのコピーや、ビットマップまたはベクター形式での保存が可能です。 イメージをコピーまたは保存すると、現在の階層リンク ルートにおけるアクティビティ全体 (すべての子およびそれらの展開された子のすべてを含む) のビューを別のプログラムにエクスポートできます。

 イメージとしてコピーするには、デザイナー内の任意の場所を右クリックし、[ **イメージとしてコピー**] を選択します。 イメージとして保存するには、デザイナー内の任意の場所を右クリックし、[ **イメージとして保存**] を選択します。 ワークフローは、JPG、PNG、GIF、および XPS の各形式のいずれかで保存できます。 この形式は、ウィンドウの下部にある [**名前を付けて保存**] ボックスの一覧にある [**名前**を付けて保存] ダイアログボックスで選択します。

## <a name="fonts-and-colors"></a>フォントおよび色
 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 内の[!INCLUDE[vs2010](../includes/vs2010-md.md)]で使用する色は、環境フォントにより制御されます。 オペレーティング システムのテーマにハイコントラストの配色を使用している場合は、[!INCLUDE[wfd2](../includes/wfd2-md.md)]で表示される色が変わります。 フォントまたは色の設定の変更後に[!INCLUDE[vs2010](../includes/vs2010-md.md)]で変更を有効にするには、[!INCLUDE[wfd2](../includes/wfd2-md.md)] を再起動する必要があります。