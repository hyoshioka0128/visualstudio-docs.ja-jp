---
title: メソッドの抽出
description: コードを選択してから Ctrl + R キー、Ctrl + M キーを入力して、コードの一部を独自のメソッドに変換します。
ms.date: 01/26/2018
ms.topic: reference
author: TerryGLee
ms.author: tglee
manager: jmartens
f1_keywords:
- vs.csharp.refactoring.extractmethod
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: b39112a696611103828d862c7f7adf04784e6222
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99860998"
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

       Program クラスの C# コードを示すスクリーンショット。 このクラスの Main 関数内で、コード行が強調表示されています (media/extractmethod-highlight-cs.png)。

   - Visual Basic:

       ![Main Sub の Visual Basic コードを示すスクリーンショット。 この Sub 内で、コード行が強調表示されています。](media/extractmethod-highlight-vb.png)

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
   > この新しい名前を使用するコメントやその他の文字列も更新できます。また、IDE の右上に表示される **[名前の変更]** ボックス内のチェックボックスを使用して、保存前に [変更をプレビュー](../../ide/preview-changes.md)することもできます。

   - C#:

      ![Program クラスの C# コードを示すスクリーンショット。 メソッド名が強調表示され、[名前の変更] ポップアップ ウィンドウが開いています。](media/extractmethod-rename-cs.png)

   - Visual Basic:

      ![Main Sub の Visual Basic コードを示すスクリーンショット。 メソッド名が強調表示され、[名前の変更] ポップアップ ウィンドウが開いています。](media/extractmethod-rename-vb.png)

3. 変更を確認した後は、 **[適用]** ボタンを選ぶか、**Enter** キーを押すと、変更がコミットされます。

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)
- [変更のプレビュー](../../ide/preview-changes.md)
