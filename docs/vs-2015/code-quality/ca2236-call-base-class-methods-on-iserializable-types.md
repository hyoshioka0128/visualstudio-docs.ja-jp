---
title: 'CA2236: ISerializable 型で基底クラスのメソッドを呼び出します |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2236
- CallBaseClassMethodsOnISerializableTypes
helpviewer_keywords:
- CA2236
- CallBaseClassMethodsOnISerializableTypes
ms.assetid: 5a15b20d-769c-4640-b31a-36e07077daae
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: a03192ac8a5b59558dc39a32f55e8177dc249365
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85545185"
---
# <a name="ca2236-call-base-class-methods-on-iserializable-types"></a>CA2236:ISerializable 型で基底クラス メソッドを呼び出します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|CallBaseClassMethodsOnISerializableTypes|
|CheckId|CA2236|
|カテゴリ|Microsoft. 使用方法|
|互換性に影響する変更点|中断なし|

## <a name="cause"></a>原因
 型は、インターフェイスを実装する型から派生 <xref:System.Runtime.Serialization.ISerializable?displayProperty=fullName> し、次の条件のいずれかが当てはまります。

- この型は、シリアル化コンストラクターを実装します。これは、パラメーターシグネチャを持つコンストラクターです <xref:System.Runtime.Serialization.SerializationInfo?displayProperty=fullName> <xref:System.Runtime.Serialization.StreamingContext?displayProperty=fullName> が、基本型のシリアル化コンストラクターを呼び出しません。

- 型はメソッドを実装し <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A?displayProperty=fullName> ますが、 <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A> 基本型のメソッドを呼び出しません。

## <a name="rule-description"></a>ルールの説明
 カスタムのシリアル化プロセスでは、型は <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A> そのフィールドをシリアル化するメソッドと、フィールドを逆シリアル化するためのシリアル化コンストラクターを実装します。 型がインターフェイスを実装する型から派生している場合は、基本型 <xref:System.Runtime.Serialization.ISerializable> <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A> のフィールドをシリアル化/逆シリアル化するために、基本型のメソッドおよびシリアル化コンストラクターを呼び出す必要があります。 それ以外の場合、型はシリアル化されず、正しくシリアル化解除されません。 派生型で新しいフィールドが追加されない場合、型は <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A> メソッドもシリアル化コンストラクターも実装したり、同等の基本型を呼び出したりする必要がないことに注意してください。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、 <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A> 対応する派生型のメソッドまたはコンストラクターから基本型のメソッドまたはシリアル化コンストラクターを呼び出します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。

## <a name="example"></a>例
 次の例は、基底クラスのシリアル化コンストラクターとメソッドを呼び出すことによって、規則を満たす派生型を示して <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A> います。

 [!code-csharp[FxCop.Usage.CallBaseISerializable#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.CallBaseISerializable/cs/FxCop.Usage.CallBaseISerializable.cs#1)]
 [!code-vb[FxCop.Usage.CallBaseISerializable#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.CallBaseISerializable/vb/FxCop.Usage.CallBaseISerializable.vb#1)]

## <a name="related-rules"></a>関連規則
 [CA2240:ISerializable を正しく実装します](../code-quality/ca2240-implement-iserializable-correctly.md)

 [CA2229:シリアル化コンストラクターを実装します](../code-quality/ca2229-implement-serialization-constructors.md)

 [CA2238:シリアル化メソッドを正しく実装します](../code-quality/ca2238-implement-serialization-methods-correctly.md)

 [CA2235:すべてのシリアル化不可能なフィールドを設定します](../code-quality/ca2235-mark-all-non-serializable-fields.md)

 [CA2237:ISerializable 型を SerializableAttribute に設定します](../code-quality/ca2237-mark-iserializable-types-with-serializableattribute.md)

 [CA2239:省略可能なフィールドに、逆シリアル化メソッドを指定します](../code-quality/ca2239-provide-deserialization-methods-for-optional-fields.md)

 [CA2120:シリアル化コンストラクターをセキュリティで保護します](../code-quality/ca2120-secure-serialization-constructors.md)
