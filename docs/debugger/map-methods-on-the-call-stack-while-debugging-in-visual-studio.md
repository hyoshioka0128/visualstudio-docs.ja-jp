---
title: 呼び出し履歴のビジュアル マップを作成する | Microsoft Docs
description: デバッグ中に呼び出し履歴を視覚的にトレースするためのコード マップを作成します。 コメントをマップに追加してコードの動作を追跡するため、バグの発見に重点を置くことができます。
ms.custom: SEO-VS-2020
ms.date: 11/26/2018
ms.topic: how-to
f1_keywords:
- vs.progression.debugwithcodemaps
dev_langs:
- CSharp
- VB
- FSharp
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
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 965232f56fcd2bf0d459910e983fb10dcca7f96d
ms.sourcegitcommit: 620d30c60da8f9805fce524fe4951cf40f28297d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/05/2021
ms.locfileid: "97903832"
---
# <a name="create-a-visual-map-of-the-call-stack-while-debugging-c-visual-basic-c-javascript"></a>デバッグ時に呼び出し履歴のビジュアル マップを作成する (C#、Visual Basic、C++、JavaScript)

デバッグ中に呼び出し履歴を視覚的にトレースするためのコード マップを作成します。 コメントをマップに追加することで、バグを見つけることに重点を置いてコードの動作を追跡できます。

チュートリアルについては、次のビデオをご覧ください。[ビデオ:コード マップ デバッガーの統合を使用して視覚的にデバッグする (Channel 9)](https://channel9.msdn.com/Series/Visual-Studio-2012-Premium-and-Ultimate-Overview/Visual-Studio-Ultimate-2012Debug-visually-with-Code-Map-debugger-integration)

コード マップで使用できるコマンドとアクションの詳細については、「[コード マップの参照および再配置](../modeling/browse-and-rearrange-code-maps.md)」を参照してください。

>[!IMPORTANT]
>コード マップは [Visual Studio Enterprise エディション](https://visualstudio.microsoft.com/downloads)でのみ作成できます。

コード マップを簡単に見てみましょう。

 ![コード マップの呼び出し履歴を使用したデバッグ](../debugger/media/debuggermap_overview.png "DebuggerMap_Overview")

## <a name="map-the-call-stack"></a><a name="MapStack"></a>呼び出し履歴でマップを作成する

1. Visual Studio Enterprise C#、Visual Basic、C++、または JavaScript プロジェクトでは、 **[デバッグ]**  >  **[デバッグの開始]** を選択するか、**F5** キーを押してデバッグを開始します。

1. アプリが中断モードになった後、または関数にステップインした後、 **[デバッグ]**  >  **[コード マップ]** を選択するか、**Ctrl**+**Shift**+ **`** キーを押します。

   現在の呼び出し履歴は新しいコード マップ上にオレンジ色で表示されます。

   ![コード マップの呼び出し履歴を確認する](../debugger/media/debuggermap_seeundocallstack.png "DebuggerMap_SeeUndoCallStack")

デバッグを続行すると、コード マップは自動的に更新されます。 マップ項目またはレイアウトを変更しても、コードに影響はありません。 マップでの名前変更、移動、削除は自由に行うことができます。

項目に関する詳細情報を取得するには、項目にカーソルを合わせて、項目のツールヒントを確認します。 ツールバーの **[凡例]** を選択すると、各アイコンの意味がわかります。

![コード マップの凡例](../debugger/media/debuggermap_showlegend.png "コード マップの凡例")

>[!NOTE]
>コード マップの上部に "**ダイアグラムは古いバージョンのコードに基づいている可能性があります**" というメッセージが表示される場合は、マップを最後に更新した後にコードが変更された可能性があることを意味します。 たとえば、マップ上の呼び出しがコードに存在しなくなった可能性があります。 メッセージを閉じてから、マップを再び更新する前にソリューションをリビルドしてみます。

## <a name="map-external-code"></a>外部コードをマップする

既定では、ユーザー自身のコードだけがマップに表示されます。 マップに外部コードを表示するには、次のようにします。

- **[呼び出し履歴]** ウィンドウを右クリックし、 **[外部コードの表示]** を選択します。

  ![[呼び出し履歴] ウィンドウを使用して外部コードを表示する](../debugger/media/debuggermap_callstackmenu.png "DebuggerMap_CallStackMenu")
- または、Visual Studio の **[ツール]** (または **[デバッグ]** ) で **[マイ コードのみを有効にする]** をオフにして、 **[オプション]**  >  **[デバッグ]** を選択します。

  ![[オプション] ダイアログ ボックスを使用して外部コードを表示する](../debugger/media/debuggermap_debugoptions.png "DebuggerMap_DebugOptions")

## <a name="control-the-maps-layout"></a>マップのレイアウトを制御する

マップのレイアウトを変更しても、コードに影響はありません。

マップのレイアウトを制御するには、マップ ツールバーの **[レイアウト]** メニューを選択します。

**[レイアウト]** メニューでは、次のことができます。

- 既定のレイアウトを変更します。
- **[デバッグ時に自動レイアウト]** をオフにして、マップの自動再配置を停止します。
- **[インクリメンタル レイアウト]** をオフにして、項目を追加するときのマップの再配置を最小限にします。

## <a name="make-notes-about-the-code"></a><a name="MakeNotes"></a>コードに関するコメントを追加する

コードの動作を追跡するためのコメントを追加することができます。

コメントを追加するには、コード マップを右クリックして **[編集]**  >  **[新しいコメント]** を選択し、コメントを入力します。

コメント内で新しい行を追加するには、**Shift**+**Enter** キーを押します。

 ![コード マップの呼び出し履歴にコメントを追加する](../debugger/media/debuggermap_addcomment.png "DebuggerMap_AddComment")

## <a name="update-the-map-with-the-next-call-stack"></a><a name="UpdateMap"></a>次の呼び出し履歴でマップを更新する

アプリを次のブレークポイントまで実行するか、関数にステップインすると、マップによって新しい呼び出し履歴が自動的に追加されます。

![次の呼び出し履歴でコード マップを更新する](../debugger/media/debuggermap_addclearcallstack.png "DebuggerMap_AddClearCallStack")

マップによって新しい呼び出し履歴が自動的に追加されないようにするには、コード マップ ツールバーの ![[コード マップにデバッガーの呼び出し履歴を自動的に表示]](../debugger/media/debuggermap_automaticupdateicon.gif "コード マップの呼び出し履歴を自動的に表示する") をオンにします。 マップには、引き続き既存の呼び出し履歴が強調表示されます。 マップに現在の呼び出し履歴を手動で追加するには、**Ctrl**+**Shift**+ **`** キーを押します。

## <a name="add-related-code-to-the-map"></a><a name="AddRelatedCode"></a>関連するコードをマップに追加する

C# または Visual Basic でマップを作成したので、フィールド、プロパティ、その他のメソッドなどの項目を追加して、コード内で起こっていることを追跡できます。

コード内のメソッドの定義に移動するには、マップ内のメソッドをダブルクリックするか、選択して **F12** キーを押すか、右クリックして **[定義に移動]** を選択します。

![コード マップのメソッドのコード定義に移動する](../debugger/media/debuggermap_gotocodedefinition.png "DebuggerMap_GoToCodeDefinition")

追跡する項目をマップに追加するには、メソッドを右クリックし、追跡する項目を選択します。追加された最新の項目は緑色で表示されます。

![呼び出し履歴コード マップのメソッドに関連するフィールド](../debugger/media/debuggermap_showedfields.png "DebuggerMap_ShowedFields")

>[!NOTE]
>既定では、マップに項目を追加すると、クラス、名前空間、アセンブリなどの親グループのノードも追加されます。 この機能をオフまたはオンにするには、コード マップ ツールバーの **[親を含める]** ボタンを選択するか、項目を追加するときに **Ctrl** キーを押します。

![呼び出し履歴コード マップのメソッドのフィールドを表示する](../debugger/media/debuggermap_showfields.png "DebuggerMap_ShowFields")

コードのさらに多くの項目を表示するには、マップの作成を続けます。

 ![フィールドを使用するメソッドを確認する: 呼び出し履歴コード マップ](../debugger/media/debuggermap_findallreferences.png "DebuggerMap_FindAllReferences")

 ![呼び出し履歴コード マップのフィールドを使用するメソッド](../debugger/media/debuggermap_foundallreferences.png "DebuggerMap_FoundAllReferences")

## <a name="find-bugs-using-the-map"></a><a name="FindBugs"></a>マップを使用してバグを見つける
 コードの視覚化はバグをよりすばやく見つけるために役立ちます。 たとえば、描画アプリのバグを調査しているとします。 直線を描画して元に戻そうとしても、別の直線を描画するまで何も起こりません。

 そのため、`clear`、`undo`、および `Repaint` メソッドにブレークポイントを設定し、デバッグを開始して、次のようなマップを作成します。

 ![コード マップに別の呼び出し履歴を追加する](../debugger/media/debuggermap_addpaintobjectcallstack.png "DebuggerMap_AddPaintObjectCallStack")

 マップ上のすべてのユーザー ジェスチャーが、`Repaint` を除いて、`undo` を呼び出していることがわかります。 これが原因で `undo` がすぐに動作しない可能性があります。

 バグを修正してアプリの実行を続けると、マップに `undo` から `Repaint` への新しい呼び出しが追加されます。

 ![コード マップの呼び出し履歴に新しいメソッド呼び出しを追加する](../debugger/media/debuggermap_addnewcallforrepaint.png "DebuggerMap_AddNewCallForRepaint")

## <a name="share-the-map-with-others"></a>他のユーザーとマップを共有する

マップをエクスポートし、Microsoft Outlook を使用して他のユーザーに送信し、ソリューションに保存して、バージョン コントロールにチェックインすることができます。

マップを共有または保存するには、コード マップ ツールバーの **[共有]** を使用します。

![呼び出し履歴コード マップを他のユーザーと共有](../debugger/media/debuggermap_sharewithothers.png "呼び出し履歴コード マップを他のユーザーと共有")

## <a name="see-also"></a>関連項目
[ソリューション間の依存関係をマップする](../modeling/map-dependencies-across-your-solutions.md)

[コード マップを使用してアプリケーションをデバッグする](../modeling/use-code-maps-to-debug-your-applications.md)

[コード マップ アナライザーを使用して潜在的な問題を検索する](../modeling/find-potential-problems-using-code-map-analyzers.md)

[コード マップの参照および再配置](../modeling/browse-and-rearrange-code-maps.md)
