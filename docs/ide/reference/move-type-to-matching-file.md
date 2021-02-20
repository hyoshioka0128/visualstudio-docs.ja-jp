---
title: 一致するファイルへの型の移動リファクタリング
description: 型を同じ名前の別のファイルに移動します。 型名を右クリックして [クイック アクションとリファクタリング] を選択し、[型を <TypeName>.cs に移動] を選択します。
ms.date: 01/26/2018
ms.topic: reference
author: TerryGLee
ms.author: tglee
manager: jmartens
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 728b9e176a40d2bfd7ae36a329409cb27f80fc86
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99927960"
---
# <a name="move-a-type-to-a-matching-file-refactoring"></a>一致するファイルへの型の移動リファクタリング

このリファクタリングは以下に適用されます。

- C#

- Visual Basic

**機能:** 選択した型を同じ名前の別のファイルに移動できます。

**条件:** 同じファイルに複数のクラス、構造体、インターフェイスなどがあり、分離したいとき。

**理由:** 同じファイルに複数の型を配置すると、これらの型を検索しづらくなります。 型を同じ名前のファイルに移動することで、コードが読みやすくナビゲートしやすくなります。

## <a name="how-to"></a>操作方法

1. 定義されている型の名前の中にカーソルを配置します。 次に例を示します。

   ```csharp
   class Person
   ```

   ```vb
   Class Person
   ```

2. 次に、以下のいずれかを実行します。

   - 行の任意の場所で **Ctrl**+ **.** キーを押すと、
   - 型名を右クリックして **[クイック アクションとリファクタリング]** を選択します。

1. メニューから **[型を *TypeName*.cs に移動]** を選択します。*TypeName* は選択した型の名前です。

   型と同じ名前を持つプロジェクト内の新しいファイルに型が移動されます。

   - C#:

      ![インラインの結果 - C#](media/movetype-result-cs.png)

   - Visual Basic:

      ![インラインの結果 - Visual Basic](media/movetype-result-vb.png)

## <a name="see-also"></a>参照

- [リファクタリング](../refactoring-in-visual-studio.md)
