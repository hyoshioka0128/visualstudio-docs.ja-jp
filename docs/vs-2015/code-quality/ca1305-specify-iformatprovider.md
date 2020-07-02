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
ms.openlocfilehash: 025d76f8e946dd3021141d6736c6b4bd40d57170
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85539087"
---
# <a name="ca1305-specify-iformatprovider"></a>CA1305:IFormatProvider を指定します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|アイテム|値|
|-|-|
|TypeName|SpecifyIFormatProvider|
|CheckId|CA1305|
|カテゴリ|Microsoft のグローバリゼーション|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 メソッドまたはコンストラクターが、パラメーターを受け取るオーバーロードを持つ1つ以上のメンバーを呼び出し <xref:System.IFormatProvider?displayProperty=fullName> ます。このメソッドまたはコンストラクターは、パラメーターを受け取るオーバーロードを呼び出しません <xref:System.IFormatProvider> 。 このルールは [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 、パラメーターを無視することによって説明されているメソッド <xref:System.IFormatProvider> の呼び出しと、さらに次のメソッドを無視します。

- <xref:System.Activator.CreateInstance%2A?displayProperty=fullName>

- <xref:System.Resources.ResourceManager.GetObject%2A?displayProperty=fullName>

- <xref:System.Resources.ResourceManager.GetString%2A?displayProperty=fullName>

## <a name="rule-description"></a>ルールの説明
 <xref:System.Globalization.CultureInfo?displayProperty=fullName>オブジェクトまたは <xref:System.IFormatProvider> オブジェクトが指定されていない場合、オーバーロードされたメンバーによって提供される既定値は、すべてのロケールで必要な結果を得られない可能性があります。 また、 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] メンバーは、コードに対して正しくない可能性がある仮定に基づいて、既定のカルチャと書式設定を選択します。 実際のシナリオに合わせてコードが期待どおりに動作することを確認するには、次のガイドラインに従って、カルチャ固有の情報を指定する必要があります。

- 値がユーザーに表示される場合は、現在のカルチャを使用します。 以下を参照してください。<xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=fullName>

- 値がソフトウェアによって保存およびアクセスされる (ファイルまたはデータベースに保存される) 場合は、インバリアントカルチャを使用します。 以下を参照してください。<xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName>

- 値の変換先がわからない場合は、データコンシューマーまたはプロバイダーによってカルチャが指定されていることを確認してください。

  <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName>は、クラスのインスタンスを使用してローカライズされたリソースを取得するためにのみ使用されることに注意 <xref:System.Resources.ResourceManager?displayProperty=fullName> してください。

  オーバーロードされたメンバーの既定の動作がニーズに適している場合でも、コードが自己文書化され、より簡単に管理できるように、カルチャ固有のオーバーロードを明示的に呼び出すことをお勧めします。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、またはを受け取るオーバーロードを使用して、 <xref:System.Globalization.CultureInfo> <xref:System.IFormatProvider> 前に示したガイドラインに従って引数を指定します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 既定のカルチャ/書式プロバイダーが適切な選択であり、コードの保守容易性が重要な開発の優先順位でない場合は、この規則からの警告を抑制することが安全です。

## <a name="example"></a>例
 次の例では、に `BadMethod` よってこの規則の2つの違反が発生します。 `GoodMethod`インバリアントカルチャをに渡して最初の違反を修正 <xref:System.String.Compare%2A> し、現在のカルチャをに渡して、2番目の違反を修正し <xref:System.String.ToLower%2A> `string3` ます。これは、がユーザーに表示されるためです。

 [!code-csharp[FxCop.Globalization.CultureInfo#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Globalization.CultureInfo/cs/FxCop.Globalization.CultureInfo.cs#1)]

## <a name="example"></a>例
 次の例で <xref:System.IFormatProvider> は、型によって選択された既定のに対する現在のカルチャの効果を示し <xref:System.DateTime> ます。

 [!code-csharp[FxCop.Globalization.IFormatProvider#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Globalization.IFormatProvider/cs/FxCop.Globalization.IFormatProvider.cs#1)]

 この例を実行すると、次の出力が生成されます。

 **6/4/1900 12:15:12 PM** 
**06/04/1900 12:15:12**
## <a name="related-rules"></a>関連規則
 [CA1304:CultureInfo を指定します](../code-quality/ca1304-specify-cultureinfo.md)

## <a name="see-also"></a>関連項目
 [NIB: CultureInfo クラスの使用](https://msdn.microsoft.com/d4329e34-64c3-4d1e-8c73-5b0ee626ba7a)
