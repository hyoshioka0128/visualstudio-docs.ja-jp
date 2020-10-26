---
title: 'CA1019: 属性引数にアクセサーを定義します。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1019
- DefineAccessorsForAttributeArguments
helpviewer_keywords:
- CA1019
- DefineAccessorsForAttributeArguments
ms.assetid: 197f2378-3c43-427e-80de-9ec25006c05c
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: ec9be9dae502ec48570a85576f483518ed0d75d6
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85534954"
---
# <a name="ca1019-define-accessors-for-attribute-arguments"></a>CA1019:属性引数にアクセサーを定義します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|DefineAccessorsForAttributeArguments|
|CheckId|CA1019|
|カテゴリ|Microsoft Design|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 コンストラクターでは、属性は対応するプロパティを持たない引数を定義します。

## <a name="rule-description"></a>ルールの説明
 属性では、対象に適用するときに必ず指定する必須の引数を定義できます。 この引数は、コンストラクターに位置指定パラメーターで属性を指定できるようになるため、位置指定引数とも呼ばれます。 必須のすべての引数について、対応する読み取り専用のプロパティも属性で規定する必要があります。これは、引数値を実行時に取得できるようにするためです。 このルールでは、各コンストラクターパラメーターに対応するプロパティが定義されていることを確認します。

 また、属性ではオプションの引数も定義できます。これは名前付き引数とも呼ばれます。 この引数は、名前でコンストラクターに属性を指定するときに使用されます。また、対応する読み取り/書き込みプロパティが必要です。

 必須および省略可能な引数については、対応するプロパティとコンストラクターパラメーターで同じ名前を使用する必要がありますが、大文字と小文字は区別されません。 プロパティは Pascal 形式の大文字と小文字を使用し、パラメーターは camel 形式を使用します。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、1つも含まれていない各コンストラクターパラメーターに読み取り専用プロパティを追加します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 必須の引数の値を取得可能にしない場合は、この規則からの警告を非表示にします。

## <a name="custom-attributes-example"></a>カスタム属性の例

### <a name="description"></a>説明
 次の例は、必須 (位置指定) パラメーターを定義する2つの属性を示しています。 属性の最初の実装が正しく定義されていません。 2番目の実装は正しい方法です。

### <a name="code"></a>コード
 [!code-csharp[FxCop.Design.AttributeAccessors#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.AttributeAccessors/cs/FxCop.Design.AttributeAccessors.cs#1)]
 [!code-vb[FxCop.Design.AttributeAccessors#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.AttributeAccessors/vb/FxCop.Design.AttributeAccessors.vb#1)]

## <a name="positional-and-named-arguments"></a>位置指定引数と名前付き引数

### <a name="description"></a>説明
 位置指定引数と名前付き引数を使用すると、ライブラリのコンシューマーに対して、属性に必須の引数と省略可能な引数を明確にすることができます。

 次の例は、位置指定引数と名前付き引数の両方を持つ属性の実装を示しています。

### <a name="code"></a>コード
 [!code-csharp[FxCop.Design.AttributeAccessorsNamed#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.AttributeAccessorsNamed/cs/FxCop.Design.AttributeAccessorsNamed.cs#1)]

### <a name="comments"></a>コメント
 次の例は、カスタム属性を2つのプロパティに適用する方法を示しています。

### <a name="code"></a>コード
 [!code-csharp[FxCop.Design.AttributeAccessorsNamedApplied#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.AttributeAccessorsNamedApplied/cs/FxCop.Design.AttributeAccessorsNamedApplied.cs#1)]

## <a name="related-rules"></a>関連規則
 [CA1813:アンシールド属性を使用しません](../code-quality/ca1813-avoid-unsealed-attributes.md)

## <a name="see-also"></a>参照
 [属性](https://msdn.microsoft.com/library/ee0038ef-b247-4747-a650-3c5c5cd58d8b)
