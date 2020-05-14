---
title: メソッドの抽出
description: コードを選択してから Ctrl + R キー、Ctrl + M キーを入力して、コードの一部を独自のメソッドに変換します。
ms.date: 01/26/2018
ms.topic: reference
author: TerryGLee
ms.author: tglee
manager: jillfra
f1_keywords:
- vs.csharp.refactoring.extractmethod
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 50f14cc2a7eafe5d65e0c6a6af54bafa2ebb5a1f
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "75569700"
---
# <a name="extract-a-method-refactoring"></a>メソッドの抽出リファクタリング

このリファクタリングは以下に適用されます。

- C#

- Visual Basic

**機能:** コードのフラグメントを独自のメソッドに変換できます。

**条件:** メソッドに、別のメソッドから呼び出される必要がある既存のコードのフラグメントがあるとき。

**理由:** コードのコピー/貼り付けはできるが、重複につながるおそれがあるため。 他のメソッドから自由に呼び出すことができる独自のメソッドに、そのフラグメントをリファクターすることをお勧めします。

## <a name="how-to"></a>操作方法

1. 抽出するコードを強調表示します。

   - C#:

       ![強調表示されたコード - C#](media/extractmethod-highlight-cs.png)

   - Visual Basic:

       ![強調表示されたコード - Visual Basic](media/extractmethod-highlight-vb.png)

2. 次に、以下のいずれかを実行します。

   - **[キーボード]**
      - **Ctrl + R** キーを押し、次に **Ctrl + M** キーを押します。 選ばれているプロファイルによってキーボード ショートカットが異なる場合があることに注意してください。
      - 行の任意の場所で **Ctrl**+ **.** キーを押すと、 **[クイック アクションとリファクタリング]** メニューをトリガーし、[プレビュー] ウィンドウ ポップアップから **[メソッドの抽出]** を選択します。
   - **マウス**
      - **[編集] > [リファクター] > [メソッドの抽出]** の順に選択します。
      - コードを右クリックし **[リファクター] > [抽出] > [メソッドの抽出]** の順に選択します。
      - コードを右クリックして **[クイック アクションとリファクタリング]** メニューを選択し、[プレビュー] ウィンドウ ポップアップから **[メソッドの抽出]** を選択します。

   メソッドがすぐに作成されます。 ここから、新しい名前を入力するだけで、メソッドの名前を今すぐ変更できます。

   > [!TIP]
   > この新しい名前を使用するコメントやその他の文字列も更新できます。また、IDE の右上に表示される [[名前の変更]](../../ide/preview-changes.md) ボックス内のチェックボックスを使用して、保存前に**変更をプレビュー**することもできます。

   - C#:

      ![メソッド名の変更 - C#](media/extractmethod-rename-cs.png)

   - Visual Basic:

      ![メソッド名の変更 - Visual Basic](media/extractmethod-rename-vb.png)

3. 変更を確認した後は、 **[適用]** ボタンを選ぶか、**Enter** キーを押すと、変更がコミットされます。

## <a name="see-also"></a>参照

- [リファクタリング](../refactoring-in-visual-studio.md)
- [変更のプレビュー](../../ide/preview-changes.md)
