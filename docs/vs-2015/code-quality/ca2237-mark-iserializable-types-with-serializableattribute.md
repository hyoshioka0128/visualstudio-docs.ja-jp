---
title: 'CA2237: ISerializable 型を SerializableAttribute | でマークします。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2237
- MarkISerializableTypesWithSerializable
helpviewer_keywords:
- MarkISerializableTypesWithSerializable
- CA2237
ms.assetid: 9bd6bb24-a527-43dd-9952-043c0c694f46
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: d8778b0bfa035c782cf35d205fc59d463112196c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85545159"
---
# <a name="ca2237-mark-iserializable-types-with-serializableattribute"></a>CA2237:ISerializable 型を SerializableAttribute に設定します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|MarkISerializableTypesWithSerializable|
|CheckId|CA2237|
|カテゴリ|Microsoft. 使用方法|
|互換性に影響する変更点|中断なし|

## <a name="cause"></a>原因
 外部から参照できる型 <xref:System.Runtime.Serialization.ISerializable?displayProperty=fullName> がインターフェイスを実装しており、型が属性でマークされていません <xref:System.SerializableAttribute?displayProperty=fullName> 。 このルールは、基本型がシリアル化可能でない派生型を無視します。

## <a name="rule-description"></a>ルールの説明
 共通言語ランタイムによってシリアル化可能として認識されるためには、 <xref:System.SerializableAttribute> 型がインターフェイスの実装によってカスタムのシリアル化ルーチンを使用する場合でも、型は属性でマークする必要があり <xref:System.Runtime.Serialization.ISerializable> ます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、 <xref:System.SerializableAttribute> 属性を型に適用します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 例外クラスでは、アプリケーションドメイン間で正しく機能するためにシリアル化できる必要があるため、この規則による警告を抑制しないでください。

## <a name="example"></a>例
 次の例は、規則に違反する型を示しています。 規則を <xref:System.SerializableAttribute> 満たすには、属性行のコメントを解除します。

 [!code-csharp[FxCop.Usage.MarkSerializable#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.MarkSerializable/cs/FxCop.Usage.MarkSerializable.cs#1)]
 [!code-vb[FxCop.Usage.MarkSerializable#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.MarkSerializable/vb/FxCop.Usage.MarkSerializable.vb#1)]

## <a name="related-rules"></a>関連規則
 [CA2236:ISerializable 型で基底クラス メソッドを呼び出します](../code-quality/ca2236-call-base-class-methods-on-iserializable-types.md)

 [CA2240:ISerializable を正しく実装します](../code-quality/ca2240-implement-iserializable-correctly.md)

 [CA2229:シリアル化コンストラクターを実装します](../code-quality/ca2229-implement-serialization-constructors.md)

 [CA2238:シリアル化メソッドを正しく実装します](../code-quality/ca2238-implement-serialization-methods-correctly.md)

 [CA2235:すべてのシリアル化不可能なフィールドを設定します](../code-quality/ca2235-mark-all-non-serializable-fields.md)

 [CA2239:省略可能なフィールドに、逆シリアル化メソッドを指定します](../code-quality/ca2239-provide-deserialization-methods-for-optional-fields.md)

 [CA2120:シリアル化コンストラクターをセキュリティで保護します](../code-quality/ca2120-secure-serialization-constructors.md)
