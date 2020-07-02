---
title: 'CA1306: データ型のロケールを設定する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1306
- SetLocaleForDataTypes
helpviewer_keywords:
- CA1306
- SetLocaleForDataTypes
ms.assetid: 104297b2-5806-4de0-a8d9-c589380a796c
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: edd1d6a7623f96f03403883ee2585d245414bb3b
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85539023"
---
# <a name="ca1306-set-locale-for-data-types"></a>CA1306:データ型のロケールを設定します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|アイテム|値|
|-|-|
|TypeName|SetLocaleForDataTypes|
|CheckId|CA1306|
|カテゴリ|Microsoft のグローバリゼーション|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 メソッドまたはコンストラクターによって1つ以上のインスタンスが作成され、 <xref:System.Data.DataTable?displayProperty=fullName> <xref:System.Data.DataSet?displayProperty=fullName> locale プロパティ ( <xref:System.Data.DataTable.Locale%2A?displayProperty=fullName> または) が明示的に設定されていませんでした <xref:System.Data.DataSet.Locale%2A?displayProperty=fullName> 。

## <a name="rule-description"></a>ルールの説明
 ロケールによって、データのカルチャ固有のプレゼンテーション要素が決定されます。たとえば、数値、通貨記号、および並べ替え順序に使用する書式設定などです。 またはを作成する場合は、 <xref:System.Data.DataTable> <xref:System.Data.DataSet> ロケールを明示的に設定する必要があります。 既定では、これらの型のロケールは現在のカルチャです。 データベースまたはファイルに格納され、グローバルに共有されるデータの場合、ロケールは通常、インバリアントカルチャ () に設定する必要があり <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName> ます。 データがカルチャ間で共有されている場合、既定のロケールを使用すると、またはの内容が <xref:System.Data.DataTable> <xref:System.Data.DataSet> 正しく表示されたり解釈されたりする可能性があります。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、またはのロケールを明示的に設定し <xref:System.Data.DataTable> <xref:System.Data.DataSet> ます。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 ライブラリまたはアプリケーションが限定されたローカルユーザーを対象としている場合、データが共有されていない場合、または既定の設定により、サポートされているすべてのシナリオで望ましい動作が得られる場合は、この規則からの警告を抑制することが安全です。

## <a name="example"></a>例
 次の例では、2つの <xref:System.Data.DataTable> インスタンスを作成します。

 [!code-csharp[FxCop.Globalization.DataTable#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Globalization.DataTable/cs/FxCop.Globalization.DataTable.cs#1)]

## <a name="see-also"></a>関連項目
 <xref:System.Data.DataTable?displayProperty=fullName> <xref:System.Data.DataSet?displayProperty=fullName>
 <xref:System.Globalization.CultureInfo?displayProperty=fullName>
 <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName>
 <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName>
