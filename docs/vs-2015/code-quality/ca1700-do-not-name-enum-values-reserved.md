---
title: 'CA1700: 予約された&#39; | &#39;列挙値の名前を指定しないでくださいMicrosoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1700
- DoNotNameEnumValuesReserved
helpviewer_keywords:
- DoNotNameEnumValuesReserved
- CA1700
ms.assetid: 7a7e01c3-ae7d-4c82-a646-91b58864a749
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 57f2a2e5959860a99a921101ff5782f9bce9ace3
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545653"
---
# <a name="ca1700-do-not-name-enum-values-39reserved39"></a>CA1700: 予約された&#39; &#39;列挙値の名前を指定しません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|DoNotNameEnumValuesReserved|
|CheckId|CA1700|
|カテゴリ|Microsoft.Naming|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 列挙メンバーの名前に "reserved" という単語が含まれています。

## <a name="rule-description"></a>ルールの説明
 この規則では、"reserved" を含む名前の列挙体のメンバーは、現在使用されていなくても、将来的なバージョンでは名前を変更するか削除されるプレースホルダーと想定しています。 メンバーの名前変更や削除は、互換性に影響する変更点です。 メンバー名に "reserved" が含まれている場合や、ユーザーがドキュメントを読んだり順守したりすることはできないので、メンバーを無視することは避けてください。 さらに、予約されたメンバーはオブジェクトブラウザーおよびスマート統合開発環境に表示されるため、実際に使用されているメンバーについて混乱を招く可能性があります。

 予約されたメンバーを使用する代わりに、将来のバージョンで列挙に新しいメンバーを追加します。 ほとんどの場合、新しいメンバーを追加しても、元のメンバーの値が変更されない限り、互換性に影響する変更はありません。

 一部のケースでは、元のメンバーが元の値を保持している場合でも、メンバーの追加は互換性に影響する変更になります。 主に、 `switch` `Select` [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] メンバーリスト全体を包含し、既定のケースで例外をスローする戻り値に対して (in) ステートメントを使用する呼び出し元を中断することなく、既存のコードパスから新しいメンバーを返すことはできません。 2つ目の問題は、クライアントコードがなどのリフレクションメソッドからの動作の変更を処理しない可能性があることです <xref:System.Enum.IsDefined%2A?displayProperty=fullName> 。 したがって、新しいメンバーが既存のメソッドから返される必要がある場合、またはリフレクションの使用率が低いために互換性のない既知のアプリケーションが発生した場合、唯一の解決策は次のようになります。

1. 元のメンバーと新しいメンバーを含む新しい列挙を追加します。

2. 属性を使用して、元の列挙体をマークし <xref:System.ObsoleteAttribute?displayProperty=fullName> ます。

   元の列挙体を公開する外部から参照できる型またはメンバーについても、同じ手順を実行します。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、メンバーを削除するか、名前を変更します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 現在使用されているメンバー、または以前に出荷されたライブラリに対しては、この規則による警告を抑制することが安全です。

## <a name="related-rules"></a>関連規則
 [CA2217:列挙型を FlagsAttribute に設定しません](../code-quality/ca2217-do-not-mark-enums-with-flagsattribute.md)

 [CA1712:列挙型値を型名のプレフィックスにしません](../code-quality/ca1712-do-not-prefix-enum-values-with-type-name.md)

 [CA1028:列挙ストレージは Int32 でなければなりません](../code-quality/ca1028-enum-storage-should-be-int32.md)

 [CA1008:Enums は 0 値を含んでいなければなりません](../code-quality/ca1008-enums-should-have-zero-value.md)

 [CA1027:列挙型を FlagsAttribute に設定します](../code-quality/ca1027-mark-enums-with-flagsattribute.md)
