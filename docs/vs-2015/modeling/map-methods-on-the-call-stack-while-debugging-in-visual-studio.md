---
title: デバッグ中の、呼び出し履歴に関するメソッドのマッピング
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
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
ms.assetid: d6a72e5e-f88d-46fc-94a3-1789d34805ef
caps.latest.revision: 43
author: MikeJo5000
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 2a2c6e95822794394dbdfc7f53104b31b7c17ea9
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74296068"
---
# <a name="map-methods-on-the-call-stack-while-debugging-in-visual-studio"></a>Visual Studio でデバッグを行うときの呼び出し履歴に対するメソッドのマップ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

デバッグ中に呼び出し履歴を視覚的にトレースするためのコード マップを作成します。 コメントをマップに追加することでバグの発見に重点を置いてコードの動作を追跡できます。

 ![コードマップでの呼び出し履歴を使用したデバッグ](../debugger/media/debuggermap-overview.png "DebuggerMap_Overview")

 要件:

- [Visual Studio Enterprise](https://www.visualstudio.com/downloads/download-visual-studio-vs)

- デバッグできるコード (Visual C# .NET、Visual Basic .NET、C++、JavaScript、X++ など) です。

  参照:[ビデオ: コードマップデバッガーの統合を使用して視覚的にデバッグする (Channel 9)](https://go.microsoft.com/fwlink/?LinkId=293418) •[コールスタックをマップ](#MapStack)する•[コードに関するメモを作成](#MakeNotes)する•[次の呼び出し履歴でマップを更新](#UpdateMap)する•[関連するコードをマップに追加する](#AddRelatedCode)• map を[使用してバグを見つける](#FindBugs)• [Q & A](#QA)

  コードマップを操作するときに使用できるコマンドとアクションの詳細については、「[コードマップの参照および再配置](../modeling/browse-and-rearrange-code-maps.md)」を参照してください。

## <a name="MapStack"></a>呼び出し履歴でマップを作成する

1. デバッグを開始します。 (キーボード: **F5**)

2. アプリが中断モードになった後、または関数にステップインする場合は、 **[コードマップ]** を選択します。 (キーボード: **Ctrl** + **Shift** +  **`** )

     ![コードマップを選択して、呼び出し履歴のマッピングを開始します](../debugger/media/debuggermap-choosecodemap.png "DebuggerMap_ChooseCodeMap")

     現在の呼び出し履歴は新しいコード マップ上にオレンジ色で表示されます。

     ![コードマップの呼び出し履歴を表示する](../debugger/media/debuggermap-seeundocallstack.png "DebuggerMap_SeeUndoCallStack")

     デバッグを継続している間、マップは自動的に更新されます。 「[次の呼び出し履歴でマップを更新する」を](#UpdateMap)参照してください。

## <a name="MakeNotes"></a>コードに関するコメントを追加する
 コードの動作を追跡するためのコメントを追加します。 コメントに新しい行を追加するには、Shift キーを押し**ながら Return**キーを押します。

 ![コードマップの呼び出し履歴にコメントを追加する](../debugger/media/debuggermap-addcomment.png "DebuggerMap_AddComment")

## <a name="UpdateMap"></a>次の呼び出し履歴でマップを更新する
 アプリを次のブレークポイントまで実行するか、関数にステップ インします。 マップに新しい呼び出し履歴が追加されます。

 ![次の呼び出し履歴でコードマップを更新](../debugger/media/debuggermap-addclearcallstack.png "DebuggerMap_AddClearCallStack")

## <a name="AddRelatedCode"></a>関連するコードをマップに追加する
 マップを作成できたところで、次の作業に進みます。 Visual C# .NET または Visual Basic .NET で作業している場合は、フィールド、プロパティ、およびその他のメソッドなどの項目を追加して、コードの動作を追跡します。

 メソッドのコード定義を表示するには、そのメソッドをダブルクリックするか、そのメソッドのショートカット メニューを使用します。 (キーボード: マップでメソッドを選択し、 **F12**キーを押します)

 ![コードマップのメソッドのコード定義へのジャンプ](../debugger/media/debuggermap-gotocodedefinition.png "DebuggerMap_GoToCodeDefinition")

 マップで追跡する項目を追加します。

 ![呼び出し履歴コードマップのメソッドにフィールドを表示する](../debugger/media/debuggermap-showfields.png "DebuggerMap_ShowFields")

> [!NOTE]
> 既定では、マップに項目を追加すると、クラス、名前空間、アセンブリなどの親グループのノードも追加されます。 これは便利ですが、マップのツールバーの **[親を含める]** ボタンを使用するか、項目を追加するときに**CTRL**キーを押して、この機能をオフにすることで、マップを単純にすることができます。

 ![呼び出し履歴コードマップのメソッドに関連するフィールド](../debugger/media/debuggermap-showedfields.png "DebuggerMap_ShowedFields")

 ここでは、同じフィールドを使用するメソッドを簡単に表示できます。 追加された最新の項目は緑色で表示されます。

 コードのさらに多くの項目を表示するには、マップの作成を続けます。

 ![フィールドを使用するメソッドの参照: 呼び出し履歴コードマップ](../debugger/media/debuggermap-findallreferences.png "DebuggerMap_FindAllReferences")

 ![呼び出し履歴コードマップのフィールドを使用するメソッド](../debugger/media/debuggermap-foundallreferences.png "DebuggerMap_FoundAllReferences")

## <a name="FindBugs"></a>マップを使用してバグを見つける
 コードの視覚化はバグをよりすばやく見つけるために役立ちます。 たとえば、描画プログラムのバグを調査しているとします。 直線を描画して元に戻そうとしても、別の直線を描画するまで何も起こりません。

 そのため、`clear`、`undo`、および `Repaint` メソッドにブレークポイントを設定し、デバッグを開始して、次のようなマップを作成します。

 ![別の呼び出し履歴をコードマップに追加する](../debugger/media/debuggermap-addpaintobjectcallstack.png "DebuggerMap_AddPaintObjectCallStack")

 マップ上のすべてのユーザー ジェスチャーが、`Repaint` を除いて、`undo` を呼び出していることがわかります。 この動作が原因で `undo` がすぐに実行されない可能性があります。

 バグを修正してプログラムの実行を続けると、マップに `undo` から `Repaint` への新しい呼び出しが追加されます。

 ![コードマップの呼び出し履歴に新しいメソッド呼び出しを追加します](../debugger/media/debuggermap-addnewcallforrepaint.png "DebuggerMap_AddNewCallForRepaint")

## <a name="QA"></a> Q & A

- **すべての呼び出しがマップに表示されるわけではありません。なぜでしょうか。**

   既定では、ユーザー自身のコードだけがマップに表示されます。 外部コードを表示するには、 **[呼び出し履歴]** ウィンドウで有効にします。

   ![[呼び出し履歴] ウィンドウを使用して外部コードを表示する](../debugger/media/debuggermap-callstackmenu.png "DebuggerMap_CallStackMenu")

   または、Visual Studio のデバッグオプションで **[マイコードのみを有効にする]** をオフにします。

   ![[オプション] ダイアログボックスを使用して外部コードを表示する](../debugger/media/debuggermap-debugoptions.png "DebuggerMap_DebugOptions")

- **マップを変更してもコードに影響はありますか。**

   マップを変更してもコードは何も影響を受けません。 マップでの名前変更、移動、削除は自由に行うことができます。

- **このメッセージの意味は、「図は古いバージョンのコードに基づいている可能性がある」ということです。**

   マップを最後に更新してからコードが変更されている可能性があります。 たとえば、マップ上の呼び出しがコードに存在しなくなった可能性があります。 メッセージを閉じてから、マップを再び更新する前にソリューションをリビルドしてみます。

- **マップのレイアウトを制御操作方法には**

   マップツールバーの **[レイアウト]** メニューを開きます。

  - 既定のレイアウトを変更します。

  - マップの自動調整を停止するには、[**デバッグ時に自動的にレイアウト**を無効にする] をオンにします。

  - 項目を追加するときにできるだけ少ない方法でマップを再配置するには、 **[インクリメンタルレイアウト]** をオフにします。

- **他のユーザーとマップを共有することはできますか。**

   マップをエクスポートし、Microsoft Outlook があれば、他のユーザーに送信できます。または、マップを独自のソリューションに保存し、Team Foundation バージョン管理にチェックインできます。

   ![呼び出し履歴コードマップを他のユーザーと共有する](../debugger/media/debuggermap-sharewithothers.png "DebuggerMap_ShareWithOthers")

- **新しい呼び出し履歴を自動的に追加しないようにマップを停止操作方法ますか?**

   [マップ] ツールバーの [![コードマップの呼び出し履歴を自動的に表示する] &#45; ](../debugger/media/debuggermap-automaticupdateicon.gif "DebuggerMap_AutomaticUpdateIcon")をクリックします。 現在の呼び出し履歴をマップに手動で追加するには、 **ctrl** + **Shift** +  **`** を押します。

   マップでは引き続き、デバッグ中にマップ上の既存の呼び出し履歴が強調表示されます。

- **項目のアイコンと矢印は何を意味するのでしょうか。**

   項目に関する詳細を取得するには、その項目の上にマウス ポインターを移動し、アイテムのヒントを確認します。 また、**凡例**を見て、各アイコンの意味を理解することもできます。

   ![呼び出し履歴コードマップのアイコンは何を意味するのでしょうか。](../debugger/media/debuggermap-showlegend.png "DebuggerMap_ShowLegend")

  参照:[コールスタックをマップ](#MapStack)する•[コードに関するメモを作成](#MakeNotes)する•[次の呼び出し履歴でマップを更新](#UpdateMap)する•[関連するコードをマップに追加する](#AddRelatedCode)•マップを[使用してバグを見つける](#FindBugs)

## <a name="see-also"></a>関連項目
 [ソリューション間の依存関係のマッピング](../modeling/map-dependencies-across-your-solutions.md)コードマップ[を使用してアプリケーションをデバッグする](../modeling/use-code-maps-to-debug-your-applications.md)コード[マップアナライザーを使用して潜在的な問題を検出](../modeling/find-potential-problems-using-code-map-analyzers.md)する[コードマップの参照および再配置](../modeling/browse-and-rearrange-code-maps.md)
