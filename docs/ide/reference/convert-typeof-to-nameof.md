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
ms.openlocfilehash: 233393114883c2a9833aa7ec82f0d78f0ef33bae
ms.sourcegitcommit: 577c905de52057a741e68c2ed168ea527813fda5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/15/2020
ms.locfileid: "88251337"
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
  <br>**"typeof" を "nameof" に変換する**ように選択します
  !["typeof" を "nameof" に変換する](media/convert-type-of.PNG)

- Visual Basic
  <br>**"GetType" を "NameOf" に変換する**ように選択します!["GetType" を "NameOf" に変換する](media/convert-get-type.PNG)

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)
