---
title: 'CA2235: すべてのシリアル化不可能なフィールドをマークします。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2235
- MarkAllNonSerializableFields
helpviewer_keywords:
- CA2235
- MarkAllNonSerializableFields
ms.assetid: 599ad877-3a15-426c-bf17-5de15427365f
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: fab79fd4daab98c6cade9271b32c45b5ae4b4332
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85545198"
---
# <a name="ca2235-mark-all-non-serializable-fields"></a>CA2235:すべてのシリアル化不可能なフィールドを設定します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|MarkAllNonSerializableFields|
|CheckId|CA2235|
|カテゴリ|Microsoft. 使用方法|
|互換性に影響する変更点|中断なし|

## <a name="cause"></a>原因
 シリアル化できない型のインスタンス フィールドが、シリアル化できる型で宣言されています。

## <a name="rule-description"></a>ルールの説明
 シリアル化可能な型は、属性でマークされた型です <xref:System.SerializableAttribute?displayProperty=fullName> 。 型をシリアル化できる場合、型に <xref:System.Runtime.Serialization.SerializationException?displayProperty=fullName> シリアル化できない型のインスタンスフィールドが含まれていると、例外がスローされます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するに <xref:System.NonSerializedAttribute?displayProperty=fullName> は、シリアル化できないフィールドに属性を適用します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 <xref:System.Runtime.Serialization.ISerializationSurrogate?displayProperty=fullName>フィールドのインスタンスをシリアル化および逆シリアル化できる型が宣言されている場合にのみ、この規則からの警告を抑制します。

## <a name="example"></a>例
 次の例は、規則に違反する型と、規則を満たす型を示しています。

 [!code-csharp[FxCop.Usage.MarkNonSerializable#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.MarkNonSerializable/cs/FxCop.Usage.MarkNonSerializable.cs#1)]
 [!code-vb[FxCop.Usage.MarkNonSerializable#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.MarkNonSerializable/vb/FxCop.Usage.MarkNonSerializable.vb#1)]

## <a name="related-rules"></a>関連規則
 [CA2236:ISerializable 型で基底クラス メソッドを呼び出します](../code-quality/ca2236-call-base-class-methods-on-iserializable-types.md)

 [CA2240:ISerializable を正しく実装します](../code-quality/ca2240-implement-iserializable-correctly.md)

 [CA2229:シリアル化コンストラクターを実装します](../code-quality/ca2229-implement-serialization-constructors.md)

 [CA2238:シリアル化メソッドを正しく実装します](../code-quality/ca2238-implement-serialization-methods-correctly.md)

 [CA2237:ISerializable 型を SerializableAttribute に設定します](../code-quality/ca2237-mark-iserializable-types-with-serializableattribute.md)

 [CA2239:省略可能なフィールドに、逆シリアル化メソッドを指定します](../code-quality/ca2239-provide-deserialization-methods-for-optional-fields.md)

 [CA2120:シリアル化コンストラクターをセキュリティで保護します](../code-quality/ca2120-secure-serialization-constructors.md)
