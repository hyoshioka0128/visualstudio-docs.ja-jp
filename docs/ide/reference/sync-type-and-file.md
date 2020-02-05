---
title: 型に合わせてファイル名を変更する
ms.date: 01/26/2018
ms.topic: reference
author: TerryGLee
ms.author: tglee
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 5b7a42a174fecd078e804f2ab3c35fbe442364a6
ms.sourcegitcommit: 4be64917e4224fd1fb27ba527465fca422bc7d62
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/03/2020
ms.locfileid: "75594397"
---
# <a name="sync-a-type-to-a-filename-or-a-filename-to-a-type-refactoring"></a>型からファイル名への同期またはファイル名から型への同期リファクタリング

このリファクタリングは以下に適用されます。

- C#

- Visual Basic

**概要:** 型名をファイル名と一致するように変更、またはファイル名を含まれている型と一致するように変更できます。

**条件:** ファイルまたは型の名前を変更したが、対応するファイルまたは型を一致するようにまだ更新していないとき。

**理由:** 型が別の名前のファイルに (またはその逆に) 配置されていると、検索が困難になります。 型またはファイルどちらかの名前を変更することで、コードが読みやすくナビゲートしやすくなります。

> [!NOTE]
> このリファクタリングは、.NET Standard プロジェクトと .NET Core プロジェクトではまだ利用できません。

## <a name="how-to"></a>方法

1. 同期する型の名前を強調表示するか、名前の内側にテキスト カーソルを置きます。

   - C#:

       ![強調表示されたコード - C#](media/synctype-highlight-cs.png)

   - Visual Basic:

       ![強調表示されたコード - Visual Basic](media/synctype-highlight-vb.png)

2. 次に、以下のいずれかを実行します。

   - **キーボード**
      - 行の任意の場所で **Ctrl**+ **.** キーを押すと、 **[クイック アクションとリファクタリング]** メニューをトリガーし、[プレビュー] ウィンドウ ポップアップから **[Rename file to *TypeName*.cs]\(ファイルの名前を TypeName.cs に変更\)** を選択します。ここで、*TypeName* は選択した型の名前です。
      - 行の任意の場所で **Ctrl**+ **.** キーを押すと、 **[クイック アクションとリファクタリング]** メニューをトリガーし、[プレビュー] ウィンドウ ポップアップ から **[型の名前を _Filename_ に変更]** を選択します。ここで、*Filename* は現在のファイルの名前です。
   - **マウス**
      - コードを右クリックして **[クイック アクションとリファクタリング]** メニューを選択し、[プレビュー] ウィンドウ ポップアップから **[Rename file to *TypeName*.cs]\(ファイルの名前を TypeName.cs に変更\)** を選択します。ここで、*TypeName* は選択した型の名前です。
      - コードを右クリックして **[クイック アクションとリファクタリング]** メニューを選択し、[プレビュー] ウィンドウ ポップアップから **[型の名前を _Filename_ に変更]** を選択します。ここで、*Filename* は現在のファイルの名前です。

   型またはファイルの名前が変更されます。

   - C#: 次の例で、ファイル **MyClass.cs** は型名と一致する **MyNewClass.cs** に名前が変更されました。

       ![インラインの結果 C#](media/synctype-result-cs.png)

   - Visual Basic: 次の例で、ファイル **Employee.vb** は型名と一致する **Person.vb** に名前が変更されました。

       ![インラインの結果 Visual Basic](media/synctype-result-vb.png)

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)
