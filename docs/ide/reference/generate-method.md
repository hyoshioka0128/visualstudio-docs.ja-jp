---
title: メソッドを生成する
description: '[クイック アクションとリファクタリング] メニューを使用して、クラスにメソッドをすぐに追加する方法について説明します。'
ms.custom: SEO-VS-2020
ms.date: 01/26/2018
ms.topic: reference
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 22c49085a430c7afc002fe4e11dcf1184348efdc
ms.sourcegitcommit: 2cf87f79762906ccaa133a7645aa4c77a0bed7da
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2020
ms.locfileid: "96617215"
---
# <a name="generate-a-method-in-visual-studio"></a>Visual Studio でメソッドを生成する

このコード生成は以下に適用されます。

- C#

- Visual Basic

**機能:** クラスにメソッドをすぐに追加できます。

**条件:** 新しいメソッドを導入し、自動的に適切に宣言したいとき。

**理由:** メソッドとパラメーターは使用する前に自分でも宣言できるが、この機能では自動的に宣言が生成されるため。

## <a name="how-to"></a>操作方法

1. 赤い波線が表示されている行にカーソルを置きます。 赤い波線は、まだ存在していないメソッドを示します。

   - C#:

       ![強調表示された C# のコード](media/method-highlight-cs.png)

   - Visual Basic:

       ![強調表示された VB のコード](media/method-highlight-vb.png)

2. 次に、以下のいずれかを実行します。

   - **[キーボード]**
      - 行の任意の場所で **Ctrl**+ **.** キーを押すと、 **[クイック アクションとリファクタリング]** メニューをトリガーします。
   - **マウス**
      - 右クリックして **[クイック アクションとリファクタリング]** メニューを選択します。
      - 赤い波線をポイントし、表示された ![エラー電球](media/error-bulb.png) アイコンをクリックします。
      - テキスト カーソルが既に赤い波線の行にある場合は、左余白に表示されている ![エラー電球](media/error-bulb.png) アイコンをクリックします。

      ![メソッド生成のプレビュー](media/method-preview-cs.png)

3. ドロップダウン メニューから **[メソッドの生成]** を選択します。

   > [!TIP]
   > プレビュー ウィンドウの下部にある **[変更のプレビュー]** リンクを使うと、選択する前に、行われる [すべての変更を確認する](../../ide/preview-changes.md)ことができます。

   メソッドと、その使用法から推論されるすべてのパラメーターが作成されます。

   - C#:

       ![C# のメソッド生成結果](media/method-result-cs.png)

   - Visual Basic:

       ![VB のメソッド生成結果](media/method-result-vb.png)

## <a name="see-also"></a>関連項目

- [コード生成](../code-generation-in-visual-studio.md)
- [変更のプレビュー](../../ide/preview-changes.md)
