---
title: '[オプション]、[テキスト エディター]、[すべての言語]、[タブ]'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.All_Languages.Tabs
- VS.ToolsOptionsPages.Text_Editor.Basic.Tabs
- VS.ToolsOptionsPages.Text_Editor.CSharp.Tabs
- VS.ToolsOptionsPages.Text_Editor.C%2FC%2B%2B.Tabs
- VS.ToolsOptionsPages.Text_Editor.CoffeeScript.Tabs
- VS.ToolsOptionsPages.Text_Editor.CSS.Tabs
- VS.ToolsOptionsPages.Text_Editor.Dockerfile.Tabs
- VS.ToolsOptionsPages.Text_Editor.F%2523.Tabs
- VS.ToolsOptionsPages.Text_Editor.HQL.Tabs
- VS.ToolsOptionsPages.Text_Editor.HTML.Tabs
- VS.ToolsOptionsPages.Text_Editor.HTMLX.Tabs
- VS.ToolsOptionsPages.Text_Editor.JavaScript.Tabs
- VS.ToolsOptionsPages.Text_Editor.TypeScript.Tabs
- VS.ToolsOptionsPages.Text_Editor.JSON.Tabs
- VS.ToolsOptionsPages.Text_Editor.LESS.Tabs
- VS.ToolsOptionsPages.Text_Editor.Plain_Text.Tabs
- VS.ToolsOptionsPages.Text_Editor.ResJSON.Tabs
- VS.ToolsOptionsPages.Text_Editor.SCSS.Tabs
- VS.ToolsOptionsPages.Text_Editor.SQL_Server_Tools.Tabs
- VS.ToolsOptionsPages.Text_Editor.StreamAnalytics.Tabs
- VS.ToolsOptionsPages.Text_Editor.T-SQL90.Tabs
- VS.ToolsOptionsPages.Text_Editor.U-SQL.Tabs
- VS.ToolsOptionsPages.Text_Editor.XAML.Tabs
- VS.ToolsOptionsPages.Text_Editor.XML.Tabs
helpviewer_keywords:
- indents, Code Editor
- Code Editor, default behavior
- tabs, setting in Code Editor
- All Languages Text Editor Options dialog box
- editors, Code Editor
- Code Editor, indenting
- Code Editor, tabs
ms.assetid: 7e208e1d-5e3a-4bf7-a27b-4417e3e049c7
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0fc169960cf757e4e334d5f77b06ff70b0d6da7c
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75594748"
---
# <a name="options-text-editor-all-languages-tabs"></a>[オプション]、[テキスト エディター]、[すべての言語]、[タブ]

このダイアログ ボックスでは、コード エディターの既定の動作を変更できます。 設定は、HTML デザイナーのソース ビューなど、コード エディターに基づいて他のエディターにも適用されます。 オプションを表示するには、 **[ツール]** メニューから **[オプション]** を選択します。 **[テキスト エディター]** フォルダー内で **[すべての言語]** サブフォルダーを展開し、 **[タブ]** を選択します。

> [!CAUTION]
> このページから、すべての開発言語の既定のオプションが設定されます。 このダイアログでオプションをリセットすると、すべての言語のタブ オプションがここで選択されているものにリセットされます。 1 つだけの言語のテキスト エディター オプションを変更にするには、その言語のサブフォルダーを展開し、そのオプション ページを選択します。

特定のプログラミング言語のタブ オプション ページで異なる設定が選択されている場合、**インデント** オプションの違いに対して "個々のテキスト形式のインデントの設定が競合しています" というメッセージが表示され、**タブ** オプションの違いに対して "個々のテキスト形式のタブの設定が競合しています" というメッセージが表示されます。 たとえば、このリマインダーは、Visual Basic の場合、 **[スマート インデント]** が選択されているときに表示されます。Visual C++ の場合、 **[ブロック インデント]** が選択されているときに表示されます。

## <a name="indenting"></a>インデント

None

選択すると、新しい行に対するインデントは行われません。 カーソルは、新しい行の最初の列に移動します。

ブロック

選択すると、新しい行に自動的にインデントが行われます。 カーソルは、前の行と同じ開始位置に移動します。

[スマート]

選択すると、コードのコンテキストに合わせ、新しい行の位置が調整されます。他のコード書式設定や開発言語の IntelliSense 規則に基づきます。 このオプションは、一部の開発言語で使用できません。

たとえば、左中かっこ ( { ) とそれに対応する右中かっこ ( } ) は同じ位置に揃えられ、その間に記述された行は、中かっこの位置を起点としてタブ ストップが挿入され、自動的にインデントされます。

## <a name="tabs"></a>タブ

[タブ サイズ]

タブ ストップの間隔を空白文字数で設定します。 既定値は 4 スペースです。

[インデント サイズ]

自動インデントの幅を空白文字数で設定します。 既定値は 4 スペースです。 指定したサイズに合わせて、タブ文字、空白文字、またはその両方が挿入されます。

[空白の挿入]

選択した場合、インデント操作によって、TAB 文字ではなく空白文字だけが挿入されます。 たとえば、 **[インデント サイズ]** に 5 を設定した場合、Tab キーを押すか、 **[書式設定]** ツール バーの **[インデントを増やす]** をクリックするたびに 5 つの空白文字が挿入されます。

[タブの保持]

選択した場合、インデント操作によって、可能な限りの TAB 文字が挿入されます。 TAB 文字の長さは、 **[タブ サイズ]** ボックスで指定したスペースの数に相当します。 **[インデント サイズ]** 値が **[タブ サイズ]** 値の倍数ではない場合は、その差を埋めるために空白文字が挿入されます。

## <a name="see-also"></a>関連項目

- [[オプション]、[テキスト エディター]、[すべての言語]](../../ide/reference/options-text-editor-all-languages.md)
- [[全般]、[環境]、[オプション] ダイアログ ボックス](../../ide/reference/general-environment-options-dialog-box.md)
