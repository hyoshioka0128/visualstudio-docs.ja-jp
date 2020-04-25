---
title: 保守性に関する警告
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.codeanalysis.maintainabilityrules
helpviewer_keywords:
- warnings, maintainability
- managed code analysis warnings, maintainability warnings
- maintainability warnings
ms.assetid: 537e70ca-a88c-49df-bfc7-0ee63bbe4f16
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: fd7fe79665ac8de665116a6832d5ef9327fb356c
ms.sourcegitcommit: dab57cebd484228e6f0cf7ab1b9685c575410c06
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/25/2020
ms.locfileid: "82152991"
---
# <a name="maintainability-warnings"></a>保守性に関する警告

保守容易性の警告により、ライブラリとアプリケーションのメンテナンスがサポートされます。

## <a name="in-this-section"></a>このセクションの内容

| ルール | 説明 |
|-----------|-----------------------------------|
| [CA1500: 変数名はフィールド名と同一にすることはできません](../code-quality/ca1500.md) | インスタンスメソッドは、宣言する型のインスタンスフィールドと名前が一致するパラメーターまたはローカル変数を宣言します。これにより、エラーが発生します。 |
| [CA1501: 継承を使用しすぎないでください](../code-quality/ca1501.md) | 型が、その継承階層内の 5 つ以上深いレベルにあります。 深いレベルで入れ子にされた型の確認、理解、および保守は困難です。 |
| [CA1502: メソッドの実装を複雑にしすぎないでください](../code-quality/ca1502.md) | この規則は、線形独立のメソッド経路数を示す尺度で、条件分岐の数と複雑さによって決まります。 |
| [CA1504: 紛らわしいフィールド名をレビューします](../code-quality/ca1504.md) | インスタンスフィールドの名前が "s_" で始まるか、または静的 (共有[!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]) フィールドの名前が "m_" で始まっています。 |
| [CA1505: メンテナンスできないコードを使用しないでください](../code-quality/ca1505.md) | 型またはメソッドの保守容易性指数が低い値です。 保守容易性指数の低い型またはメソッドは、保守が困難な可能性があるため、デザインの変更を検討することをお勧めします。 |
| [CA1506: クラス結合度を大きくしすぎないでください](../code-quality/ca1506.md) | この規則は、型またはメソッドに含まれる一意の型参照の数をカウントすることによって、クラス結合度を計測します。 |
| [CA1507: 文字列の代わりに文字列を使用します。](../code-quality/ca1507.md) | 文字列リテラルは、式を`nameof`使用できる引数として使用されます。 |
| [CA1508: デッド条件コードを回避する](../code-quality/ca1508.md) | メソッドには、常に`true`または`false`実行時に評価される条件付きコードがあります。 これにより、条件の`false`分岐でコードが停止します。 |

## <a name="see-also"></a>関連項目

- [マネージコードの複雑さと保守性の測定](../code-quality/code-metrics-values.md)
