---
title: 'CA2229: シリアル化コンストラクターを実装します。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2229
- ImplementSerializationConstructors
helpviewer_keywords:
- CA2229
- ImplementSerializationConstructors
ms.assetid: 8e04d5fe-dfad-445a-972e-0648324fac45
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: ba654496d80654f0d9790a01bbc41326f7a5f13e
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85540492"
---
# <a name="ca2229-implement-serialization-constructors"></a>CA2229:シリアル化コンストラクターを実装します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|アイテム|値|
|-|-|
|TypeName|ImplementSerializationConstructors|
|CheckId|CA2229|
|カテゴリ|Microsoft. 使用方法|
|互換性に影響する変更点|中断なし|

## <a name="cause"></a>原因
 この型はインターフェイスを実装し <xref:System.Runtime.Serialization.ISerializable?displayProperty=fullName> 、はデリゲートまたはインターフェイスではなく、次のいずれかの条件に該当します。

- 型には、 <xref:System.Runtime.Serialization.SerializationInfo?displayProperty=fullName> オブジェクトと <xref:System.Runtime.Serialization.StreamingContext?displayProperty=fullName> オブジェクト (シリアル化コンストラクターのシグネチャ) を受け取るコンストラクターがありません。

- 型はシールされていません。シリアル化コンストラクターのアクセス修飾子は保護されていません (ファミリ)。

- 型が sealed で、シリアル化コンストラクターのアクセス修飾子がプライベートではありません。

## <a name="rule-description"></a>ルールの説明
 このルールは、カスタムシリアル化をサポートする型に関連しています。 型は、インターフェイスを実装する場合、カスタムシリアル化をサポート <xref:System.Runtime.Serialization.ISerializable> します。 シリアル化コンストラクターは、メソッドを使用してシリアル化されたオブジェクトを逆シリアル化または再作成するために必要です <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A?displayProperty=fullName> 。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、シリアル化コンストラクターを実装します。 シールされたクラスの場合、コンストラクターをプライベートにするか、プロテクトにします。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 規則違反を抑制しないでください。 この型は逆シリアル化ではなく、多くのシナリオでは機能しません。

## <a name="example"></a>例
 次の例は、ルールを満たす型を示しています。

 [!code-csharp[FxCop.Usage.ISerializableCtor#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.ISerializableCtor/cs/FxCop.Usage.ISerializableCtor.cs#1)]

## <a name="related-rules"></a>関連規則
 [CA2237:ISerializable 型を SerializableAttribute に設定します](../code-quality/ca2237-mark-iserializable-types-with-serializableattribute.md)

## <a name="see-also"></a>関連項目
 <xref:System.Runtime.Serialization.ISerializable?displayProperty=fullName> <xref:System.Runtime.Serialization.SerializationInfo?displayProperty=fullName>
 <xref:System.Runtime.Serialization.StreamingContext?displayProperty=fullName>
