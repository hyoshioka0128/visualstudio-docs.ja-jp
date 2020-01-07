---
title: コマンド
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Visual Studio, commands
- commands, Visual Studio
- command syntax
ms.assetid: 76ffa394-ee89-4629-aba9-1a62b72e6cc1
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3af3685288c00e27bb63cd45c682ab8b6354f4e5
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72622114"
---
# <a name="visual-studio-commands"></a>Visual Studio のコマンド

Visual Studio のコマンドは、 **[コマンド]** ウィンドウ、 **[イミディエイト]** ウィンドウ、または **[検索/コマンド]** ボックスで入力できます。 どの場合でも、不等号 (`>`) は後続の操作が検索またはデバッグではなくコマンドであることを示します。

コマンドの完全な一覧とその構文は、 **[ツール]**  >  **[オプション]**  >  **[環境]** の **[キーボード]** ページで確認できます。

IDE のローカライズ版では、IDE のネイティブ言語または英語のどちらでもコマンド名を入力できます。 たとえば、フランス語版 IDE では、「 `File.NewFile` 」または「 `Fichier.NouveauFichier` 」と入力して同じコマンドを実行できます。

多くのコマンドにエイリアスがあります。 コマンド エイリアスの一覧については、[コマンド エイリアス](../../ide/reference/visual-studio-command-aliases.md)に関する記事をご覧ください。 コマンドのキーボード ショートカットについては、「[Visual Studio の既定のキーボード ショートカット](../default-keyboard-shortcuts-in-visual-studio.md)」をご覧ください。

## <a name="escape-character"></a>エスケープ文字

Visual Studio のコマンドのエスケープ文字は、キャレット (^) です。 エスケープ文字は、その直後の文字を制御文字ではなくリテラル文字として解釈することを意味します。 したがって、引用符 (")、スペース、先頭のスラッシュ、カレット、その他の任意のリテラル文字をパラメーターまたはスイッチの値に直接埋め込むことができます。ただし、スイッチ名には埋め込むことができません。 次に例を示します。

```
>Edit.Find ^^t /regex
```

カレットは、引用符の前後のどちらに置かれた場合でも同じ働きをします。 行の最後の文字がカレットの場合は無視されます。

## <a name="commands-with-arguments"></a>引数を持つコマンド

次のコマンドは、引数またはスイッチを受け取ります。

| コマンド名 | 説明 |
| - | - |
| [既存項目の追加](../../ide/reference/add-existing-item-command.md) | 既存のファイルを現在のソリューションに追加して、そのファイルを開きます。 |
| [[既存プロジェクトの追加]](../../ide/reference/add-existing-project-command.md) | 既存のプロジェクトを現在のソリューションに追加します。 |
| [新しい項目の追加](../../ide/reference/add-new-item-command.md) | 新規ソリューションのアイテム (.htm、.css、.txt、フレームセットなど) を現在のソリューションに追加して、そのソリューションを開きます。 |
| [Alias](../../ide/reference/alias-command.md) | 完全なコマンド、完全なコマンドと引数、または他のエイリアスに対して新しいエイリアスを作成します。 |
| [[ステートメントの評価]](../../ide/reference/evaluate-statement-command.md) | 指定したステートメントを評価し、表示します。 |
| [[検索]](../../ide/reference/find-command.md) | **[検索と置換]** コントロールにあるオプションを使用してファイルを検索します。 |
| [フォルダーを指定して検索](../../ide/reference/find-in-files-command.md) | [[フォルダーを指定して検索]](../../ide/find-in-files.md) で使用可能なオプションのサブセットを使用してファイルを検索します。 |
| [移動先](../../ide/reference/go-to-command.md) | 指定した行にカーソルを移動します。 |
| [[呼び出し履歴の一覧表示]](../../ide/reference/list-call-stack-command.md) | 現在の呼び出し履歴を表示します。 |
| [[逆アセンブルの一覧表示]](../../ide/reference/list-disassembly-command.md) | デバッグ プロセスが開始され、エラーの処理方法を指定できるようになります。 |
| [[メモリの一覧表示]](../../ide/reference/list-memory-command.md) | 指定範囲のメモリの内容を表示します。 |
| [[モジュールの一覧]](../../ide/reference/list-modules-command.md) | 現在のプロセスのモジュールが一覧表示されます。 |
| [[レジスタの一覧]](../../ide/reference/list-registers-command.md) | レジスタの一覧を表示します。 |
| [[ソースの一覧]](../../ide/reference/list-source-command.md) | ソース コードの指定行が表示されます。 |
| [[スレッドの一覧表示]](../../ide/reference/list-threads-command.md) | 現在のプログラムのスレッド一覧を表示します。 |
| [[ログ コマンド ウィンドウ出力のログ]](../../ide/reference/log-command-window-output-command.md) | コマンド ウィンドウの入出力をすべてファイルにコピーします。 |
| [[新しいファイル]](../../ide/reference/new-file-command.md) | 新規ファイルを作成し、現在選択されているプロジェクトに追加します。 |
| [[ファイルを開く]](../../ide/reference/open-file-command.md) | 既存のファイルを開き、エディターを指定できます。 |
| [プロジェクトを開く](../../ide/reference/open-project-command.md) | 既存のプロジェクトを開き、現在のソリューションに追加できます。 |
| [印刷](../../ide/reference/print-command.md) | 式を評価し、結果または指定した文字列を表示します。 |
| [QuickWatch コマンド](../../ide/reference/quick-watch-command.md) | 選択または指定したテキストが **[クイック ウォッチ]** ダイアログ ボックスの **[式]** フィールドに表示されます。 |
| [置換](../../ide/reference/replace-command.md) | **[検索と置換]** コントロールにあるオプションを使用してファイル内の文字列を置換します。 |
| [[フォルダーを指定して置換]](../../ide/reference/replace-in-files-command.md) | [[フォルダーを指定して置換]](../../ide/replace-in-files.md) で使用可能なオプションのサブセットを使用してファイル内の文字列を置換します。 |
| [[現在のスタック フレームを設定する]](../../ide/reference/set-current-stack-frame-command.md) | 特定のスタック フレームを表示できます。 |
| [[現在のスレッドを設定する]](../../ide/reference/set-current-thread-command.md) | 特定のスレッドを表示できます。 |
| [[基数の設定]](../../ide/reference/set-radix-command.md) | 表示するバイト数を指定します。 |
| [Shell](../../ide/reference/shell-command.md) | コマンド プロンプトからコマンドを実行した場合と同様に、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 内からプログラムを起動します。 |
| [ShowWebBrowser コマンド](../../ide/reference/showwebbrowser-command.md) | 指定した URL を統合開発環境 (IDE: Integrated Development Environment) の内部または外部の Web ブラウザーのウィンドウに表示します。 |
| [[開始]](../../ide/reference/start-command.md) | デバッグ プロセスが開始され、エラーの処理方法を指定できるようになります。 |
| [パス](../../ide/reference/symbol-path-command.md) | デバッガーによってシンボルが検索されるディレクトリの一覧を設定します。 |
| [ブレークポイントの設定/解除](../../ide/reference/toggle-breakpoint-command.md) | ファイル内の現在位置で、現在の状態に基づいてブレークポイントのオン/オフを切り替えます。 |
| [Watch コマンド](../../ide/reference/watch-command.md) | 指定したインスタンスの **[ウォッチ]** ウィンドウを作成し、開きます。 |

## <a name="see-also"></a>関連項目

- [コマンド ウィンドウ](../../ide/reference/command-window.md)
- [[検索/コマンド] ボックス](../../ide/find-command-box.md)
- [Visual Studio コマンドのエイリアス](../../ide/reference/visual-studio-command-aliases.md)
