---
title: '[ドキュメント] ([オプション] ダイアログ ボックス - [環境])'
description: '[ドキュメント] セクションの [環境] ページを使用して、IDE でのドキュメントの表示を制御し、ドキュメントやファイルに対する外部変更を管理する方法について説明します。'
ms.custom: SEO-VS-2020
ms.date: 03/28/2019
ms.topic: reference
f1_keywords:
- VS.Environment.Documents
- VS.ToolsOptionsPages.Environment.Documents
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
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 28b0e7920aca2ae8b789a37fad25509dbb8b4d7a
ms.sourcegitcommit: 2244665d5a0e22d12dd976417f2a782e68684705
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2020
ms.locfileid: "96305481"
---
# <a name="options-dialog-box-environment--documents"></a>[オプション] ダイアログ ボックス:[環境] \> [ドキュメント]

**[オプション]** ダイアログ ボックスのこのページを使用し、統合開発環境 (IDE) の文書表示を制御し、ドキュメントやファイルに対する外部変更を管理します。 このダイアログ ボックスにアクセスするには、**[ツール]** メニューの **[オプション]** をクリックし、**[環境]** > **[ドキュメント]** を選択します。

**環境外でのファイルの変更を検出**

このオプションを選択すると、開いているファイルが IDE の外部のエディターで変更された場合、直後にメッセージで通知されます。 このメッセージにより、ストレージからファイルを再読み込みできます。

**保存されていない変更がない限り、変更されたファイルを再読み込みする**

**[環境外でのファイルの変更を検出]** を選択しているとき、IDE で開いているファイルが IDE の外部で変更されると、既定で、警告メッセージが生成されます。 このオプションを有効にすると、警告は表示されず、ドキュメントが IDE に再読み込みされ、外部の変更が反映されます。

**読み取り専用ファイルの編集を有効にし、保存時に警告する**

このオプションを有効にすると、読み取り専用ファイルを開き、編集できます。 完了時、変更の記録を保存する場合、**[名前を付けて保存]** コマンドを利用し、新しいファイル名でファイルを保存する必要があります。

**現在アクティブなドキュメントのディレクトリを使ってファイルを開く**

このオプションを選択すると、**[ファイルを開く]** ダイアログ ボックスにアクティブなドキュメントのディレクトリが表示されます。 このオプションを選択しない場合、**[ファイルを開く]** ダイアログ ボックスには、ファイルを開くために前回利用されたディレクトリが表示されます。

**読み込み時に行の終わりの整合性を確認する**

このオプションを選択すると、エディターはファイルの行の終わりをスキャンし、終わりの書式設定に不整合が検出された場合、メッセージ ボックスを表示します。

**全体的に元に戻す操作で編集したファイルが変更される場合、警告を表示**

このオプションを選択すると、リファクタリング操作後に変更されたファイルで行われたリファクタリング変更を **[全体的に元に戻す]** コマンドでロールバックするときにメッセージ ボックスが表示されます。 ファイルをリファクタリング前の状態に戻すと、リファクタリング後にファイルに行った変更が破棄されることがあります。

**その他のファイルをソリューション エクスプローラーに表示**

このオプションを選択すると、**[ソリューション エクスプローラー]** に **[その他のファイル]** ノードが表示されます。 その他のファイルとは、プロジェクトやソリューションに関連付けられていないファイルですが、利便性のために **ソリューション エクスプローラー** に表示できます。

> [!NOTE]
> このオプションを選択すると、アクティブな Web アプリケーションに含まれていない Web ドキュメントで、 **[ファイル]** メニューの **[ブラウザーで表示]** コマンドが有効になります。

**その他のファイル プロジェクトに保存された項目**

**ソリューション エクスプローラー** の **その他のファイル** フォルダーに保存するファイルの数を指定します。 ファイルはエディターで開いていなくても一覧表示されます。 0 から 256 までの任意の整数を指定できます。 既定の数は 0 です。

たとえば、このオプションを 5 に設定したとき、10 個のその他のファイルを開いている場合、10 個のファイルをすべて閉じたとき、最初の 5 個のファイルが **その他のファイル** フォルダーに引き続き表示されます。

**コードページでデータが保存できない場合、Unicode でドキュメントを保存**

このオプションを選択すると、選択したコードページと互換性のない情報を含むファイルが既定で Unicode として保存されます。

## <a name="see-also"></a>関連項目

- [その他のファイル](../../ide/reference/miscellaneous-files.md)
- [テキストの検索と置換](../../ide/finding-and-replacing-text.md)
