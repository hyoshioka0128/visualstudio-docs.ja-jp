---
title: 'CA2240: ISerializable を正しく実装します |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2240
- ImplementISerializableCorrectly
helpviewer_keywords:
- CA2240
- ImplementISerializableCorrectly
ms.assetid: cf05936d-0d6c-49ed-a1b4-220032e50b97
caps.latest.revision: 23
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 217f95b7d3658db107fc482040686eea9ee47604
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85543664"
---
# <a name="ca2240-implement-iserializable-correctly"></a>CA2240:ISerializable を正しく実装します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|ImplementISerializableCorrectly|
|CheckId|CA2240|
|カテゴリ|Microsoft. 使用方法|
|互換性に影響する変更点|中断なし|

## <a name="cause"></a>原因
 外部から参照できる型は、インターフェイスに割り当てることができ、 <xref:System.Runtime.Serialization.ISerializable?displayProperty=fullName> 次のいずれかの条件が当てはまります。

- 型はを継承しますが、メソッドをオーバーライドしません <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A?displayProperty=fullName> 。型は、属性でマークされていないインスタンスフィールドを宣言し <xref:System.NonSerializedAttribute?displayProperty=fullName> ます。

- 型はシールされていません。型は、 <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A> 外部から参照できないオーバーライド可能なメソッドを実装しています。

## <a name="rule-description"></a>ルールの説明
 インターフェイスを継承する型で宣言されたインスタンスフィールド <xref:System.Runtime.Serialization.ISerializable?displayProperty=fullName> は、シリアル化プロセスに自動的に含まれません。 フィールドを含めるには、型は <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A> メソッドとシリアル化コンストラクターを実装する必要があります。 フィールドをシリアル化しない場合は、フィールドに属性を適用して <xref:System.NonSerializedAttribute> 明示的に決定を指定します。

 シールされていない型では、メソッドの実装を <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A> 外部から参照できるようにする必要があります。 したがって、メソッドは派生型によって呼び出すことができ、オーバーライド可能です。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、 <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A> メソッドを表示およびオーバーライドできるようにし、すべてのインスタンスフィールドがシリアル化プロセスに含まれるか、または属性で明示的にマークされていることを確認し <xref:System.NonSerializedAttribute> ます。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。

## <a name="example"></a>例
 次の例は、規則に違反する2つのシリアル化可能な型を示しています。

 [!code-cpp[FxCop.Usage.ImplementISerializableCorrectly#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Usage.ImplementISerializableCorrectly/cpp/FxCop.Usage.ImplementISerializableCorrectly.cpp#1)]
 [!code-csharp[FxCop.Usage.ImplementISerializableCorrectly#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.ImplementISerializableCorrectly/cs/FxCop.Usage.ImplementISerializableCorrectly.cs#1)]
 [!code-vb[FxCop.Usage.ImplementISerializableCorrectly#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.ImplementISerializableCorrectly/vb/FxCop.Usage.ImplementISerializableCorrectly.vb#1)]

## <a name="example"></a>例
 次の例では、[GetObjectData] () の上書き可能な実装を指定することで、以前の2つの違反を修正します。<!-- TODO: review code entity reference <xref:assetId:///ISerializable.GetObjectData?qualifyHint=False&amp;autoUpgrade=False>  -->) の実装を提供します。 <!-- TODO: review code entity reference <xref:assetId:///ISerializable.GetObjectData?qualifyHint=False&amp;autoUpgrade=False>  --> ライブラリクラスで。

 [!code-cpp[FxCop.Usage.ImplementISerializableCorrectly2#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Usage.ImplementISerializableCorrectly2/cpp/FxCop.Usage.ImplementISerializableCorrectly2.cpp#1)]
 [!code-csharp[FxCop.Usage.ImplementISerializableCorrectly2#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.ImplementISerializableCorrectly2/cs/FxCop.Usage.ImplementISerializableCorrectly2.cs#1)]
 [!code-vb[FxCop.Usage.ImplementISerializableCorrectly2#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.ImplementISerializableCorrectly2/vb/FxCop.Usage.ImplementISerializableCorrectly2.vb#1)]

## <a name="related-rules"></a>関連規則
 [CA2236:ISerializable 型で基底クラス メソッドを呼び出します](../code-quality/ca2236-call-base-class-methods-on-iserializable-types.md)

 [CA2229:シリアル化コンストラクターを実装します](../code-quality/ca2229-implement-serialization-constructors.md)

 [CA2238:シリアル化メソッドを正しく実装します](../code-quality/ca2238-implement-serialization-methods-correctly.md)

 [CA2235:すべてのシリアル化不可能なフィールドを設定します](../code-quality/ca2235-mark-all-non-serializable-fields.md)

 [CA2237:ISerializable 型を SerializableAttribute に設定します](../code-quality/ca2237-mark-iserializable-types-with-serializableattribute.md)

 [CA2239:省略可能なフィールドに、逆シリアル化メソッドを指定します](../code-quality/ca2239-provide-deserialization-methods-for-optional-fields.md)

 [CA2120:シリアル化コンストラクターをセキュリティで保護します](../code-quality/ca2120-secure-serialization-constructors.md)
