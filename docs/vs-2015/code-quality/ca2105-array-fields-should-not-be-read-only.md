---
title: 'CA2105: 配列フィールドを読み取り専用にすることはできません |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2105
- ArrayFieldsShouldNotBeReadOnly
helpviewer_keywords:
- ArrayFieldsShouldNotBeReadOnly
- CA2105
ms.assetid: 0bdc3421-3ceb-4182-b30c-a992fbfcc35d
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: db52bf869642a5bdcc28eeb0792b295ae314a508
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85538672"
---
# <a name="ca2105-array-fields-should-not-be-read-only"></a>CA2105:配列フィールドを読み取り専用にすることはできません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|ArrayFieldsShouldNotBeReadOnly|
|CheckId|CA2105|
|カテゴリ|Microsoft.Security|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 配列を保持するパブリックまたはプロテクトフィールドが読み取り専用として宣言されています。

## <a name="rule-description"></a>ルールの説明
 `readonly` `ReadOnly` 配列を含むフィールドに (in) 修飾子を適用すると [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 、別の配列を参照するようにフィールドを変更することはできません。 ただし、読み取り専用フィールドに格納された配列の要素は変更できます。 パブリックにアクセスできる読み取り専用配列の要素に基づいて決定を行ったり、操作を実行したりするコードには、悪用可能なセキュリティ脆弱性が含まれている場合があります。

 パブリックフィールドを持つと、デザインルール CA1051 にも違反することに注意してください。 [表示インスタンスフィールドを宣言しません](../code-quality/ca1051-do-not-declare-visible-instance-fields.md)。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則によって識別されるセキュリティの脆弱性を修正するには、パブリックにアクセスできる読み取り専用配列の内容に依存しないでください。 次のいずれかの手順を使用することを強くお勧めします。

- 配列を、変更できない厳密に型指定されたコレクションに置き換えます。 詳細については、「<xref:System.Collections.ReadOnlyCollectionBase?displayProperty=fullName>」を参照してください。

- パブリックフィールドを、プライベート配列の複製を返すメソッドに置き換えます。 コードは複製に依存しないため、要素が変更されても危険はありません。

  2番目の方法を選択した場合は、フィールドをプロパティに置き換えることはできません。配列を返すプロパティは、パフォーマンスに悪影響を及ぼします。 詳細については、「 [CA1819: Properties は配列を返すことができません](../code-quality/ca1819-properties-should-not-return-arrays.md)」を参照してください。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 このルールからの警告の除外は避けることを強くお勧めします。 読み取り専用フィールドの内容が重要でない場合でも、ほとんどのシナリオは発生しません。 このような場合は、メッセージを除外するのではなく、修飾子を削除し `readonly` ます。

## <a name="example"></a>例
 この例は、このルールに違反する危険性を示しています。 最初の部分は、 `MyClassWithReadOnlyArrayField` セキュリティで保護されていない2つのフィールド (と) を含む型のライブラリの例を示してい `grades` `privateGrades` ます。 フィールドは `grades` パブリックであるため、任意の呼び出し元に対して脆弱です。 フィールドは `privateGrades` プライベートですが、メソッドによって呼び出し元に返されるため、まだ脆弱です `GetPrivateGrades` 。 フィールドは、 `securePrivateGrades` メソッドによって安全な方法で公開され `GetSecurePrivateGrades` ます。 このメソッドは、適切な設計手法に従うためにプライベートとして宣言されています。 2番目の部分は、メンバーとメンバーに格納されている値を変更するコードを示して `grades` `privateGrades` います。

 次の例では、クラスライブラリの例が表示されています。

 [!code-csharp[FxCop.Security.ArrayFieldsNotReadOnly#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.ArrayFieldsNotReadOnly/cs/FxCop.Security.ArrayFieldsNotReadOnly.cs#1)]

## <a name="example"></a>例
 次のコードでは、例のクラスライブラリを使用して、読み取り専用の配列のセキュリティの問題を示しています。

 [!code-csharp[FxCop.Security.TestArrayFieldsRead#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.TestArrayFieldsRead/cs/FxCop.Security.TestArrayFieldsRead.cs#1)]

 この例の出力は次のとおりです。

 **改ざん前: グレード:90、90、90プライベートグレード:90、90、90 Secure グレード、90、90、90** 
**改ざん後: グレード:90、555、90プライベートグレード:90、555、90 Secure グレード、90、90、90**
## <a name="see-also"></a>参照
 <xref:System.Array?displayProperty=fullName> <xref:System.Collections.ReadOnlyCollectionBase?displayProperty=fullName>
