---
title: XML スキーマデザイナーのワークスペース |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: 588fa495-fe7f-4b16-8a9f-6b6b8d2d502a
caps.latest.revision: 9
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 8a16be3adb799fe2b0751d6119e5a980dd1b90d4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72669382"
---
# <a name="xml-schema-designer-workspace"></a>XML スキーマ デザイナーのワークスペース
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

XML スキーマ デザイナー (XSD デザイナー) は、XML スキーマを調べるために使用できるグラフィカル ツールです。 Xml スキーマ [エクスプローラー](../xml-tools/xml-schema-explorer.md)を使用すると、xml スキーマツリーを参照して移動したり、検索を実行したりすることができます。 xsd デザイナーには、xsd スキーマをより詳細に調べることができる3つのビューが用意されています。 スタート ビューは XSD デザイナーの起点で、スタート ビューからは、XSD デザイナーの他のビューに移動したり、スキーマ セットの詳細を表示したりすることができます。 グラフ ビューでは、スキーマ セットの概要とスキーマ ノード間のリレーションシップを表示できます。 コンテンツ モデル ビューには、単純型、複合型、要素、グループ、属性、属性グループなど、ローカル スキーマ ノードとグローバル スキーマ ノードの詳細がグラフィック表示されます。

 目的のノードを調べるには、ワークスペースにノードを追加する必要があります。 ワークスペースは、すべてのビューで共有されます。

## <a name="adding-nodes-to-the-workspace"></a>ワークスペースへのノードの追加
 次の方法でワークスペースにノードを追加できます。

- [スタート ビュー](../xml-tools/start-view.md) の [スキーマ セットの詳細] セクションで、グローバル ノード型の横にある **[追加]** リンクをクリックします。

- XML スキーマ エクスプローラーからは、3 つのどのビューにでもグローバル ノード、ファイル ノード、および名前空間ノードをドラッグ アンド ドロップすることができます。 詳細については、「[XML スキーマ エクスプローラー](../xml-tools/xml-schema-explorer.md)」の「ノードのドラッグ アンド ドロップ」セクションを参照してください。

- XML スキーマ エクスプローラーのコンテキスト メニューを使用します。 詳細については、「 [コンテキストメニュー](../xml-tools/context-menus-xml-schema-explorer.md)」を参照してください。

- XSD エクスプローラーで検索を実行して、概要結果ペインの **[強調表示されたノードをワークスペースに追加]** ボタンをクリックします。 詳細については、「 [スキーマセットの検索](../xml-tools/searching-the-schema-set.md)」を参照してください。

## <a name="view-switching"></a>ビューの切り替え
 ビューを切り替えるには、次のいずれかを使用します。

- XSD デザイナーのツール バー。

- コンテンツ モデル ビューおよびグラフ ビューのコンテキスト メニュー

- スタート ビューのウォーターマークか、空白のコンテンツ モデル ビューまたはグラフ ビューのウォーターマーク。

- ホット キー: スタート ビューに切り替えるには Ctrl + 1、グラフ ビューに切り替えるには Ctrl + 2、およびコンテンツ モデル ビューに切り替えるには Ctrl + 3。

## <a name="in-this-section"></a>このセクションの内容

- [スタート ビュー](../xml-tools/start-view.md)

- [グラフ ビュー](../xml-tools/graph-view.md)

- [コンテンツ モデル ビュー](../xml-tools/content-model-view.md)
