---
title: タスク一覧の使用
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- TaskListWindow
- VS.TaskList
- tasklist
helpviewer_keywords:
- task list
- Visual Studio, task list
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: abd6d73c7b312cf00062307370ba2f7aebe6694e
ms.sourcegitcommit: f27084e64c79e6428746a20dda92795df996fb31
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85768625"
---
# <a name="use-the-task-list"></a>タスク一覧の使用

**[タスク一覧]** を使って、`TODO` や `HACK` などのトークンやカスタム トークンを使用するコード コメントを追跡し、コード内の事前に定義された場所に直接アクセスできるショートカットを管理できます。 ソース コード内のその場所に移動するには、一覧の項目をクリックします。

> [!NOTE]
> このトピックは、Windows 上の Visual Studio に適用されます。 Visual Studio for Mac については、「[タスク コメント (Visual Studio for Mac)](/visualstudio/mac/task-comments)」を参照してください。

## <a name="the-task-list-window"></a>[タスク一覧] ウィンドウ

**[タスク一覧]** が開き、アプリケーション ウィンドウの下部に表示されます。

**[タスク一覧]** を開くには、 **[表示]**  >  **[タスク一覧]** を選ぶか、**Ctrl**+ **\\** 、**T** キーを順に押します。

![タスク一覧ウィンドウ](../ide/media/vs2015_task_list.png)

一覧の並べ替え順序を変更するには、列のヘッダーを選びます。 検索結果をさらに絞り込むには、**Shift** キーを押しながら 2 番目の列ヘッダーをクリックします。 または、ショートカット メニューで **[並べ替え]** を選んでから、ヘッダーを選びます。 検索結果をさらに絞り込むには、**Shift** キーを押しながら 2 番目のヘッダーをクリックします。

列の表示と非表示を切り替え得るには、ショートカット メニューの **[列の表示]** を選びます。 表示または非表示にする列を選びます。

列の順序を変更するには、列のヘッダーを目的の場所にドラッグします。

## <a name="user-tasks"></a>ユーザーの作業

Visual Studio 2015 では、ユーザー タスク機能が削除されています。 Visual Studio 2013 以前のバージョンからのユーザー タスク データを含むソリューションを開くと、 *.suo* ファイル内のユーザー タスク データは影響を受けませんが、ユーザー タスクはタスク一覧に表示されません。

ユーザー タスク データに引き続きアクセスして更新する場合は、プロジェクトを Visual Studio 2013 で開き、好きなプロジェクト管理ツール (Team Foundation Server など) にユーザー タスクの内容をコピーします。

## <a name="tokens-and-comments"></a>トークンとコメント

**[タスク一覧]** には、コメント マーカーが手前にあるコードのコメント、および定義済みのトークンも表示されます。 たとえば、次の C# コメントには 3 つの個別の部分があります。

- コメント マーカー (`//`)

- トークン、たとえば (`TODO`)

- コメント (残りのテキスト)

```csharp
// TODO: Load state from previously suspended application
```

`TODO` が事前に定義されたトークンであるため、このコメントは `TODO` タスクとして一覧に表示されます。

> [!NOTE]
> 既定のトークンは、C/C++、C#、および VB 言語でのみ使用できます。 その他の言語については、「**カスタム トークン**」のセクションを参照してください。

### <a name="custom-tokens"></a>カスタム トークン

既定では、Visual Studio にはトークン `HACK`、`TODO`、`UNDONE`、`UnresolvedMergeConflict` が含まれます。 これらは大文字と小文字を区別しません。 カスタム トークンを独自に作成することもできます。

カスタム トークンを作成するには:

1. **[ツール]** メニューの **[オプション]** を選択します。

2. **[環境]** フォルダーを開き、 **[タスク一覧]** をクリックします。

   [[タスク一覧] オプション ページ](../ide/reference/task-list-environment-options-dialog-box.md)が表示されます。

   ![Visual Studio タスク一覧](../ide/media/vs2015_task_list_options.png)

3. **[名前]** テキスト ボックスにトークン名を入力します (例: **BUG**)。

4. **[優先順位]** ドロップダウン リストで、新しいトークンの既定の優先順位を選択します。

5. **[追加]** をクリックします。

> [!TIP]
> 名前を入力すると、 **[追加]** ボタンが有効になります。 **[追加]** をクリックする前に名前を入力する必要があります。

### <a name="c-todo-comments"></a>C++ TODO コメント

既定で、C++ TODO コメントは **[タスク一覧]** に表示されます。

C++ の TODO コメントをオフにするには、 **[ツール]** メニューで、 **[オプション]**  >  **[テキストエディター]**  >  **[C/C++]**  >  **[表示]**  >  **[コメント タスクの列挙]** の順に選択し、値を **False** に設定します。

## <a name="shortcuts"></a>ショートカット

"*ショートカット*" は、 **[タスク一覧]** で追跡されるコード内のブックマークです。 標準のブックマークとは異なるアイコンが表示されます。 コード内の対応する位置に移動するには、 **[タスク一覧]** にあるショートカットをダブルクリックします。

![Visual Studio タスク一覧へのショートカット アイコン](../ide/media/vs2015_task_list_bookmark.png)

### <a name="create-a-shortcut"></a>ショートカットを作成する

ショートカットを作成するには、ショートカットを配置するコードにポインターを挿入します。 **[編集]**  >  **[ブックマーク]**  >  **[タスク一覧へのショートカットの追加]** の順に選択するか、または **Ctrl**+**K**、**Ctrl**+**H** キーを押します。

コード内のショートカットをナビゲートしていくには、一覧でショートカットを選択し、ショートカット メニューから **[次のタスク]** か **[前のタスク]** をクリックします。

## <a name="see-also"></a>参照

- [[タスク一覧] ([オプション] ダイアログ ボックス - [環境])](../ide/reference/task-list-environment-options-dialog-box.md)
- [タスク コメント (Visual Studio for Mac)](/visualstudio/mac/task-comments)
