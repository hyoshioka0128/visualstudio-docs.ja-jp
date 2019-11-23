---
title: 'CA1305: IFormatProvider | を指定します。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- SpecifyIFormatProvider
- CA1305
helpviewer_keywords:
- CA1305
- SpecifyIFormatProvider
ms.assetid: fb34ed9a-4eab-47cc-8eef-3068a4a1397e
caps.latest.revision: 24
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 299e8bfec526dc3a5e8dc166d9ab405d51037cbe
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72661435"
---
# <a name="ca1305-specify-iformatprovider"></a>CA1305: IFormatProvider を指定します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|SpecifyIFormatProvider|
|CheckId|CA1305|
|カテゴリ|Microsoft のグローバリゼーション|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 メソッドまたはコンストラクターが、<xref:System.IFormatProvider?displayProperty=fullName> パラメーターを受け入れるオーバーロードを持つ1つ以上のメンバーを呼び出します。メソッドまたはコンストラクターは、<xref:System.IFormatProvider> パラメーターを受け取るオーバーロードを呼び出しません。 このルールは、<xref:System.IFormatProvider> パラメーターを無視するように記述された [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] メソッドの呼び出しと、さらに次のメソッドを無視します。

- <xref:System.Activator.CreateInstance%2A?displayProperty=fullName>

- <xref:System.Resources.ResourceManager.GetObject%2A?displayProperty=fullName>

- <xref:System.Resources.ResourceManager.GetString%2A?displayProperty=fullName>

## <a name="rule-description"></a>規則の説明
 <xref:System.Globalization.CultureInfo?displayProperty=fullName> オブジェクトまたは <xref:System.IFormatProvider> オブジェクトが指定されていない場合、オーバーロードされたメンバーによって提供される既定値は、すべてのロケールで必要な結果を得られない可能性があります。 また、[!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] メンバーは、コードに対して正しくない可能性がある仮定に基づいて、既定のカルチャと書式設定を選択します。 実際のシナリオに合わせてコードが期待どおりに動作することを確認するには、次のガイドラインに従って、カルチャ固有の情報を指定する必要があります。

- 値がユーザーに表示される場合は、現在のカルチャを使用します。 「<xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=fullName>」を参照してください。

- 値がソフトウェアによって保存およびアクセスされる (ファイルまたはデータベースに保存される) 場合は、インバリアントカルチャを使用します。 「<xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName>」を参照してください。

- 値の変換先がわからない場合は、データコンシューマーまたはプロバイダーによってカルチャが指定されていることを確認してください。

  <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName> は、<xref:System.Resources.ResourceManager?displayProperty=fullName> クラスのインスタンスを使用してローカライズされたリソースを取得するためにのみ使用されることに注意してください。

  オーバーロードされたメンバーの既定の動作がニーズに適している場合でも、コードが自己文書化され、より簡単に管理できるように、カルチャ固有のオーバーロードを明示的に呼び出すことをお勧めします。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、<xref:System.Globalization.CultureInfo> または <xref:System.IFormatProvider> を受け取るオーバーロードを使用して、前に示したガイドラインに従って引数を指定します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 既定のカルチャ/書式プロバイダーが適切な選択であり、コードの保守容易性が重要な開発の優先順位でない場合は、この規則からの警告を抑制することが安全です。

## <a name="example"></a>例
 次の例では、`BadMethod` によってこの規則の2つの違反が発生します。 `GoodMethod` は、インバリアントカルチャを <xref:System.String.Compare%2A>に渡して最初の違反を修正し、`string3` がユーザーに表示されるため、現在のカルチャを <xref:System.String.ToLower%2A> に渡すことによって2番目の違反を修正します。

 [!code-csharp[FxCop.Globalization.CultureInfo#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Globalization.CultureInfo/cs/FxCop.Globalization.CultureInfo.cs#1)]

## <a name="example"></a>例
 次の例は、<xref:System.DateTime> の種類によって選択された既定の <xref:System.IFormatProvider> に対する現在のカルチャの効果を示しています。

 [!code-csharp[FxCop.Globalization.IFormatProvider#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Globalization.IFormatProvider/cs/FxCop.Globalization.IFormatProvider.cs#1)]

 この例を実行すると、次の出力が生成されます。

 **6/4/1900 12:15:12 PM**
**06/04/1900 12:15:12**
## <a name="related-rules"></a>関連規則
 [CA1304: CultureInfo を指定します](../code-quality/ca1304-specify-cultureinfo.md)

## <a name="see-also"></a>関連項目
 [NIB: CultureInfo クラスの使用](https://msdn.microsoft.com/d4329e34-64c3-4d1e-8c73-5b0ee626ba7a)
