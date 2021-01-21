---
title: メソッドのインライン化
description: Visual Studio の [クイック アクションとリファクタリング] メニューを使用してインライン メソッド宣言をリファクターし、より明確な構文を提供する方法について説明します。
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
ms.openlocfilehash: 655c6dad03b05b257aec3d92199321a0e0e93d22
ms.sourcegitcommit: 3c571f44bfd6402efea5187af43df287bac5b6ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/24/2020
ms.locfileid: "97761421"
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

    ![Visual Studio の [クイック アクションとリファクタリング] メニューのスクリーンショット。[Inline 'CreateWidget()']\(CreateWidget()' のインライン化\) が選択され、C# コードの変更が表示されています。](media/inline-method-remove-declaration.png)

   **[Inline and keep `<QualifiedMethodName>`]\(インライン化して `<QualifiedMethodName>` を保持\)** を選択して、元のメソッド宣言を保持します。

    ![Visual Studio の [クイック アクションとリファクタリング] メニューのスクリーンショット。[Inline and keep 'CreateWidget()']\('CreateWidget()' をインライン化して保持\) が選択され、C# コードの変更が表示されています。](media/inline-method-preserve-declaration.png)

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)
