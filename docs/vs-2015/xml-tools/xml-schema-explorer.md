---
title: XML スキーマエクスプローラー |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: 2fc39e98-b194-456b-a452-cfafb0a52d66
caps.latest.revision: 11
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 5e9f61c56dd7ff2a9c6c19afc20ed279a7fdf855
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72669374"
---
# <a name="xml-schema-explorer"></a>XML スキーマ エクスプローラー
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

XML スキーマ エクスプローラーは Microsoft Visual Studio および XML エディターに統合されており、これを使用すると、XML スキーマ定義言語 (XSD) スキーマの操作が可能になります。 XML スキーマファイルを開くと、XML スキーマエクスプローラーに [ **スキーマセット** ] ノードが表示されます。 XML スキーマ エクスプローラーには、対象ファイルに対してインクルード、インポート、または再定義されたすべてのスキーマだけでなく、`include` ステートメントまたは `import` ステートメントを通じて参照されているファイルも表示されます。

 XML スキーマ エクスプローラーでは、次の操作を実行できます。

- スキーマ セットの概要をすばやく確認する。

- ツリーを参照して移動する。

- キーワード検索とスキーマ固有の検索を実行する。 詳細については、「 [スキーマセットの検索](../xml-tools/searching-the-schema-set.md)」を参照してください。

- グラフ ビューまたはコンテンツ モデル ビューに検索結果を追加する。

- ドキュメントの順序、ドキュメントの種類、またはドキュメント名でツリーを並べ替える。 詳細については、「 [並べ替え、フィルター処理、およびグループ化](../xml-tools/sorting-filtering-and-grouping-xml-schema-explorer.md)」を参照してください。

- XML エディターを開き、XSD ファイルのコードの場所にジャンプする。 詳細については、「 [XML エディターとの統合](../xml-tools/integration-with-xml-editor.md)」を参照してください。

- グローバル要素のサンプル XML を生成する。

  XML スキーマ エクスプローラーでは、ツリー ビューでスキーマ セットの階層を表示することができます。 また、検索、フィルター処理、ナビゲーション、および並べ替えを行うこともできます。 XML スキーマ エクスプローラーにアクセスするには、次のいずれかの操作を実行します。

- [スタート ビュー](../xml-tools/start-view.md)が表示されている場合は、 **[XML スキーマ エクスプローラー]** リンクをクリックします。

- [グラフビュー](../xml-tools/graph-view.md)または[コンテンツモデルビュー](../xml-tools/content-model-view.md)で、ワークスペースにノードがある場合は、コンテキストメニューを使用して XML スキーマエクスプローラーを選択します。

- また、[ **表示** ] メニューの [XML スキーマ] Explorerfrom を選択することもできます。

- XML スキーマ Explorerfrom ファイルにアクセスするには、.xsd ファイルに関連付けられている Visual Basic XML リテラルが必要です。 XML スキーマエクスプローラーでスキーマセットを表示するには、xml リテラルまたは XML 名前空間インポートで XML ノードを右クリックし、[ **スキーマエクスプローラーで表示** ] コマンドを選択します。 詳細については、「xml [リテラルと Xml スキーマエクスプローラーの統合](../xml-tools/integration-of-xml-literals-with-xml-schema-explorer.md)」を参照してください。

## <a name="tree-view"></a>ツリー ビュー
 XML スキーマ エクスプローラーでは、事前にコンパイルされたスキーマ セット情報がツリー構造で表示されます。 ツリー構造は、次のように構成されます。

- 最上位レベルは、スキーマ セット ノードです。

- 2 番目のレベルには名前空間が含まれます。

- 3 番目のレベルにはファイルが含まれます。

- 4 番目のレベルにはグローバル ノードが含まれます。 これには、要素、グループ、複合型、単純型、属性、属性グループ、`include` ステートメント`import` ステートメント、および `redefine` ステートメントを含めることができます。

  ツリー構造の例を次に示します。

  ![XML スキーマ エクスプローラー](../xml-tools/media/xmlschemaexplorer.gif "XMLSchemaExplorer")

## <a name="selection-and-activation"></a>選択とアクティブ化
 ノードを強調表示して選択するには、スキーマ エクスプローラーでそのノードをクリックします。

 ノードをアクティブ化するには、ノードをダブルクリックするか、ノードを選択して **Enter** キーを押します。

- ノードをアクティブ化すると、このノードが定義されているファイルが開き (ファイルが既に開かれていない場合)、ファイル内でノードが選択されます。

- ファイル ノードをアクティブ化すると、選択されたファイルが開き (既に開かれていない場合)、`<schema>` ノードが強調表示されます。

- SchemaSet または名前空間ノードをアクティブ化しても、何も行われません。

## <a name="draging-and-dropping-nodes"></a>ノードのドラッグ アンド ドロップ
 グローバル ノード、ファイル ノード、名前空間ノードを XSD デザイナーのビューにドラッグ アンド ドロップすることができます。 現在のビューが[スタート ビュー](../xml-tools/start-view.md)の場合は、ビューにノードをドラッグすると、[グラフ ビュー](../xml-tools/graph-view.md)が開きます。 現在のビューが[コンテンツ モデル ビュー](../xml-tools/content-model-view.md)またはグラフ ビューの場合は、ビューにノードをドロップしてもビューは変化しません。

 ビューでファイルを削除すると、ファイル内のすべてのグローバルノードが [XSD デザイナーワークスペース](../xml-tools/xml-schema-designer-workspace.md)に追加されます。 ビューに名前空間をドロップすると、名前空間内のすべてのグローバル ノードがワークスぺースに追加されます。 ワークスペースは、すべてのビューで共有されます。

 ローカル ノードまたはローカル インポートをドラッグ アンド ドロップすることはできません。

## <a name="in-this-section"></a>このセクションの内容

- [スキーマセットの検索](../xml-tools/searching-the-schema-set.md)

- [並べ替え、フィルター処理、およびグループ化](../xml-tools/sorting-filtering-and-grouping-xml-schema-explorer.md)

- [コンテキストメニュー](../xml-tools/context-menus-xml-schema-explorer.md)

- [Xml リテラルと XML スキーマエクスプローラーの統合](../xml-tools/integration-of-xml-literals-with-xml-schema-explorer.md)

## <a name="see-also"></a>参照
 [方法: XML スキーマエクスプローラーからワークスペースにノードを追加する](../xml-tools/how-to-add-nodes-to-the-workspace-from-the-xml-schema-explorer.md)
