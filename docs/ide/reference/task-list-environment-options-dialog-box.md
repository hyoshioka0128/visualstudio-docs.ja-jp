---
title: '[タスク一覧] ([オプション] ダイアログ ボックス - [環境])'
description: '[環境] セクションの [タスク一覧] ページを使用して、タスク一覧のアラームを生成するコメント トークンを追加、削除、変更する方法について説明します。'
ms.custom: SEO-VS-2020
ms.date: 03/28/2019
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Environment.Task_List
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
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4b7b29c477bf046cfd47db9e39cb57360d999dee
ms.sourcegitcommit: 2cf87f79762906ccaa133a7645aa4c77a0bed7da
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2020
ms.locfileid: "96616292"
---
# <a name="options-dialog-box-environment--task-list"></a>[オプション] ダイアログ ボックス:[環境] \> [タスク一覧]

この [オプション] ページでは、**タスク一覧** のアラームを生成するコメント トークンを追加、削除、変更できます。 これらの設定を表示するには、 **[ツール]** メニューの **[オプション]** を選択し、 **[環境]** フォルダーを展開して **[タスク一覧]** を選択します。

## <a name="task-list-tokens"></a>タスク一覧のトークン

**[トークン リスト]** に登録されたトークンで始まるコメントをコード内に挿入すると、ファイルを編集用に開くたびにそのコメントが新しいエントリとして **タスク一覧** に表示されます。 コード内のコメント行に直接ジャンプするには、**タスク一覧** の項目をクリックします。 詳細については、「[タスク一覧の使用](../../ide/using-the-task-list.md)」を参照してください。

トークン リスト\
トークンの一覧が表示され、カスタム トークンを追加または削除できます。 C# および C++ ではコメント トークンの大文字と小文字が区別されますが、Visual Basic では区別されません。

> [!NOTE]
> トークン リストに表示されたとおりにトークンを入力しないと、**タスク一覧** にコメント タスクが表示されません。

優先度\
選択されたトークンを使用するタスクの優先順位を設定します (低、標準、高)。 このトークンで始まるタスク コメントには、指定された優先順位が **タスク一覧** で自動的に割り当てられます。

名前\
ここにトークン文字列を入力した後、 **[追加]** をクリックすると、文字列がトークン リストに追加されます。

追加\
新しい **名前** を入力すると有効になります。 クリックすると、 **[名前]** フィールドと **[優先順位]** フィールドに入力された値を使用して、新しいトークン文字列が追加されます。

削除\
クリックすると、選択したトークンがトークン リストから削除されます。 既定のコメント トークンは削除できません。

変更\
クリックすると、 **[名前]** フィールドと **[優先順位]** フィールドに入力された値を使用して、既存のトークンが変更されます。

> [!NOTE]
> 既定のコメント トークンの名前変更や削除はできませんが、優先順位は変更できます。

## <a name="see-also"></a>関連項目

- [タスク一覧の使用](../../ide/using-the-task-list.md)
- [コードへのブックマークの設定](../../ide/setting-bookmarks-in-code.md)
