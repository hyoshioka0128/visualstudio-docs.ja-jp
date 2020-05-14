---
title: '[ドキュメント] ([オプション] ダイアログ ボックス - [環境]) | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- VS.Environment.Documents
- VS.ToolsOptionsPages.Environment.Documents
- VS.ToolsOptionsPag.Environment.Documents
helpviewer_keywords:
- Documents Environment Options dialog box
- defaults, directories
- error messages, customizing
- files [Visual Studio], default options
- files [Visual Basic], auto-loading modified
- windows, customizing environment
- in-memory editing
- folders [Visual Studio], specifying where Open File goes
- Open File dialog box
- windows, enabling re-use of current
- notifications, files changed
- files [Visual Studio], displaying in Solution Explorer
- default directories
- read-only files, editing
- Options dialog box, showing Miscellaneous Files
- directories [Visual Studio], IDE environment options
- Options dialog box, Documents page
- warnings, files changed
- Solution Explorer, displaying files in
ms.assetid: 4e3ccf1b-cd68-4db6-9470-710c911b47fc
caps.latest.revision: 25
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 705b1a5992d1a3e7931c316c713d46e7e8c7f72e
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72657768"
---
# <a name="documents-environment-options-dialog-box"></a>[ドキュメント] ([オプション] ダイアログ ボックス - [環境])
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

**[オプション]** ダイアログ ボックスのこのページを使用し、統合開発環境 (IDE) の文書表示を制御し、ドキュメントやファイルに対する外部変更を管理します。 このダイアログ ボックスにアクセスするには、 **[ツール]** メニューの **[オプション]** をクリックし、 **[環境]** ノードの **[ドキュメント]** を選択します。 **[ドキュメント]** が一覧に表示されない場合は、 **[オプション]** ダイアログ ボックスの **[すべての設定を表示]** を選択します。

> [!NOTE]
> 使用している設定またはエディションによっては、ダイアログ ボックスで使用可能なオプションや、メニュー コマンドの名前や位置がヘルプに記載されている内容と異なる場合があります。 設定を変更するには、 **[ツール]** メニューの **[設定のインポートとエクスポート]** をクリックします。 詳細については、「 [Visual Studio での開発設定のカスタマイズ](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)」を参照してください。

 **保存済みの現在のドキュメント ウィンドウを再利用** 選択すると、保存されている場合、現在のドキュメントを閉じ、同じウィンドウで新しいドキュメントを開きます。 現在のドキュメントが保存されていない場合、開いている状態が維持され、新しいドキュメントを別個のウィンドウで開きます。 このオプションが選択されていない場合、新しいドキュメントを常に別個のウィンドウで開きます。

 切り取りと貼り付けの操作を複数のドキュメントで行うことがあまりなく、自分の作業領域で、開いているドキュメントやウィンドウの数を最小限に抑える場合、このオプションをお試しください。

 **環境外でのファイルの変更を検出** このオプションを選択すると、開いているファイルが IDE の外部のエディターで変更された場合、直後にメッセージで通知されます。 このメッセージにより、ストレージからファイルを再読み込みできます。

 **保存する場合、変更を自動的に読み込む** **[環境外でのファイルの変更を検出]** を選択しているとき、IDE で開いているファイルが IDE の外部で変更されると、既定で、警告メッセージが生成されます。 このオプションを有効にすると、警告は表示されず、ドキュメントが IDE に再読み込みされ、外部の変更が反映されます。

 **読み取り専用ファイルの編集を有効にし、保存時に警告する** このオプションを有効にすると、読み取り専用ファイルを開き、編集できます。 完了時、変更の記録を保存する場合、 **[名前を付けて保存]** コマンドを利用し、新しいファイル名でファイルを保存する必要があります。

 **現在アクティブなドキュメントのディレクトリを使ってファイルを開く** このオプションを選択すると、 **[ファイルを開く]** ダイアログ ボックスにアクティブなドキュメントのディレクトリが表示されます。 このオプションを選択しない場合、 **[ファイルを開く]** ダイアログ ボックスには、ファイルを開くために前回利用されたディレクトリが表示されます。

 **読み込み時に行の終わりの整合性を確認する** このオプションを選択すると、エディターはファイルの行の終わりをスキャンし、終わりの書式設定に不整合が検出された場合、メッセージ ボックスを表示します。

 **全体的に元に戻す操作で編集したファイルが変更される場合、警告を表示** このオプションを選択すると、リファクタリング操作後に変更されたファイルで行われたリファクタリング変更を **[全体的に元に戻す]** コマンドでロールバックするときにメッセージ ボックスが表示されます。 ファイルをリファクタリング前の状態に戻すと、リファクタリング後にファイルに行った変更が破棄されることがあります。

 **その他のファイルをソリューション エクスプローラーに表示** このオプションを選択すると、 **[ソリューション エクスプローラー]** に **[その他のファイル]** ノードが表示されます。 その他のファイルとは、プロジェクトやソリューションに関連付けられていないファイルですが、利便性のために**ソリューション エクスプローラー**に表示できます。

> [!NOTE]
> このオプションを選択すると、アクティブな Web アプリケーションに含まれていない Web ドキュメントで、 **[ファイル]** メニューの **[ブラウザーで表示]** コマンドが有効になります。

 **その他のファイル プロジェクトに保存された \<** *n* **> 項目** **ソリューション エクスプローラー**の **[その他のファイル]** フォルダーに保存するファイルの数を指定します。 ファイルはエディターで開いていなくても一覧表示されます。 0 から 256 までの任意の整数を指定できます。 既定の数は 0 です。

 たとえば、このオプションを 5 に設定したとき、10 個のその他のファイルを開いている場合、10 個のファイルをすべて閉じたとき、最初の 5 個のファイルが **その他のファイル** フォルダーに引き続き表示されます。

 **コードページでデータが保存できない場合、Unicode でドキュメントを保存** このオプションを選択すると、選択したコードページと互換性のない情報を含むファイルが既定で Unicode として保存されます。

## <a name="see-also"></a>関連項目
 [[環境オプション] ダイアログボックス](../../ide/reference/environment-options-dialog-box.md)[その他のファイル](../../ide/reference/miscellaneous-files.md)[の検索と置換](../../ide/finding-and-replacing-text.md)
