---
title: typeof を nameof に変換する
description: Visual Studio の [クイック アクションとリファクタリング] メニューを使用して、C# で typeof を nameof に変換し、Visual Basic で GetType を NameOf に変換する方法について説明します。
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
ms.openlocfilehash: ce76b82e2ebc68634be7cf4d463f6b8216d81e06
ms.sourcegitcommit: 3c571f44bfd6402efea5187af43df287bac5b6ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/24/2020
ms.locfileid: "97761200"
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
      <br>**['typeof' から 'nameof' へ変換]** を選択します。![Visual Studio の [クイック アクションとリファクタリング] メニューのスクリーンショット。['typeof' から 'nameof' へ変換] が選択され、C# コードの変更が表示されています。](media/convert-type-of.PNG)

    - Visual Basic
      <br>**['GetType' から 'NameOf' へ変換]** を選択します。![Visual Studio の [クイック アクションとリファクタリング] メニューのスクリーンショット。['GetType' から 'NameOf' へ変換] が選択され、Visual Basic コードの変更が表示されています。](media/convert-get-type.PNG)

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)
