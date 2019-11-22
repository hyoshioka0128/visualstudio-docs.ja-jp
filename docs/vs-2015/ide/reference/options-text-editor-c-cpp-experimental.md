---
title: '[オプション]、[テキスト エディター]、[C-C++]、[実験用] | Microsoft Docs'
ms.date: 11/15/2016
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.C/C++.Experimental
- VS.ToolsOptionsPages.Text_Editor.C%2FC%2B%2B.Experimental
- VS.ToolsOptionsPages.Text_Editor.C\C++.Experimental
ms.assetid: b9e9dda2-350c-460d-b368-37d6c5342eee
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 5979363f16f2e9d78a2f50ffbb6511d03146caaa
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74297861"
---
# <a name="options-text-editor-cc-experimental"></a>[オプション]、[テキスト エディター]、[C/C++]、[実験用]
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

これらのオプションを変更することによって、C または C++ でプログラミングを行うときに、IntelliSense に関連する動作と参照データベースを変更できます。

 このページを表示するには、左ウィンドウの **[オプション]** ダイアログ ボックスで、 **[テキスト エディター]** 、 **[C/C++]** を順に展開して、 **[実験用]** を選びます。

 これらの機能は、Visual Studio 2015 更新プログラム 1 RC のインストールで入手できます。

> [!NOTE]
> 次の手順で参照している Visual Studio ユーザー インターフェイス要素の一部は、お使いのコンピューターでは名前や場所が異なる場合があります。 これらの要素は、使用している Visual Studio のエディションや独自の設定によって決まります。 「[Visual Studio での開発設定のカスタマイズ](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)」を参照してください。

## <a name="browsingnavigation"></a>参照/ナビゲーション
 **Enable New Database Engine** This should automatically speed up database population and make all database operations faster (with no loss in accuracy) for operations such as **Go To Definition** and **Find All References**. (変更を適用するにはソリューションを閉じてもう一度開くだけです。Visual Studio を再起動する必要はありません。)

## <a name="intellisense"></a>IntelliSense
 **Member List Dot-To-Arrow** Replaces '.' with '->' when applicable for Member List.

## <a name="refactoring"></a>Refactoring
 **Enable Extract Function** Extract selected code to its own function and replace code with a call to the new function. この機能にアクセスするには、選んだコードを右クリックして **[クイック アクション]** を選ぶか、単に Ctrl キーを押しながらドット キーを押すだけです (Ctrl+.、既定のショートカット)。

 **Enable Change Signature** Add, reorder, and delete parameters of a function and propagate the changes to all call sites. この機能にアクセスするには、関数の任意の使用法を右クリックして **[クイック アクション]** を選ぶか、Ctrl キーを押しながらドット キーを押すだけです (Ctrl+.、既定のショートカット)。

## <a name="text-editor"></a>[テキスト エディター]
 **Enable Expand Scopes** If enabled, you can surround selected text with curly braces by typing '{' into the text editor.

 **Enable Expand Precedence** If enabled, you can surround selected text with parentheses by typing '(' into the text editor.

 Visual Studio ギャラリーのその他のテキスト エディター機能については、 [ここ](https://go.microsoft.com/fwlink/?LinkId=692016)の一覧をご覧ください。 例として、 [C++ Quick Fixes](https://visualstudiogallery.msdn.microsoft.com/be91feef-8dc3-4f7a-ac9f-f34e7ca5918f)があります。これは、次をサポートします。

- **不足している #include の追加** -コード内の不明なシンボルについて関連する #include を提案します

- **名前空間/完全修飾シンボルの使用を追加** - 前の項目と同様ですが、名前空間に機能します。

- **不足しているセミコロンの追加**

- **MSDN ヘルプ** - MSDN を検索して、エラー メッセージを調べます

  波線の上にカーソルを合わせて電球マークを表示させるか、Ctrl キーを押しながらドットを押すだけです (Ctrl+.、既定のキーボード ショートカット)。 キーボード ショートカットでは、キャレットを特定のエラーやトークンの位置に置く必要はありません。エラーが出た同じ行にカーソルがあれば、行の上の何らかのものに対して解決策が提示されます。

## <a name="see-also"></a>参照
 [Setting Language-Specific Editor Options](../../ide/reference/setting-language-specific-editor-options.md) [Refactoring in C++ (VC Blog)](https://devblogs.microsoft.com/cppblog/all-about-c-refactoring-in-visual-studio-2015-preview/)
