---
title: 'CA2226: 演算子には対称的なオーバーロード | が必要です。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- OperatorsShouldHaveSymmetricalOverloads
- CA2226
helpviewer_keywords:
- OperatorsShouldHaveSymmetricalOverloads
- CA2226
ms.assetid: d202401a-ea14-4559-b15e-0ea4f5b68789
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 430a8d3cfd3b8ced45b60bd9dc70211711886d43
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85540570"
---
# <a name="ca2226-operators-should-have-symmetrical-overloads"></a>CA2226:演算子は対称型オーバーロードを含まなければなりません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|OperatorsShouldHaveSymmetricalOverloads|
|CheckId|CA2226|
|カテゴリ|Microsoft. 使用方法|
|互換性に影響する変更点|中断なし|

## <a name="cause"></a>原因
 型で等値演算子または非等値演算子を実装し、逆の働きをする演算子を実装していません。

## <a name="rule-description"></a>ルールの説明
 等値または非等値が型のインスタンスに適用され、反対側の演算子が定義されていない状況はありません。 型は、通常、等値演算子の符号を反転した値を返すことによって、非等値演算子を実装します。

 C# コンパイラは、この規則違反のエラーを発行します。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、等値演算子と非等値演算子の両方を実装するか、存在する演算子を削除します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。 型は、と一貫性のある方法では動作しません [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 。

## <a name="related-rules"></a>関連規則
 [CA1046:参照型で、演算子 equals をオーバーロードしないでください](../code-quality/ca1046-do-not-overload-operator-equals-on-reference-types.md)

 [CA2225:演算子オーバーロードには名前付けされた代替が存在します](../code-quality/ca2225-operator-overloads-have-named-alternates.md)

 [CA2224:オーバーロードする演算子 equals で Equals をオーバーライドします](../code-quality/ca2224-override-equals-on-overloading-operator-equals.md)

 [CA2218:オーバーライドする Equals で GetHashCode をオーバーライドします](../code-quality/ca2218-override-gethashcode-on-overriding-equals.md)

 [CA2231:ValueType.Equals のオーバーライドで、演算子 equals をオーバーロードします](../code-quality/ca2231-overload-operator-equals-on-overriding-valuetype-equals.md)
