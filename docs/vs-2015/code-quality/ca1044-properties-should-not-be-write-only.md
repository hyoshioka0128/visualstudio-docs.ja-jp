---
title: 'CA1044: プロパティを書き込み専用にすることはできません |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- PropertiesShouldNotBeWriteOnly
- CA1044
helpviewer_keywords:
- CA1044
- PropertiesShouldNotBeWriteOnly
ms.assetid: 8386bf3a-b161-4841-bf8b-92591595aea9
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 2ca0fb61c0973553ee6d410bc8b2718d19aeb28c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85546862"
---
# <a name="ca1044-properties-should-not-be-write-only"></a>CA1044:プロパティを書き込み専用にすることはできません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|PropertiesShouldNotBeWriteOnly|
|CheckId|CA1044|
|カテゴリ|Microsoft Design|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 パブリックまたはプロテクトプロパティに set アクセサーがありますが、get アクセサーがありません。

## <a name="rule-description"></a>ルールの説明
 Get アクセサーは、プロパティへの読み取りアクセスを提供し、set アクセサーは書き込みアクセスを提供します。 読み取り専用のプロパティは許容され、必要な場合もよくありますが、書き込み専用のプロパティを使用することはデザインのガイドラインで禁止されています。 これは、ユーザーが値を設定し、ユーザーが値を表示できないようにしても、セキュリティが確保されないためです。 また、読み取りアクセスがないと、共有オブジェクトのステータスを参照できないため、実用性が制限されます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、プロパティに get アクセサーを追加します。 または、書き込み専用プロパティの動作が必要な場合は、このプロパティをメソッドに変換することを検討してください。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告を抑制しないことを強くお勧めします。

## <a name="example"></a>例
 次の例で `BadClassWithWriteOnlyProperty` は、は書き込み専用プロパティを持つ型です。 `GoodClassWithReadWriteProperty` 修正されたコードが含まれています。

 [!code-csharp[FxCop.Design.PropertiesNotWriteOnly#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.PropertiesNotWriteOnly/cs/FxCop.Design.PropertiesNotWriteOnly.cs#1)]
 [!code-vb[FxCop.Design.PropertiesNotWriteOnly#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.PropertiesNotWriteOnly/vb/PropertiesNotWriteOnly.vb#1)]
