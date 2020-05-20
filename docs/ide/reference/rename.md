---
title: 名前の変更のリファクタリング
ms.date: 01/26/2018
ms.topic: reference
author: TerryGLee
ms.author: tglee
manager: jillfra
f1_keywords:
- vs.csharp.refactoring.rename
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 4dbccd4732f56d671fd74f59916885ea338136f8
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "75565462"
---
# <a name="rename-a-code-symbol-refactoring"></a>コード シンボルの名前の変更のリファクタリング

このリファクタリングは以下に適用されます。

- C#

- Visual Basic

**概要:** フィールド、ローカル変数、メソッド、名前空間、プロパティ、型などのコード シンボルの識別子の名前を変更します。

**タイミング:** すべてのインスタンスを検索して新しい名前をコピー/貼り付けすることなく、安全に名前を変更したいとき。

**理由:** プロジェクト全体で新しい名前をコピーおよび貼り付けることは、エラーにつながる可能性があるため。 このリファクタリング ツールでは、正確に名前変更操作が実行されます。

## <a name="how-to"></a>操作方法

1. 名前を変更する項目を強調表示するか、項目の内側にテキスト カーソルを置きます。

   - C#:

       ![強調表示されたコード - C#](media/rename-highlight-cs.png)

   - Visual Basic:

       ![強調表示されたコード - Visual Basic](media/rename-highlight-vb.png)

2. 次に、以下のいずれかを実行します。

   - **[キーボード]**
      - **Ctrl + R** キーを押し、次に **Ctrl + R** キーを押します。 選ばれているプロファイルによってキーボード ショートカットが異なる場合があることに注意してください。
   - **マウス**
      - **[編集] > [リファクター] > [名前の変更]** の順に選択します。
      - コードを右クリックし **[名前の変更]** を選択します。

3. 新しい名前を入力して、項目の名前を変更します。

   - C#:

      ![名前の変更のアニメーション - C#](media/rename-animated-cs.gif)

   - Visual Basic:

      ![名前の変更 - VB](media/rename-rename-vb.png)

   > [!TIP]
   > この新しい名前を使うように、コメントや他の文字列も更新できます。また、エディターの右上に表示される **[名前の変更]** ボックスのチェック ボックスを使って、保存前に[変更をプレビューする](../../ide/preview-changes.md)こともできます。

4. 変更を確認した後は、 **[適用]** ボタンを選ぶか、**Enter** キーを押すと、変更がコミットされます。

## <a name="remarks"></a>解説

- Visual Studio 2019 バージョン 16.3 以降では、ある型の名前がそれが含まれているファイルの名前に一致するとき、その型の名前を変更すると、ファイルの名前も同時に変更できるチェックボックスが表示されます。 クラス、インターフェイス、または列挙型の名前を変更するとき、このオプションが表示されます。 このオプションは、複数の定義を持つ部分型ではサポートされていません。

   ![ファイルを含むアニメーションの名前を変更する - C#](media/rename-with-file-animated-cs.gif)

- 競合が発生する可能性がある既存の名前を使うと、 **[名前の変更]** ボックスに警告が表示されます。

   ![名前変更の競合](media/rename-conflict-cs.png)

- シンボルの名前を変更する別の方法は、エディターでその名前を変更することです。 次に、シンボル名にカーソルを置き、**Ctrl**+ **を押します。** または、表示された電球アイコン メニューを展開して、 **[\<古い名前> を \<新しい名前> に変更]** を選択します。

## <a name="see-also"></a>参照

- [リファクタリング](../refactoring-in-visual-studio.md)
- [変更のプレビュー](../../ide/preview-changes.md)
