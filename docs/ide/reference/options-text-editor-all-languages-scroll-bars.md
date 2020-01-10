---
title: '[オプション]、[テキスト エディター]、[すべての言語]、[スクロール バー]'
ms.date: 10/25/2018
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.All_Languages.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.Basic.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.CSharp.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.C%2FC%2B%2B.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.CoffeeScript.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.CSS.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.Dockerfile.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.F%2523.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.HQL.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.HTML.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.HTMLX.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.JavaScript.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.TypeScript.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.JSON.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.LESS.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.Plain_Text.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.ResJSON.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.SCSS.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.SQL_Server_Tools.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.StreamAnalytics.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.T-SQL90.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.U-SQL.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.XAML.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.XML.ScrollBars
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 54ce07537adc436f719de8596657d1367afcb87d
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75588799"
---
# <a name="options-text-editor-all-languages-scroll-bars"></a>[オプション]、[テキスト エディター]、[すべての言語]、[スクロール バー]
このダイアログ ボックスでは、コード エディターのスクロール バーの既定の動作を変更できます。 オプションを表示するには、 **[ツール]** メニューから **[オプション]** を選択します。 **[テキスト エディター]** フォルダー内で **[すべての言語]** サブフォルダーを展開し、 **[スクロール バー]** を選択します。

> [!CAUTION]
> このページから、すべての開発言語の既定のオプションが設定されます。 このダイアログでオプションをリセットすると、すべての言語のスクロール バー オプションがここで選択されているものにリセットされます。 1 つだけの言語のテキスト エディター オプションを変更にするには、その言語のサブフォルダーを展開し、そのオプション ページを選択します。

## <a name="show-horizontal-scroll-bar"></a>水平スクロール バーの表示

選択すると、水平スクロール バーが表示されます。このバーで左右にスクロールし、エディターの表示領域外の要素を表示できます。 水平スクロール バーが表示されない場合は、カーソル キーでスクロールできます。

## <a name="show-vertical-scroll-bar"></a>垂直スクロール バーの表示

選択すると、垂直スクロール バーが表示されます。このバーで上下にスクロールし、エディターの表示領域外の要素を表示できます。 縦のスクロール バーが利用できない場合、Page Up キー、Page Down キー、カーソル キーでスクロールできます。

## <a name="display"></a>表示

### <a name="show-annotations-over-vertical-scroll-bar"></a>垂直スクロール バーへのコメントの表示

垂直スクロール バーで次の注釈を表示するかどうかを選択します。

- 変更点
- マーク
- エラー
- キャレット位置

> [!TIP]
> **[マークの表示]** オプションには、ブレークポイントとブックマークが含まれています。

サイズの大きなコード ファイルを開き、ファイルの何か所かにあるテキストを置き換えて試してみてください。 スクロール バーに置き換えた結果が表示されるため、置き換えるべきでないものを置き換えた場合は変更を取り消すことができます。

コードを編集するときのさまざまな色と記号の意味については、[強化されたスクロール バー](https://blogs.msdn.microsoft.com/cdnstudents/2014/01/21/visual-studio-tips-and-tricks-enhanced-scroll-bar/)のブログ記事をご覧ください。

## <a name="behavior"></a>動作

スクロール バーには、バー モードとマップ モードの 2 つのモードがあります。

### <a name="use-bar-mode-for-vertical-scroll-bar"></a>垂直スクロール バーでのバー モードの使用

*バー モード*では、コメントのインジケーターがスクロール バーに表示されます。 スクロール バーをクリックすると、ページが上下にスクロールしますが、ファイル内のその位置にはジャンプしません。

### <a name="use-map-mode-for-vertical-scroll-bar"></a>垂直スクロール バーでのマップ モードの使用

*マップ モード*では、スクロール バーのある位置をクリックすると、1 ページのみ上下にスクロールするのではなく、ファイル内のその位置にカーソルがジャンプします。 コード行がスクロール バーに縮小表示されます。 **[ソースの概要]** で値を選択すると、マップの列幅を選択できます。 マップにポインターを置いたときにコードのより大きなプレビューを表示するには、 **[プレビュー ツール ヒントの表示]** オプションを選択します。 折りたたまれた部分は他と異なる影付きで表示され、ダブルクリックすると展開されます。

> [!TIP]
> **[ソースの概要]** を **[オフ]** に設定すると、マップ モードの縮小版のコード ビューをオフにすることができます。 **[プレビュー ツール ヒントの表示]** を選択すると、スクロール バーにポインターを置いたときにその場所のコードのプレビューが表示され、クリックすると、ファイルのその位置にカーソルがジャンプするようになります。

## <a name="see-also"></a>関連項目

- [方法: スクロール バーのカスタマイズ](../how-to-track-your-code-by-customizing-the-scrollbar.md)
