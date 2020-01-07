---
title: '[オプション]、[テキスト エディター]、[全般] | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- VS.TOOLSOPTIONSPAGES.TEXT_EDITOR.SQL_SERVER_TOOLS.GENERAL
- VS.ToolsOptionsPages.Text_Editor.All_Languages.General
- VS.ToolsOptionsPages.Text_Editor.RDL_Expression.General
- VS.ToolsOptionsPages.Text_Editor.SQL.General
- vs.toolsoptionspages.text_editor
- VS.ToolsOptionsPages.Text_Editor.XML.General
- VS.ToolsOptionsPages.Text_Editor.T-SQL80.General
- VS.ToolsOptionsPages.Text_Editor.CSS
- VS.ToolsOptionsPages.Text_Editor.Plain_Text.General
- VS.ToolsOptionsPages.Text_Editor.Visual_JSharp.General
- VS.ToolsOptionsPages.Text_Editor.SQL_Script.General
- VS.ToolsOptionsPages.Text_Editor.CSharp.General
- VS.ToolsOptionsPages.Text_Editor.All_Languages
- VS.ToolsOptionsPages.Text_Editor.T-SQL7.General
- VS.ToolsOptionsPages.Text_Editor.Basic.General
- VS.ToolsOptionsPages.Text_Editor.T-SQL.General
- vs.toolsoptionspages.text_editor.visual_jsharp
- VS.ToolsOptionsPages.Text_Editor.F#.Tabs
- VS.ToolsOptionsPages.Text_Editor.F#
- VS.ToolsOptionsPages.Text_Editor.PL/SQL.General
- VS.ToolsOptionsPages.Text_Editor.C/C++.General
- VS.ToolsOptionsPages.Text_Editor.Plain_Text
- VS.ToolsOptionsPages.Text_Editor.HTML
- VS.ToolsOptionsPages.Text_Editor.XAML.General
- VS.ToolsOptionsPages.Text_Editor
- VS.ToolsOptionsPages.Text_Editor.F#.General
- VS.ToolsOptionsPages.Text_Editor.XOML.General
- VS.ToolsOptionsPages.Text_Editor.SQL
- vs.toolsoptionspages.text_editor.c/c++
- VS.ToolsOptionsPages.Text_Editor.SQL_Script
- VS.ToolsOptionsPages.Text_Editor.T-SQL90.General
- VS.ToolsOptionsPages.Text_Editor.General
- VS.ToolsOptionsPages.Text_Editor.CSharp
helpviewer_keywords:
- Text Editor Options dialog box
- Code Editor
- Text Editor [Visual Studio]
- editors, global settings
ms.assetid: 4ac21e48-3243-4141-9058-7eaf12b3cde7
caps.latest.revision: 34
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: fa81b08d6e375da4ad67b2e6eec32f244a779408
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72662263"
---
# <a name="options-text-editor-general"></a>[オプション]、[テキスト エディター]、[全般]
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

このダイアログ ボックスでは、[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] コード/テキスト エディターのグローバル設定を変更できます。 このダイアログ ボックスを表示するには、 **[ツール]** メニューの **[オプション]** をクリックし、 **[テキスト エディター]** フォルダーを展開し、 **[全般]** をクリックします。

> [!NOTE]
> 実際に画面に表示されるダイアログ ボックスとメニュー コマンドは、アクティブな設定またはエディションによっては、ヘルプの説明と異なる場合があります。 設定を変更するには、 **[ツール]** メニューの **[設定のインポートとエクスポート]** をクリックします。 詳細については、「 [Visual Studio での開発設定のカスタマイズ](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)」を参照してください。

## <a name="settings"></a>設定
 ドラッグアンドドロップによるテキスト編集を選択すると、テキストを選択して、現在のドキュメントまたは開いている他のドキュメント内の別の場所にドラッグすることによってテキストを移動できます。

 選択した場合に自動的に区切り記号を強調表示すると、パラメーターまたは項目と値のペアを区切る区切り文字と、一致するかっこが強調表示されます。

 [変更の追跡] コードエディターが選択されている場合は、ファイルが最後に保存されてから変更されたコードをマークするために、選択余白に垂直の黄色の線が表示されます。 変更を保存すると、縦線は緑色になります。

 既定では、署名なしの UTF-8 エンコードが自動的に検出されます。エディターは、バイト順マークまたは文字セットタグを検索することによってエンコードを検出します。 現在の文書でいずれも見つからない場合、コード エディターはバイト順序をスキャンし、UTF-8 エンコードを自動検出します。 エンコードの自動検出を無効にするには、このオプションをオフにします。

## <a name="display"></a>表示
 [選択範囲] 選択すると、エディターのテキスト領域の左端に沿った縦方向の余白が表示されます。 この余白をクリックしてテキスト行全体を選択したり、クリックしてドラッグし、連続するテキスト行を選択したりできます。

|マージン オン|マージン オフ|
|-------------------------|--------------------------|
|![HTMLpageSelectionMarginOn のスクリーンショット](../../ide/reference/media/vxselmaron.gif "|::ref1::|")|![HTMLpageSelectionMarginOff のスクリーンショット](../../ide/reference/media/vxselmaroff.gif "|::ref2::|")|

 [インジケーターの余白] 選択すると、エディターのテキスト領域の左端の外側に垂直方向の余白が表示されます。 この余白をクリックすると、アイコンとテキストに関連付けられているヒントが表示されます。 たとえば、インジケーター マージンにブレークポイントやタスク一覧のショートカットが表示されます。 インジケーター マージンの情報は印刷されません。

 垂直スクロールバーを選択すると、垂直スクロールバーが表示されます。このスクロールバーを上下にスクロールして、エディターの表示領域の外側にある要素を表示することができます。 縦のスクロール バーが利用できない場合、Page Up キー、Page Down キー、カーソル キーでスクロールできます。

 水平スクロールバー選択すると、水平スクロールバーが表示されます。このスクロールバーを使用すると、エディターの表示領域の外側にある要素を表示できます。 水平スクロール バーが表示されない場合は、カーソル キーでスクロールできます。

 選択したときに現在の行を強調表示すると、カーソルが置かれているコード行の周りに灰色のボックスが表示されます。

## <a name="see-also"></a>関連項目
 [[オプション]、[テキストエディター]、[すべての言語 ](../../ide/reference/options-text-editor-all-languages.md) [Options]、[テキストエディター]、[すべての言語]、[タブ ](../../ide/reference/options-text-editor-all-languages-tabs.md) [Options]、[テキストエディター]、[ファイル拡張子 ](../../ide/reference/options-text-editor-file-extension.md) [Identifying]、[キーボードショートカットのカスタマイズ] ](../../ide/identifying-and-customizing-keyboard-shortcuts-in-visual-studio.md) エディター [Customizing](../../ide/customizing-the-editor.md) [Using IntelliSense](../../ide/using-intellisense.md)
