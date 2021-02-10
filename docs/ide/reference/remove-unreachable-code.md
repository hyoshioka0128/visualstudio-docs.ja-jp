---
title: 到達できないコードの削除リファクタリング
description: '[クイック アクションとリファクタリング] メニューを使用して、実行されないコードを削除する方法について説明します。'
ms.custom: SEO-VS-2020
ms.date: 03/10/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jmartens
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: a7ce04b38c13b0994d47974488b90114a63495e6
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99958116"
---
# <a name="remove-unreachable-code-refactoring"></a>到達できないコードの削除リファクタリング

このリファクタリングは以下に適用されます。

- C#

- Visual Basic

**機能:** 実行されないコードを削除します。

**条件:** プログラムにコード スニペットに到達するパスがなく、そのコード スニペットが不要になっているとき。

**理由:** 不必要で実行されることのないコードを削除することで、読みやすさを向上させ保守を容易にします。

## <a name="how-to"></a>操作方法

1. 到達できずフェードアウトされているコードの任意の場所にカーソルを置きます。

![フェードアウトされている到達できないコード](media/unreachablecode-faded-cs.png)

1. 次に、以下のいずれかを実行します。

   - **[キーボード]**
      - 行の任意の場所で **Ctrl**+ **.** キーを押すと、 **[クイック アクションとリファクタリング]** メニューをトリガーし、[プレビュー] ウィンドウ ポップアップから **[到達できないコードを削除します]** を選択します。
   - **マウス**
      - コードを右クリックして **[クイック アクションとリファクタリング]** メニューを選択し、[プレビュー] ウィンドウ ポップアップから **[到達できないコードを削除します]** を選択します。

1. 変更を確認したら、**Enter** キーを押すか、メニューの [修正] をクリックすると、変更がコミットされます。

例:

```csharp
// Before
private void Method()
{
    throw new Exception(nameof(Method));
    Console.WriteLine($"Exception for method {nameof(Method)}");
}

// Remove unreachable code

// After
private void Method()
{
    throw new Exception(nameof(Method));
}
```

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)
- [変更のプレビュー](../../ide/preview-changes.md)
