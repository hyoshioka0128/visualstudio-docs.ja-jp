---
title: '[オプション]、[テキスト エディター]、[すべての言語]、[タブ] | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.ResJSON.Tabs
- VS.ToolsOptionsPages.Text_Editor.JavaScript.Tabs
- VS.ToolsOptionsPages.Text_Editor.All_Languages.Tabs
helpviewer_keywords:
- indents, Code Editor
- Code Editor, default behavior
- tabs, setting in Code Editor
- All Languages Text Editor Options dialog box
- editors, Code Editor
- Code Editor, indenting
- Code Editor, tabs
ms.assetid: 7e208e1d-5e3a-4bf7-a27b-4417e3e049c7
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 4cb670ab52e321f15c5b009c66ca40623409f10a
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72662383"
---
# <a name="options-text-editor-all-languages-tabs"></a>[オプション]、[テキスト エディター]、[すべての言語]、[タブ]
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

このダイアログ ボックスでは、コード エディターの既定の動作を変更できます。 設定は、HTML デザイナーのソース ビューなど、コード エディターに基づいて他のエディターにも適用されます。 オプションを表示するには、**[ツール]** メニューから **[オプション]** を選択します。 **[テキスト エディター]** フォルダー内で **[すべての言語]** サブフォルダーを展開し、**[タブ]** を選択します。

> [!CAUTION]
> このページから、すべての開発言語の既定のオプションが設定されます。 このダイアログでオプションをリセットすると、すべての言語のタブ オプションがここで選択されているものにリセットされます。 1 つだけの言語のテキスト エディター オプションを変更にするには、その言語のサブフォルダーを展開し、そのオプション ページを選択します。

 特定のプログラミング言語のタブ オプション ページで異なる設定が選択されている場合、**インデント** オプションの違いに対して "個々のテキスト形式のインデントの設定が競合しています" というメッセージが表示され、**タブ** オプションの違いに対して "個々のテキスト形式のタブの設定が競合しています" というメッセージが表示されます。 たとえば、このリマインダーは、Visual Basic の場合、**[スマート インデント]** が選択されているときに表示されます。Visual C++ の場合、**[ブロック インデント]** が選択されているときに表示されます。

> [!NOTE]
> 実際に画面に表示されるダイアログ ボックスとメニュー コマンドは、アクティブな設定またはエディションによっては、ヘルプの説明と異なる場合があります。 設定を変更するには、 **[ツール]** メニューの **[設定のインポートとエクスポート]** をクリックします。 詳細については、「 [Visual Studio での開発設定のカスタマイズ](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)」を参照してください。

## <a name="indenting"></a>インデント
 選択されていない場合、新しい行はインデントされません。 カーソルは、新しい行の最初の列に移動します。

 [ブロック] を選択すると、新しい行が自動的にインデントされます。 カーソルは、前の行と同じ開始位置に移動します。

 スマートの方を選択すると、コードのコンテキストに合わせ、新しい行の位置が調整されます。他のコード書式設定や開発言語の IntelliSense 規則に基づきます。 このオプションは、一部の開発言語で使用できません。

 たとえば、左中かっこ ( { ) とそれに対応する右中かっこ ( } ) は同じ位置に揃えられ、その間に記述された行は、中かっこの位置を起点としてタブ ストップが挿入され、自動的にインデントされます。

## <a name="tabs"></a>タブ
 [タブサイズ] タブストップ間の間隔をスペース単位で設定します。 既定値は 4 スペースです。

 インデントサイズ自動インデントのサイズをスペース単位で設定します。 既定値は 4 スペースです。 指定したサイズに合わせて、タブ文字、空白文字、またはその両方が挿入されます。

 [スペースの挿入] 選択した場合、インデント操作では、タブ文字ではなく空白文字のみを挿入します。 たとえば、**[インデント サイズ]** に 5 を設定した場合、Tab キーを押すか、**[書式設定]** ツール バーの **[インデントを増やす]** をクリックするたびに 5 つの空白文字が挿入されます。

 タブを選択したままにすると、インデント操作では可能な限り多くのタブ文字が挿入されます。 TAB 文字の長さは、**[タブ サイズ]** ボックスで指定したスペースの数に相当します。 **[インデント サイズ]** 値が **[タブ サイズ]** 値の倍数ではない場合は、その差を埋めるために空白文字が挿入されます。

## <a name="see-also"></a>関連項目
 [オプション] ([[テキストエディター](../../ide/reference/options-text-editor-all-languages.md) ]/ [[全般] ([オプション] ダイアログボックス-[環境](../../ide/reference/general-environment-options-dialog-box.md)])
