---
title: '[オプション]、[テキスト エディター]、[C/C++]、[表示]'
ms.date: 10/29/2018
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.C/C++.View
- VS.ToolsOptionsPages.Text_Editor.C%2FC%2B%2B.View
- VS.ToolsOptionsPages.Text_Editor.C\C++.View
author: corob-msft
ms.author: corob
manager: markl
ms.workload:
- cplusplus
ms.openlocfilehash: 95963245b15828f374e9812a9bb09d015b21a94b
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "77278694"
---
# <a name="options-text-editor-cc-view"></a>[オプション]、[テキスト エディター]、[C/C++]、[表示]

これらのプロパティ ページを使用し、C または C++ でプログラムを記述する際のコード エディターの既定の動作を変更します。

このプロパティ ページにアクセスするには、 **[ツール]**  >  **[オプション]** を選択し、 **[テキスト エディター]** 、 **[C/C++]** を展開してから、 **[表示]** を選択します。

## <a name="code-squiggles"></a>コードの波線

以下の設定を有効または無効にして、C および C++ のコードの波線をテキスト エディターで処理する方法を管理します。

- **スキップされた閲覧領域内のマクロ** - 閲覧データベースでスキップされた領域内のマクロを強調表示する方法を定義します (定義にかっこが含まれるマクロなど)。

- **constexpr に変換可能なマクロ** - `constexpr` 定義に変換できるマクロ定義を強調表示する方法を定義します。

## <a name="inactive-code"></a>[アクティブでないコード]

- **アクティブでないブロックの表示** - プリプロセッサのアクティブでないブロックが異なる色で表示されます。

- **アクティブでないコードの不透明度の無効化** - 不透明ではなく純色が、アクティブでないコード ブロックに使用されます。

- **アクティブでないコードの不透明度** - アクティブでないコード ブロックの不透明度の割合です。

## <a name="miscellaneous"></a>その他

- **コメント タスクの列挙** - 開いているソース ファイルで VS トークンをスキャンし、[タスク一覧] ウィンドウで報告します。

- **一致するトークンの強調表示** - カーソルが置かれている場所と一致する、囲んでいる中かっこまたは構文を強調表示します。

## <a name="outlining"></a>[アウトライン]

- **アウトラインの有効化** - ファイルが開いたときにアウトライン モードに入ります。

- **Outline Pragma Regions (プラグマ領域のアウトライン化)** - `#pragma` 領域ブロックを自動的にアウトライン化します。

- **Outline Statement Blocks (ステートメント ブロックのアウトライン化)** - ステートメント ブロックを自動的にアウトライン化します。

## <a name="see-also"></a>参照

- [言語固有のエディター オプションの設定](../../ide/reference/setting-language-specific-editor-options.md)
- [C++ でのリファクタリング (VC のブログ)](https://devblogs.microsoft.com/cppblog/all-about-c-refactoring-in-visual-studio-2015-preview/)
