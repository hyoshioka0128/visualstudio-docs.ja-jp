---
title: 'CA1711: 識別子は正しくないサフィックス | を含むことはできませんMicrosoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1711
- IdentifiersShouldNotHaveIncorrectSuffix
helpviewer_keywords:
- CA1711
- IdentifiersShouldNotHaveIncorrectSuffix
ms.assetid: a63359ab-386d-44ae-b381-ee3a983aca29
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 1e753083e9b4bda1e33553021ccb0027a2af2533
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85544015"
---
# <a name="ca1711-identifiers-should-not-have-incorrect-suffix"></a>CA1711:識別子は、不適切なサフィックスを含むことはできません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|IdentifiersShouldNotHaveIncorrectSuffix|
|CheckId|CA1711|
|カテゴリ|Microsoft.Naming|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 識別子のサフィックスが不適切です。

## <a name="rule-description"></a>ルールの説明
 規則では、特定の基本型を拡張する型、特定のインターフェイスを実装する型、またはそのような型から派生した型の名前にのみ、固有の予約済みサフィックスを末尾に付けます。 その他の型名では、予約済みのサフィックスを使用しないでください。

 予約済みのサフィックス、および関連付けられている基本型とインターフェイスを次の表に示します。

|サフィックス|基本型/インターフェイス|
|------------|--------------------------|
|属性|<xref:System.Attribute?displayProperty=fullName>|
|コレクション|<xref:System.Collections.ICollection?displayProperty=fullName><br /><br /> <xref:System.Collections.IEnumerable?displayProperty=fullName><br /><br /> <xref:System.Collections.Queue?displayProperty=fullName><br /><br /> <xref:System.Collections.Stack?displayProperty=fullName><br /><br /> <xref:System.Collections.Generic.ICollection%601?displayProperty=fullName><br /><br /> <xref:System.Data.DataSet?displayProperty=fullName><br /><br /> <xref:System.Data.DataTable?displayProperty=fullName>|
|Dictionary|<xref:System.Collections.IDictionary?displayProperty=fullName><br /><br /> <xref:System.Collections.Generic.IDictionary%602?displayProperty=fullName>|
|EventArgs|<xref:System.EventArgs?displayProperty=fullName>|
|EventHandler|イベント ハンドラーのデリゲート|
|例外|<xref:System.Exception?displayProperty=fullName>|
|権限|<xref:System.Security.IPermission?displayProperty=fullName>|
|キュー|<xref:System.Collections.Queue?displayProperty=fullName>|
|スタック|<xref:System.Collections.Stack?displayProperty=fullName>|
|ストリーム|<xref:System.IO.Stream?displayProperty=fullName>|

 また、次のサフィックスは使用 **しない** でください。

- 代理人

- 列挙型

- Impl – 代わりに ”Core” を使用します。

- 型を以前のバージョンと区別するための Ex または類似のサフィックス

  名前付け規則では、共通言語ランタイムをターゲットとするライブラリの統一的な名前の付け方が規定されています。 これにより、新しいソフトウェア ライブラリを習得するまでの時間を短縮でき、マネージド コード開発の専門家によってライブラリが開発されたという信頼を顧客に与えることができます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 型名からサフィックスを削除します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 アプリケーション ドメインでサフィックスに明確な意味がある場合を除き、この規則による警告を抑制しないでください。

## <a name="related-rules"></a>関連規則
 [CA1710:識別子は、正しいサフィックスを含んでいなければなりません](../code-quality/ca1710-identifiers-should-have-correct-suffix.md)

## <a name="see-also"></a>参照
 [属性](https://msdn.microsoft.com/library/ee0038ef-b247-4747-a650-3c5c5cd58d8b) [NIB: イベントとデリゲート](https://msdn.microsoft.com/d98fd58b-fa4f-4598-8378-addf4355a115)
