---
title: デバッグ中の、呼び出し履歴に関するメソッドのマッピング
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.progression.debugwithcodemaps
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- call stacks, code maps
- Call Stack window, mapping calls
- debugging [Visual Studio], diagramming the call stack
- call stacks, mapping
- Call Stack window, visualizing
- debugging code visually
- debugging [Visual Studio], mapping the call stack
- call stacks, visualizing
- debugging, code maps
- Call Stack window, tracing calls visually
- Call Stack window, show on code map
- debugging [Visual Studio], tracing the call stack visually
- debugging [Visual Studio], visualizing the call stack
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4a918cc94cd242c74b672ff65c3d5093f111a25f
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75593305"
---
# <a name="map-methods-on-the-call-stack-while-debugging-in-visual-studio"></a>Visual Studio でデバッグを行うときの呼び出し履歴に対するメソッドのマップ

デバッグ中に呼び出し履歴を視覚的にトレースするためのコード マップを作成します。 コメントをマップに追加することでバグの発見に重点を置いてコードの動作を追跡できます。

 ![コード マップの呼び出し履歴を使用したデバッグ](../debugger/media/debuggermap_overview.png)

 要件:

 ::: moniker range="vs-2017"

- [Visual Studio Enterprise](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)

::: moniker-end

::: moniker range="vs-2019"

- [Visual Studio Enterprise](https://visualstudio.microsoft.com/downloads)

::: moniker-end

- Visual c#、Visual Basic、C++、JavaScript、または x++ など、デバッグできるコード

  参照トピック

- [ビデオ: は、コード マップ デバッガーの統合 (チャネル 9) で視覚的にデバッグします。](https://channel9.msdn.com/Series/Visual-Studio-2012-Premium-and-Ultimate-Overview/Visual-Studio-Ultimate-2012Debug-visually-with-Code-Map-debugger-integration)

- [呼び出し履歴でマップします。](#MapStack)

- [コードに関するメモを作成します。](#MakeNotes)

- [次の呼び出し履歴でマップを更新](#UpdateMap)

- [マップに関連するコードを追加します。](#AddRelatedCode)

- [マップを使用してバグを見つける](#FindBugs)

- [Q &AMP; A](#QA)

  コマンドとコード マップを使用する場合に使用できる操作の詳細については、次を参照してください。[参照およびコード マップの再配置](../modeling/browse-and-rearrange-code-maps.md)します。

## <a name="MapStack"></a>呼び出し履歴でマップを作成する

1. デバッグを開始します。 (キーボード: **F5**)

2. アプリが中断モードになるか、関数にステップ イン、選択**コード マップ**します。 (キーボード: **Ctrl** + **Shift** +  **`** )

     ![コード マップを選択して呼び出し履歴のマッピングを開始](../debugger/media/debuggermap_choosecodemap.png)

     現在の呼び出し履歴は新しいコード マップ上にオレンジ色で表示されます。

     ![コード マップの呼び出し履歴を参照](../debugger/media/debuggermap_seeundocallstack.png)

     デバッグを継続している間、マップは自動的に更新されます。 参照してください[次の呼び出し履歴でマップを更新](#UpdateMap)します。

## <a name="MakeNotes"></a>コードに関するコメントを追加する

 コードで何が起こっているかを追跡するためにコメントを追加します。 コメントで新しい行を追加するキーを押して**shift + return**します。

 ![コード マップの呼び出し履歴にコメントを追加](../debugger/media/debuggermap_addcomment.png)

## <a name="UpdateMap"></a>次の呼び出し履歴でマップを更新する

 アプリを次のブレークポイントまで実行するか、関数にステップ インします。 マップに新しい呼び出し履歴が追加されます。

 ![次の呼び出し履歴でコード マップを更新](../debugger/media/debuggermap_addclearcallstack.png)

## <a name="AddRelatedCode"></a>関連するコードをマップに追加する

 作成できたマップ - どのような横でしょうか。 C# または Visual Basic で作業している場合は、フィールド、プロパティ、およびコードで何が起こっているかを追跡するために、他の方法などの項目を追加します。

 メソッドのコード定義を表示するには、そのメソッドをダブルクリックするか、そのメソッドのショートカット メニューを使用します。 (キーボード: マップとキーを押してでメソッドを選択**F12**)

 ![コード マップのメソッドのコード定義に移動](../debugger/media/debuggermap_gotocodedefinition.png)

 マップで追跡する項目を追加します。

 ![呼び出し履歴コード マップのメソッドのフィールドを表示](../debugger/media/debuggermap_showfields.png)

> [!NOTE]
> 既定では、マップに項目を追加すると、クラス、名前空間、アセンブリなどの親グループのノードも追加されます。 便利ですが、おくと、マップ単純な機能を使用してこの機能をオフに、**親を含める**マップのツールバー、またはキーを押してボタン**CTRL**項目を追加するとします。

 ![呼び出し履歴コード マップのメソッドに関連するフィールド](../debugger/media/debuggermap_showedfields.png)

 ここでは、同じフィールドを使用するメソッドを簡単に表示できます。 追加された最新の項目は緑色で表示されます。

 コードのさらに多くの項目を表示するには、マップの作成を続けます。

 ![フィールドを使用するメソッドを参照: 呼び出し履歴コード マップ](../debugger/media/debuggermap_findallreferences.png)

 ![呼び出し履歴コード マップのフィールドを使用するメソッド](../debugger/media/debuggermap_foundallreferences.png)

## <a name="FindBugs"></a>マップを使用してバグを見つける

 コードの視覚化はバグをよりすばやく見つけるために役立ちます。 たとえば、描画プログラムでバグを調査するいるとします。 直線を描画して元に戻そうとしても、別の直線を描画するまで何も起こりません。

 そのため、`clear`、`undo`、および `Repaint` メソッドにブレークポイントを設定し、デバッグを開始して、次のようなマップを作成します。

 ![コード マップに別の呼び出し履歴を追加](../debugger/media/debuggermap_addpaintobjectcallstack.png)

 マップ上のすべてのユーザー ジェスチャーが、`Repaint` を除いて、`undo` を呼び出していることがわかります。 これが原因で `undo` がすぐに動作しない可能性があります。

 バグを修正してプログラムの実行を続けると、マップに `undo` から `Repaint` への新しい呼び出しが追加されます。

 ![コード マップの呼び出し履歴に新しいメソッド呼び出しを追加](../debugger/media/debuggermap_addnewcallforrepaint.png)

## <a name="QA"></a> Q & A

- **すべての呼び出しがマップに表示されるわけではありません。なぜでしょうか。**

   既定では、ユーザー自身のコードだけがマップに表示されます。 外部コードを表示するで有効にする、**呼び出し履歴**ウィンドウ。

   ![[呼び出し履歴] ウィンドウを使用して外部コードを表示](../debugger/media/debuggermap_callstackmenu.png)

   オフにするか**マイ コードのみを有効にする**Visual studio のデバッグ オプション。

   ![[オプション] ダイアログ ボックスを使用して、外部コードを表示](../debugger/media/debuggermap_debugoptions.png)

- **マップを変更するコードに影響しますか。**

   マップを変更すると、任意の方法でコードに影響しません。 マップでの名前変更、移動、削除は自由に行うことができます。

- **このメッセージの意味:「ダイアグラムは、コードの古いバージョンに基づく可能性があります」でしょうか。**

   マップを最後に更新してからコードが変更されている可能性があります。 たとえば、マップ上の呼び出しがコードに存在しなくなった可能性があります。 メッセージを閉じてから、マップを再び更新する前にソリューションをリビルドしてみます。

- **マップのレイアウトを制御する方法は?**

   開く、**レイアウト**マップのツールバー メニュー。

  - 既定のレイアウトを変更します。

  - オフにする、マップを自動的に再配置を停止する**デバッグ時に自動レイアウト**します。

  - 項目を追加するときに、できるだけ少なくのマップを再配置、オフにする。**インクリメンタル レイアウト**します。

- **マップを他のユーザーと共有できますか。**

   マップをエクスポート、Microsoft Outlook、またはソース管理にチェックインすることができますので、ソリューションに保存した場合は、他のユーザーに送信できます。

   ![呼び出し履歴コード マップを他のユーザーと共有](../debugger/media/debuggermap_sharewithothers.png)

- **新しい呼び出し履歴を自動的に追加することから、マップを停止するにはどうすればよいですか。**

   選択![ボタン&#45;Show コール スタックは、自動的にコード マップに](../debugger/media/debuggermap_automaticupdateicon.gif)マップのツールバー。 マップを現在の呼び出し履歴を手動で追加するには、キーを押して**Ctrl** + **Shift** +  **`** します。

   デバッグ中に、マップ上の既存の呼び出し履歴を強調表示、マップが続行されます。

- **項目のアイコンと矢印の意味**

   項目に関する詳細情報を取得するには、上にマウス ポインターを移動し、項目のツールヒントを確認します。 検索することも、**凡例**に各アイコンの意味について説明します。

   ![呼び出し履歴コード マップのアイコンの意味](../debugger/media/debuggermap_showlegend.png)

  参照トピック

- [呼び出し履歴でマップします。](#MapStack)

- [コードに関するメモを作成します。](#MakeNotes)

- [次の呼び出し履歴でマップを更新](#UpdateMap)

- [マップに関連するコードを追加します。](#AddRelatedCode)

- [マップを使用してバグを見つける](#FindBugs)

## <a name="see-also"></a>関連項目

- [ソリューション間の依存関係をマップする](../modeling/map-dependencies-across-your-solutions.md)
- [コード マップを使用してアプリケーションをデバッグする](../modeling/use-code-maps-to-debug-your-applications.md)
- [コード マップ アナライザーを使用して潜在的な問題を検索する](../modeling/find-potential-problems-using-code-map-analyzers.md)
- [コード マップの参照および再配置](../modeling/browse-and-rearrange-code-maps.md)
