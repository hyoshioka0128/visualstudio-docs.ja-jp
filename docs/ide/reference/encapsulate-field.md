---
title: フィールドをプロパティにリファクタリングする
description: '[クイック アクションとリファクタリング] メニューを使用して、フィールドをプロパティに変換する方法について説明します。'
ms.custom: SEO-VS-2020
ms.date: 01/26/2018
ms.topic: reference
author: TerryGLee
ms.author: tglee
manager: jillfra
f1_keywords:
- vs.csharp.refactoring.encapsulatefield
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: e4ac28646af9d68accd18c0d40480dd22e47b023
ms.sourcegitcommit: 2244665d5a0e22d12dd976417f2a782e68684705
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2020
ms.locfileid: "96305464"
---
# <a name="encapsulate-a-field-refactoring"></a>フィールドのカプセル化リファクタリング

このリファクタリングは以下に適用されます。

- C#

- Visual Basic

**機能:** フィールドをプロパティに変換し、そのフィールドのすべての使用を、新しく作成したプロパティを使用するように更新できます。

**条件:** フィールドをプロパティに移動し、そのフィールドへのすべての参照を更新したいとき。

**理由:** 他のクラスにフィールドへのアクセスを許可しますが、これらのクラスに直接アクセス権を持たせたくはありません。  プロパティ内にフィールドをラップすることによって、たとえば、割り当てられる値を検証するコードを記述できます。

## <a name="how-to"></a>操作方法

1. カプセル化するフィールドの名前を強調表示するか、名前の内側にテキスト カーソルを置きます。

   - C#:

       ![強調表示されたコード - C#](media/encapsulate-highlight-cs.png)

   - Visual Basic:

       ![強調表示されたコード - Visual Basic](media/encapsulate-highlight-vb.png)

2. 次に、以下のいずれかを実行します。

   - **[キーボード]**
      - **Ctrl + R** キーを押し、次に **Ctrl + E** キーを押します。  選ばれているプロファイルによってキーボード ショートカットが異なる場合があることに注意してください。
      - 行の任意の場所で **Ctrl**+ **.** キーを押すと、 **[クイック アクションとリファクタリング]** メニューをトリガーし、[プレビュー] ウィンドウ ポップアップからどちらかの **[フィールドのカプセル化]** エントリを選択します。
   - **マウス**
      - **[編集] > [リファクター] > [フィールドのカプセル化]** の順に選択します。
      - コードを右クリックして **[クイック アクションとリファクタリング]** メニューを選択し、[プレビュー] ウィンドウ ポップアップからどちらかの **[フィールドのカプセル化]** エントリを選択します。

   選択 | 説明
   --------- | -----------
   **フィールドのカプセル化 (およびプロパティを使用します)** | プロパティでフィールドをカプセル化し、生成されたプロパティを使用するようにフィールドのすべての使用を更新します。
   **フィールドのカプセル化 (ただし、フィールドを継続して使用します)** | プロパティでフィールドをカプセル化しますが、フィールドのすべての使用については手を加えずに残します。

   プロパティが作成され、選ばれている場合はフィールドへの参照が更新されます。

   > [!TIP]
   > ポップアップ ウィンドウの **[変更のプレビュー]** リンクを使って、コミットする前に [結果を確認する](../../ide/preview-changes.md)ことができます。

   - C#:

      ![プロパティのカプセル化の結果 - C#](media/encapsulate-result-cs.png)

   - Visual Basic:

      ![プロパティのカプセル化の結果 - Visual Basic](media/encapsulate-result-vb.png)

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)
- [変更のプレビュー](../../ide/preview-changes.md)
