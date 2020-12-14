---
title: 参照の近くに変数宣言を移動する
description: '[クイック アクションとリファクタリング] メニューを使用して、変数宣言を使用箇所の近くに移動する方法について説明します。'
ms.custom: SEO-VS-2020
ms.date: 03/10/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 188907b4f1b6630e95ab435d588878b16c763f4a
ms.sourcegitcommit: 2cf87f79762906ccaa133a7645aa4c77a0bed7da
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2020
ms.locfileid: "96616929"
---
# <a name="move-declaration-near-reference-refactoring"></a>参照の近くへの宣言の移動リファクタリング

このリファクタリングは以下に適用されます。

- C#

- Visual Basic

**機能:** 変数宣言を使用箇所の近くに移動できます。

**条件:** より狭いスコープに保持できる変数宣言があるとき。

**理由:** そのままにしておくこともできますが、読みやすさの問題または情報の隠蔽を招く可能性があります。 これは、読みやすさを向上させるためにリファクタリングするチャンスです。

## <a name="how-to"></a>操作方法

1. 変数宣言にカーソルを置きます。

1. 次に、以下のいずれかを実行します。

   - **[キーボード]**
      - 行の任意の場所で **Ctrl**+ **.** キーを押すと、 **[クイック アクションとリファクタリング]** メニューをトリガーし、[プレビュー] ウィンドウ ポップアップから **[宣言を参照の近くに移動]** を選択します。
   - **マウス**
      - コードを右クリックして **[クイック アクションとリファクタリング]** メニューを選択し、[プレビュー] ウィンドウ ポップアップから **[宣言を参照の近くに移動]** を選択します。

1. 変更を確認したら、**Enter** キーを押すか、メニューの [修正] をクリックすると、変更がコミットされます。

例:

```csharp
// Before
int x;
if (condition)
{
    x = 1;
    Console.WriteLine(x);
}

// Move declaration near reference

// After
if (condition)
{
    int x = 1;
    Console.WriteLine(x);
}
```

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)
- [変更のプレビュー](../../ide/preview-changes.md)
