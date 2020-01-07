---
title: '[タスク一覧] ([オプション] ダイアログ ボックス - [環境]) | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Environment.Task_List
- VS.ToolsOptionsPag.Environment.Task_List
- VS.ToolsOptionsPages.Environment.TaskList
- VS.Environment.Task List
helpviewer_keywords:
- Token List
- tokens
- icons, in Task List
- Task List, customizing environment
- Options dialog box, Task List environment
- exclamation points
- comments, comment tasks in Task List
- tokens, and the Task List
- Task List, comment tasks
ms.assetid: 88327e04-fa3e-48db-995b-ad89e0dc4ed2
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 72e5f82fa3ca4b7ca909ee07e5b77a31b3e20879
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72650972"
---
# <a name="task-list-environment-options-dialog-box"></a>[タスク一覧] \([オプション] ダイアログ ボックス - [環境])
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

この [オプション] ページでは、**タスク一覧**のアラームを生成するコメント トークンを追加、削除、変更できます。 これらの設定を表示するには、 **[ツール]** メニューの **[オプション]** を選択し、 **[環境]** フォルダーを展開して **[タスク一覧]** を選択します。

## <a name="task-list-options"></a>タスク一覧オプション
 [タスクの削除の確認] 選択した場合、**タスク一覧**からユーザータスクが削除されるたびにメッセージボックスが表示され、削除を確認することができます。 既定では、このオプションはオンです。

> [!NOTE]
> タスク コメントを削除するには、コメントを探すリンクを使用し、その後コードからコメントを削除します。

 [ファイル名のみ表示] を選択した場合、**タスク一覧**の **[ファイル]** 列には、完全なパスではなく、編集するファイルの名前のみが表示されます。

## <a name="tokens"></a>トークン
 **[トークン リスト]** に登録されたトークンで始まるコメントをコード内に挿入すると、ファイルを編集用に開くたびにそのコメントが新しいエントリとして**タスク一覧**に表示されます。 この**タスク一覧**エントリをクリックすることによって、コード内のコメント行に直接ジャンプできます。 詳細については、「[タスク一覧の使用](../../ide/using-the-task-list.md)」を参照してください。

 トークンの一覧には、トークンの一覧が表示され、カスタムトークンを追加または削除することができます。 Visual C# および Visual C++ ではコメント トークンの大文字と小文字が区別されますが、Visual Basic では区別されません。

> [!NOTE]
> **[トークン リスト]** に表示されたとおりにトークンを入力しないと、**タスク一覧**にコメント タスクが表示されません。

 Priority は、選択したトークンを使用するタスクの優先順位を設定します。 このトークンで始まるタスク コメントには、指定された優先順位が**タスク一覧**で自動的に割り当てられます。

 名前トークン文字列を入力します。 入力すると、 **[追加]** ボタンをクリックできるようになります。 **[追加]** をクリックすると、この文字列が **[トークン リスト]** に追加され、この名前で始まるコメントが**タスク一覧**に表示されます。

 新しい**名前**を入力したときに有効になります。 クリックすると、 **[名前]** フィールドと **[優先順位]** フィールドに入力された値を使用して、新しいトークン文字列が追加されます。

 [削除] 選択したトークンを [**トークン] ボックスの一覧**から削除します。 既定のコメント トークンは削除できません。

 変更 **[名前]** フィールドと **[優先順位]** フィールドに入力された値を使用して、既存のトークンを変更します。

> [!NOTE]
> 既定のコメント トークンの名前変更や削除はできませんが、優先順位は変更できます。

## <a name="see-also"></a>関連項目
 [コード[環境オプション] ダイアログボックス](../../ide/reference/environment-options-dialog-box.md)の [[タスク一覧の](../../ide/using-the-task-list.md)[ブックマーク設定](../../ide/setting-bookmarks-in-code.md)] の使用
