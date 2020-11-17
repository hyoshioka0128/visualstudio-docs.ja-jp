---
title: メソッドのインライン化
ms.date: 11/03/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 0cc619ea61a7fd4d7f4bc542b946e298933a8f73
ms.sourcegitcommit: f4b49f1fc50ffcb39c6b87e2716b4dc7085c7fb5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2020
ms.locfileid: "93403538"
---
# <a name="inline-method"></a>メソッドのインライン化

このリファクタリングは以下に適用されます。

- C#

- Visual Basic

**概要:** インライン メソッドのリファクタリング。 

**条件:** 1 つのステートメント本体内の静的、インスタンス、および拡張の各メソッドの使用を、元のメソッドの宣言を削除するオプションに置き換える必要があります。

**理由:** このリファクタリングによって、構文がより明確になります。

## <a name="how-to"></a>方法

1. メソッドの使用にカレットを置きます。

2. 行の任意の場所で **Ctrl**+ **.** キーを押すと、 **[クイック アクションとリファクタリング]** メニューをトリガーします。

3. 次のオプションから 1 つを選択します。 
    
   **[Inline `<QualifiedMethodName>`]\(`<QualifiedMethodName>` のインライン化\)** を選択し、メソッドのインラインでの宣言を削除します。

    ![クラスを抽象にする](media/inline-method-remove-declaration.png)

   **[Inline and keep `<QualifiedMethodName>`]\(インライン化して `<QualifiedMethodName>` を保持\)** を選択して、元のメソッド宣言を保持します。

    ![クラスを抽象にする](media/inline-method-preserve-declaration.png)

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)
