---
title: '[オプション]、[テキスト エディター]、[基本] (VB)、[詳細]'
ms.date: 01/16/2019
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Visual_Basic.Editor
- VS.ToolsOptionsPages.Text_Editor.Basic.Editor
- VS.ToolsOptionsPages.Visual_Basic_Editor.Editor
- VS.ToolsOptionsPages.Text_Editor.Basic.SimplifiedEditorPage
- VS.ToolsOptionsPages.Text_Editor.Basic
- VS.ToolsOptionsPages.Text_Editor.Basic.Advanced
- VS.ToolsOptionsPages.Text_Editor.Basic.VB_Specific
helpviewer_keywords:
- Basic Text Editor Options dialog box
ms.assetid: 5a8cafca-f7b4-4a2d-92ce-6894a7673d00
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 562358ca90e223a07926aaa383ded41a5f7557cc
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "79431476"
---
# <a name="options-text-editor-basic-visual-basic-advanced"></a>[オプション]、[テキスト エディター]、[基本] (Visual Basic)、[詳細]
**[オプション]** ( **[ツール]** メニュー) ダイアログ ボックスの **[テキスト エディター]** フォルダーにある **[Basic]** フォルダーの **[VB 固有]** プロパティ ページでは、次のプロパティを指定します。

## <a name="analysis"></a>分析

- ライブ コード分析またはバックグラウンド分析スコープ

   マネージド コードのバックグラウンド分析スコープを構成します。 詳細については、[方法: マネージド コードのライブ コード分析スコープを構成する](../../code-quality/configure-live-code-analysis-scope-managed-code.md)」を参照してください。

## <a name="using-directives"></a>Using ディレクティブ

- using を並べ替える際に、'System' ディレクティブを先頭に配置する

   選択した場合、右クリック メニューの **[using の削除と並べ替え]** コマンドによって `using` ディレクティブが並べ替えられ、'System' 名前空間が一覧の先頭に置かれます。

- ディレクティブ グループを使用して分離します

   選択した場合、右クリック メニューの **[using の削除と並べ替え]** コマンドによって、同じルート名前空間を持つディレクティブのグループの間に空の行を挿入することで、`using` ディレクティブが分離されます。

- 参照アセンブリの型に using を提案する
- NuGet パッケージの型に using を提案する

   これらのオプションを選択した場合、[クイック アクション](../quick-actions.md)を使用して NuGet パッケージをインストールし、参照されていない型の `using` ディレクティブを追加できます。

   ![Visual Studio に NuGet パッケージをインストールするためのクイック アクション](media/nuget-lightbulb.png)

## <a name="highlighting"></a>強調表示

 **[参照とキーワードの強調表示を有効にする]**

テキスト エディターで、すべてのシンボルのインスタンスまたは `If..Then`、`While...End While`、`Try...Catch...Finally` などの 句のすべてのキーワードを強調表示できます。 強調表示された参照間またはキーワード間を移動するには、**Ctrl** + **Shift** + **下方向キー**を押すか、**Ctrl** + **Shift** + **上方向キー**を押します。

## <a name="outlining"></a>アウトライン

**[アウトライン モードを有効にする]**

ファイルをコード エディターで開くときに、ドキュメントをアウトライン モードで表示できます。 詳細については、「[アウトライン](../../ide/outlining.md)」を参照してください。 このオプションをオンにすると、ファイルを開くときにアウトライン表示機能が有効になります。

**[プロシージャ行の区切り文字を表示する]**

テキスト エディターに、プロシージャのスコープが表示されます。 プロジェクトの *.vb* ソース ファイルで、次の表に示す場所に線が表示されます。

|.vb ソース ファイル内の場所|線が表示される場所の例|
|---------------------------------|------------------------------|
|ブロック宣言構造の後|-   クラス、構造体、モジュール、インターフェイス、または列挙型の最後<br />-   プロパティ、関数、または sub の後<br />-   プロパティの get 句と set 句の間は対象外|
|一連の単一行構造|-   import ステートメントの後、クラス ファイルの型定義の前<br />-   クラスで宣言されている変数の後、プロシージャの前|
|単一行宣言|-   Import ステートメント、Inherits ステートメント、変数宣言、イベント宣言、デリゲート宣言、および DLL の Declare ステートメントの後|

## <a name="block-structure-guides"></a>ブロック構造のガイド

選択した場合、構造化されたコード ブロックに合う垂直線がエディターに表示され、個々のコード ブロックを簡単に識別できます。 たとえば、`Sub` ステートメントの `Sub` と `EndSub` の間に線が表示されます。

## <a name="editor-help"></a>エディターのヘルプ

**[コードの再フォーマット]** 必要に応じてコードの書式が再設定されます。 このオプションをオンにすると、コード エディターによって次の処理が行われます。

- コードを正しいタブ位置に揃える。

- キーワード、変数、およびオブジェクトの大文字と小文字の区別を修正する。

- `Then` ステートメントの `If...Then` が欠けていた場合に補う。

- 関数呼び出しにかっこを追加する。

- 文字列の右引用符が欠けていた場合に補う。

- 指数表記の書式を正す。

- 日付の書式を正す。

**[End コンストラクトの自動挿入]**

たとえば、プロシージャ宣言の最初の行として `Sub Main` を入力して **Enter** キーを押すと、対応する `End Sub` 行がテキスト エディターに追加されます。 同様に、[For](/dotnet/visual-basic/language-reference/statements/for-next-statement) ループを追加すると、対応する `Next` ステートメントがテキスト エディターに追加されます。 このオプションをオンにすると、コード エディターで自動的に End 構造が追加されます。

**[Interface と MustOverride メンバーの自動挿入]**

クラスの `Implements` ステートメントまたは `Inherits` ステートメントをコミットすると、実装またはオーバーライドする必要があるメンバーのそれぞれのプロトタイプがテキスト エディターに自動的に挿入されます。

**[エラー修正候補を有効にする]**

一般的なエラーの解決方法がテキスト エディターに表示され、適切な修正方法を選択できます。修正方法を選択するとコードに適用されます。

## <a name="see-also"></a>関連項目

- [[全般]、[環境]、[オプション] ダイアログ ボックス](../../ide/reference/general-environment-options-dialog-box.md)
- [[オプション]、[テキスト エディター]、[すべての言語]、[タブ]](../../ide/reference/options-text-editor-all-languages-tabs.md)
