---
title: '[オプション]、[テキスト エディター]、[全般]'
ms.date: 01/18/2019
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor
- vs.toolsoptionspages.text_editor
- VS.ToolsOptionsPages.Text_Editor.CSharp.Formatting
- VS.ToolsOptionsPages.Text_Editor.CSharp.Outlining
- VS.ToolsOptionsPages.Text_Editor.General
- VS.ToolsOptionsPages.Text_Editor.PL/SQL
- VS.ToolsOptionsPages.Text_Editor.PL/SQL.General
- VS.ToolsOptionsPages.Text_Editor.Python
- VS.ToolsOptionsPages.Text_Editor.R
- VS.ToolsOptionsPages.Text_Editor.RDL_Expression.General
- VS.ToolsOptionsPages.Text_Editor.SQL
- VS.ToolsOptionsPages.Text_Editor.SQL.General
- VS.ToolsOptionsPages.Text_Editor.SQL_Script
- VS.ToolsOptionsPages.Text_Editor.SQL_Script.General
- VS.ToolsOptionsPages.Text_Editor.T-SQL
- VS.ToolsOptionsPages.Text_Editor.T-SQL.General
- VS.ToolsOptionsPages.Text_Editor.T-SQL7.General
- VS.ToolsOptionsPages.Text_Editor.T-SQL80
- VS.ToolsOptionsPages.Text_Editor.T-SQL80.General
helpviewer_keywords:
- Text Editor Options dialog box
- Code Editor
- Text Editor [Visual Studio]
- editors, global settings
ms.assetid: 4ac21e48-3243-4141-9058-7eaf12b3cde7
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ebe526bbac859777edb4c2c78c65a1cdbd27fc85
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75568413"
---
# <a name="options-dialog-box-text-editor--general"></a>[オプション] ダイアログ ボックス:[テキスト エディター] \> [全般]

このダイアログ ボックスでは、Visual Studio コード/テキスト エディターのグローバル設定を変更できます。 このダイアログ ボックスを表示するには、 **[ツール]** メニューの **[オプション]** を選択し、 **[テキスト エディター]** フォルダーを展開し、 **[全般]** を選択します。

## <a name="settings"></a>設定

### <a name="drag-and-drop-text-editing"></a>[ドラッグ アンド ドロップ編集]

選択すると、マウスでテキストを選択してドラッグし、現在の文書内や開いている他の文書内の別の場所に移動させることができます。

### <a name="automatic-delimiter-highlighting"></a>[区切り記号を自動強調表示する]

選択すると、パラメーターまたは項目/値の組を分ける区切り文字とそれに対応する括弧が強調表示されます。

### <a name="track-changes"></a>[変更履歴を記録する]

コード エディターが選択されているとき、マージンに黄色の縦線が表示され、ファイルが前回保存されてから変更されたコードに印を付けます。 変更を保存すると、縦線は緑色になります。

### <a name="auto-detect-utf-8-encoding-without-signature"></a>[シグネチャ (BOM) なしの UTF-8 エンコードを自動検出]

既定では、エディターはバイト オーダー マークまたは文字セット タグを探してエンコードを検出します。 現在の文書でいずれも見つからない場合、コード エディターはバイト順序をスキャンすることで、UTF-8 エンコードを自動検出します。 エンコードの自動検出を無効にするには、このオプションをオフにします。

### <a name="follow-project-coding-conventions"></a>プロジェクトのコーディング規則に従う

選択した場合、プロジェクトに指定されたコーディング規則によって、個人のプロジェクトで使用しているコーディング規則が上書きされます。

### <a name="enable-mouse-click-to-perform-go-to-definition"></a>マウス クリックを有効にして [定義へ移動] を実行する

選択した場合、**Ctrl** キーを押ながらマウスをクリックすると、マウス ポインターが要素に移動します。 これを行うと、選択した要素の定義に移動します。 **[修飾キーの使用]** ドロップダウンから、 **[Alt]** または **[Ctrl** + **Alt]** を選択することもできます。

コード エディターの現在の場所から移動せずに選択した要素の定義をウィンドウに表示するには、 **[ピーク ビューで定義を開く]** チェック ボックスをオンにします。

## <a name="display"></a>表示

### <a name="selection-margin"></a>[マージン]

選択すると、エディターのテキスト領域の左端に沿って縦の余白が表示されます。 この余白をクリックしてテキスト行全体を選択したり、クリックしてドラッグし、連続するテキスト行を選択したりできます。

|マージン オン|マージン オフ|
| - | - |
|![HTMLpageSelectionMarginOn スクリーンショット](../../ide/reference/media/vxselmaron.gif)|![HTMLpageSelectionMarginOff スクリーンショット](../../ide/reference/media/vxselmaroff.gif)|

### <a name="indicator-margin"></a>インジケーター マージン

選択すると、エディターのテキスト領域の左端の外に縦の余白が表示されます。 この余白をクリックすると、アイコンとテキストに関連付けられているヒントが表示されます。 たとえば、インジケーター マージンにブレークポイントやタスク一覧のショートカットが表示されます。 インジケーター マージンの情報は出力されません。

### <a name="highlight-current-line"></a>[現在の行を強調表示する]

選択すると、カーソルが置かれているコード行の周りに灰色のボックスが表示されます。

### <a name="show-structure-guide-lines"></a>構造のガイド線を表示する

選択した場合、構造化されたコード ブロックに合う垂直線がエディターに表示され、個々のコード ブロックを簡単に識別できます。

## <a name="see-also"></a>関連項目

- [[オプション]、[テキスト エディター]、[すべての言語]](../../ide/reference/options-text-editor-all-languages.md)
- [[オプション]、[テキスト エディター]、[すべての言語]、[タブ]](../../ide/reference/options-text-editor-all-languages-tabs.md)
- [[オプション]、[テキスト エディター]、[ファイル拡張子]](../../ide/reference/options-text-editor-file-extension.md)
- [キーボード ショートカットの識別とカスタマイズ](../../ide/identifying-and-customizing-keyboard-shortcuts-in-visual-studio.md)
- [エディターのカスタマイズ](../how-to-change-text-case-in-the-editor.md)
- [IntelliSense の使用](../../ide/using-intellisense.md)
