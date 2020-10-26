---
title: 保守容易性に関する警告 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- vs.codeanalysis.maintainabilityrules
helpviewer_keywords:
- warnings, maintainability
- managed code analysis warnings, maintainability warnings
- maintainability warnings
ms.assetid: 537e70ca-a88c-49df-bfc7-0ee63bbe4f16
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: e448a72e2ff92b3e3028829d4b1e7658c304ee3c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72667890"
---
# <a name="maintainability-warnings"></a>保守性に関する警告
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

保守容易性の警告により、ライブラリとアプリケーションのメンテナンスがサポートされます。

## <a name="in-this-section"></a>このセクションの内容

|ルール|説明|
|----------|-----------------|
|[CA1500:変数名はフィールド名と同一にすることはできません](../code-quality/ca1500-variable-names-should-not-match-field-names.md)|インスタンスメソッドは、宣言する型のインスタンスフィールドと名前が一致するパラメーターまたはローカル変数を宣言します。これにより、エラーが発生します。|
|[CA1501:継承を使用しすぎないでください](../code-quality/ca1501-avoid-excessive-inheritance.md)|型が、その継承階層内の 5 つ以上深いレベルにあります。 深いレベルで入れ子にされた型の確認、理解、および保守は困難です。|
|[CA1502:メソッドの実装を複雑にしすぎないでください](../code-quality/ca1502-avoid-excessive-complexity.md)|この規則は、線形独立のメソッド経路数を示す尺度で、条件分岐の数と複雑さによって決まります。|
|[CA1504:紛らわしいフィールド名を確認します](../code-quality/ca1504-review-misleading-field-names.md)|インスタンスフィールドの名前が "s_" で始まるか、または静的 (共有) フィールドの名前が [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] "m_" で始まっています。|
|[CA1505:メンテナンスできないコードを使用しないでください](../code-quality/ca1505-avoid-unmaintainable-code.md)|型またはメソッドの保守容易性指数が低い値です。 保守容易性指数の低い型またはメソッドは、保守が困難な可能性があるため、デザインの変更を検討することをお勧めします。|
|[CA1506:クラス結合度を大きくしすぎないでください](../code-quality/ca1506-avoid-excessive-class-coupling.md)|この規則は、型またはメソッドに含まれる一意の型参照の数をカウントすることによって、クラス結合度を計測します。|

## <a name="see-also"></a>参照
 [マネージド コードの複雑さと保守性の測定](../code-quality/measuring-complexity-and-maintainability-of-managed-code.md)
