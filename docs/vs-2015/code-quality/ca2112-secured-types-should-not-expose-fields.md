---
title: 'CA2112: セキュリティで保護された型はフィールドを公開できません |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2112
- SecuredTypesShouldNotExposeFields
helpviewer_keywords:
- SecuredTypesShouldNotExposeFields
- CA2112
ms.assetid: 9eb13a78-3487-49f2-81d1-3c3866db132f
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 4267b4f55f78106a4d1e8f3b2f9b296be9ddf618
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85546537"
---
# <a name="ca2112-secured-types-should-not-expose-fields"></a>CA2112:セキュリティで保護された型はフィールドを公開してはなりません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|SecuredTypesShouldNotExposeFields|
|CheckId|CA2112|
|カテゴリ|Microsoft.Security|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 パブリックまたはプロテクト型にはパブリックフィールドが含まれ、 [リンク確認要求](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d)によってセキュリティ保護されます。

## <a name="rule-description"></a>ルールの説明
 リンク確認要求で保護されている型のインスタンスに対するアクセス権がコードにある場合、その型のフィールドにアクセスするためにリンク確認要求に適合する必要はありません。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、フィールドを非パブリックにし、フィールドデータを返すパブリックプロパティまたはメソッドを追加します。 型の LinkDemand セキュリティチェックは、型のプロパティとメソッドへのアクセスを保護します。 ただし、コードアクセスセキュリティはフィールドには適用されません。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 セキュリティの問題と優れた設計の両方で、パブリックフィールドを非公開にすることで、違反を修正する必要があります。 セキュリティで保護されたままにする必要がある情報をフィールドに保持しておらず、フィールドの内容に依存していない場合は、この規則からの警告を抑制できます。

## <a name="example"></a>例
 次の例は、セキュリティで保護されていないフィールドを持つライブラリ型 () で構成されています `SecuredTypeWithFields` 。型 () は、 `Distributor` ライブラリ型のインスタンスを作成することができます。また、型のインスタンスを作成するアクセス許可がない型 () と、インスタンスのフィールドを読み取ることができるアプリケーションコードもあります。

 次のライブラリコードは規則に違反しています。

 [!code-csharp[FxCop.Security.LinkDemandOnField#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.LinkDemandOnField/cs/FxCop.Security.LinkDemandOnField.cs#1)]

## <a name="example"></a>例
 アプリケーションでは、セキュリティで保護された型を保護するリンク確認要求のためにインスタンスを作成できません。 アプリケーションがセキュリティで保護された型のインスタンスを取得できるようにするクラスを次に示します。

 [!code-csharp[FxCop.Security.LDOnFieldsDistributor#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.LDOnFieldsDistributor/cs/FxCop.Security.LDOnFieldsDistributor.cs#1)]

## <a name="example"></a>例
 次のアプリケーションは、セキュリティで保護された型のメソッドにアクセスする権限を持たない場合に、コードからそのフィールドにアクセスできるようにする方法を示しています。

 [!code-csharp[FxCop.Security.TestLinkDemandOnFields#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.TestLinkDemandOnFields/cs/FxCop.Security.TestLinkDemandOnFields.cs#1)]

 この例を実行すると、次の出力が生成されます。

 **SecuredTypeWithFields のインスタンスを作成しています。** 
セキュリティで保護された**型のフィールド:22、33** 
セキュリティで保護された**型のフィールドを変更しています...** 
キャッシュされた**オブジェクトフィールド:99、33**
## <a name="related-rules"></a>関連規則
 [CA1051:参照可能なインスタンス フィールドを宣言しません](../code-quality/ca1051-do-not-declare-visible-instance-fields.md)

## <a name="see-also"></a>参照
 [リンク確認要求](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d)[のデータとモデリング](https://msdn.microsoft.com/library/8c37635d-e2c1-4b64-a258-61d9e87405e6)
