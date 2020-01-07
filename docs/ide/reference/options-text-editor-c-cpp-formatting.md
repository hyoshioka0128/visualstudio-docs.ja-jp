---
title: '[オプション]、[テキスト エディター]、[C/C++]、[書式設定]'
ms.date: 04/30/2018
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.C/C++.Formatting.General
- VS.ToolsOptionsPages.Text_Editor.C%2fC%2b%2b.Formatting.General
dev_langs:
- CPP
helpviewer_keywords:
- Text Editor Options dialog box, formatting
- ClangFormat
ms.assetid: cb6f1cbb-5305-48da-a8e8-33fd70775d46
author: mikeblome
ms.author: mblome
manager: markl
ms.workload:
- cplusplus
ms.openlocfilehash: b866d09dbd448950a641ebb59501c13c3bf35188
ms.sourcegitcommit: 85d66dc9fea3fa49018263064876b15aeb6f9584
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/24/2019
ms.locfileid: "68461804"
---
# <a name="options-text-editor-cc-formatting"></a>[オプション]、[テキスト エディター]、[C/C++]、[書式設定]

これらのプロパティ ページを使用し、C または C++ でプログラムを記述する際のコード エディターの既定の動作を変更します。

![C++ Formatting プロパティ ページ](media/cpp-formatting.png)

このページを表示するには、左ペインの **[オプション]** ダイアログ ボックスで、 **[テキスト エディター]** フォルダー、 **[C/C++]** を順に展開して、 **[書式設定]** をクリックします。

> [!NOTE]
> 次の手順で参照している Visual Studio ユーザー インターフェイス要素の一部は、お使いのコンピューターでは名前や場所が異なる場合があります。 これらの要素は、使用している Visual Studio のエディションや独自の設定によって決まります。 詳細については、「[Visual Studio IDE のカスタマイズ](../../ide/personalizing-the-visual-studio-ide.md)」を参照してください。

## <a name="general-page"></a>[全般] ページ

このページには、入力したステートメントやブロックの書式を設定するためのオプションがあります。

::: moniker range="vs-2017"

**Visual Studio 2017 バージョン 15.7 以降**:

::: moniker-end

このページにも、[ClangFormat](https://clang.llvm.org/docs/ClangFormat.html) バージョン 5.0 のサポートを構成するためのオプションがあります。 ClangFormat は、.clang-format または _clang-format ファイルで構成できる一連のルールに基づいてコードのスタイルや書式を簡単に設定できるユーティリティです。

### <a name="configuring-clangformat-options"></a>ClangFormat オプションを構成する

::: moniker range="vs-2017"

**Visual Studio 2017 バージョン 15.7 以降**:

::: moniker-end

ClangFormat のサポートは、既定で有効になっています。 一般的な書式設定規則であるLLVM、Google、Chromium、Mozilla、WebKit のうち、すべてのプロジェクトに適用するものを選択できます。 また、カスタム書式定義の .clang-format または _clang-format ファイルを作成できます。 そのようなファイルがプロジェクト フォルダーに置かれている場合、Visual Studio は、そのフォルダーとそのサブフォルダーのすべてのソース コード ファイルの書式設定にそのファイルを使用します。

既定では、Visual Studio は clangformat.exe をバックグラウンドで実行し、ユーザーが入力すると書式設定を適用します。 書式設定コマンド **Format Document (Ctrl + K、Ctrl + D)** または **Format Selection (Ctrl + K、Ctrl + F)** を手動で呼び出す場合にのみ、clangformat.exe を実行するように指定することもできます。

## <a name="indentation-new-lines-spacing-wrapping-pages"></a>インデント、改行、間隔、折り返しのページ

これらのページでは、さまざまな書式設定をカスタマイズできますが、ClangFormat が有効になっている場合は無視されます。

## <a name="see-also"></a>関連項目

- [[全般]、[環境]、[オプション] ダイアログ ボックス](../../ide/reference/general-environment-options-dialog-box.md)
- [IntelliSense の使用](../../ide/using-intellisense.md)
