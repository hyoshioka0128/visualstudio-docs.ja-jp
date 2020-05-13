---
title: '[オプション]、[テキスト エディター]、[基本] (Visual Basic) | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Visual_Basic.Editor
- VS.ToolsOptionsPages.Text_Editor.Basic.Editor
- VS.ToolsOptionsPages.Visual_Basic_Editor.Editor
- VS.ToolsOptionsPages.Text_Editor.Basic.SimplifiedEditorPage
- VS.ToolsOptionsPages.Text_Editor.Basic
- VS.ToolsOptionsPages.Text_Editor.Basic.VB_Specific
helpviewer_keywords:
- Basic Text Editor Options dialog box
ms.assetid: 5a8cafca-f7b4-4a2d-92ce-6894a7673d00
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 1edb7ceae1ba187b01b92d64ca33d41d83364e72
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72662372"
---
# <a name="options-text-editor-basic-visual-basic"></a>[オプション]、[テキスト エディター]、[基本] (Visual Basic)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

**[オプション]** ( **[ツール]** メニュー) ダイアログ ボックスの **[テキスト エディター]** フォルダーにある **[Basic]** フォルダーの **[VB 固有]** プロパティ ページでは、次のプロパティを指定します。

 **[構造文の終端の自動挿入]** たとえば、プロシージャ宣言の最初の行として `Sub Main—` を入力し、Enter キーを押すと、対応する `End Sub` 行がテキスト エディターに追加されます。 同様に、[For](https://msdn.microsoft.com/library/f5fc0d51-67ce-4c36-9f09-31c9a91c94e9) ループを追加すると、対応する `Next` ステートメントがテキスト エディターに追加されます。 このオプションをオンにすると、コード エディターで自動的に End 構造が追加されます。

 **[コードの再フォーマット]** 必要に応じてコードの書式が再設定されます。 このオプションをオンにすると、コード エディターによって次の処理が行われます。

- コードを正しいタブ位置に揃える。

- キーワード、変数、およびオブジェクトの大文字と小文字の区別を修正する。

- `Then` ステートメントの `If...Then` が欠けていた場合に補う。

- 関数呼び出しにかっこを追加する。

- 文字列の右引用符が欠けていた場合に補う。

- 指数表記の書式を正す。

- 日付の書式を正す。

  **アウトラインモードを有効にする**コードエディターでファイルを開くと、アウトラインモードでドキュメントを表示できます。 詳細については、「[アウトライン](../../ide/outlining.md)」を参照してください。 このオプションをオンにすると、ファイルを開くときにアウトライン表示機能が有効になります。

  **インターフェイスと MustOverride メンバーの自動挿入**クラスの `Implements` ステートメントまたは `Inherits` ステートメントをコミットすると、実装またはオーバーライドする必要があるメンバーのプロトタイプがテキストエディターによってそれぞれ挿入されます。

  **プロシージャ行の区切り記号を表示する**テキストエディターは、プロシージャのスコープを視覚的に示します。 プロジェクトの .vb ソース ファイルで、次の表に示す場所に線が表示されます。

|.vb ソース ファイル内の場所|線が表示される場所の例|
|---------------------------------|------------------------------|
|ブロック宣言構造の後|-   クラス、構造体、モジュール、インターフェイス、または列挙型の最後<br />-   プロパティ、関数、または sub の後<br />-   プロパティの get 句と set 句の間は対象外|
|一連の単一行構造|-   import ステートメントの後、クラス ファイルの型定義の前<br />-   クラスで宣言されている変数の後、プロシージャの前|
|単一行宣言|-   Import ステートメント、Inherits ステートメント、変数宣言、イベント宣言、デリゲート宣言、および DLL の Declare ステートメントの後|

 **エラー修正候補を有効にする**テキストエディターでは、一般的なエラーの解決策を提案し、適切な修正を選択して、コードに適用することができます。

 **参照とキーワードの強調表示を有効にする**テキストエディターでは、`If..Then`、`While...End While`、`Try...Catch...Finally` などの句で、シンボルまたはすべてのキーワードのすべてのインスタンスを強調表示できます。 強調表示された参照間またはキーワード間を移動するには、Ctrl キーと Shift キーを押しながら下方向キーを押すか、Ctrl キーと Shift キーを押しながら上方向キーを押します。

## <a name="see-also"></a>関連項目
 [[全般]、[環境]、[オプション] ダイアログボックス](../../ide/reference/general-environment-options-dialog-box.md)[の [オプション]、[テキストエディター]、[すべての言語]、[タブ](../../ide/reference/options-text-editor-all-languages-tabs.md)]
