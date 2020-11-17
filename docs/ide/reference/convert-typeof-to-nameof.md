---
title: typeof を nameof に変換する
ms.date: 08/12/2020
ms.topic: reference
author: m-redding
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 96bd4d67302fb09e5c1cb7837ad73b345ad88c81
ms.sourcegitcommit: f4b49f1fc50ffcb39c6b87e2716b4dc7085c7fb5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2020
ms.locfileid: "93400325"
---
# <a name="convert-typeof-to-nameof"></a>`typeof` を `nameof` に変換する

このリファクタリングは以下に適用されます。

- C#
- Visual Basic

**概要:** C# で `typeof(<QualifiedType>).Name` のインスタンスを `nameof(<QualifiedType>)` に変換し、Visual Basic で `GetType(<QualifiedType>).Name` のインスタンスを `NameOf(<QualifiedType>)` に変換できます。

**条件:** `someType` がジェネリック型ではない `typeof(<QualifiedType>).Name` のあらゆるインスタンス。 この場合は同じ文字列値が `nameof(<QualifiedType>)` として返されないため、この除外は必要になります。 Visual Basic インスタンスにも同じことが当てはまります。

**理由:** `type` の名前ではなく `nameof` を使用することで、`type` オブジェクトの取得に関連する反映が回避されます。プログラミング手法としては実用性が高くなります。

## <a name="how-to"></a>操作方法

1. C# の `typeof(<QualifiedType>).Name` インスタンスまたは Visual Basic の `GetType(<QualifiedType>).Name` の中にカーソルを置きます。

2. 行の任意の場所で **Ctrl**+ **.** キーを押すと、 **[クイック アクションとリファクタリング]** メニューをトリガーします。

3. 次のオプションから 1 つを選択します。

    - C#
      <br>**['typeof' から 'nameof' へ変換]** を選択します。![typeof を nameof に変換する](media/convert-type-of.PNG)

    - Visual Basic
      <br>**['GetType' から 'NameOf' へ変換]** を選択します。![typeof を nameof に変換する](media/convert-get-type.PNG)

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)
