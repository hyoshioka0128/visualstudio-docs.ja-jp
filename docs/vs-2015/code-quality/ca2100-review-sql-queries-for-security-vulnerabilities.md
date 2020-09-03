---
title: 'CA2100: セキュリティの脆弱性に対する SQL クエリを確認するMicrosoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- Review SQL queries for security vulnerabilities
- ReviewSqlQueriesForSecurityVulnerabilities
- CA2100
helpviewer_keywords:
- CA2100
- ReviewSqlQueriesForSecurityVulnerabilities
ms.assetid: 79670604-c02a-448d-9c0e-7ea0120bc5fe
caps.latest.revision: 26
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 797c071cdc74c36afeece304bfa4c708d7bf7147
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85521213"
---
# <a name="ca2100-review-sql-queries-for-security-vulnerabilities"></a>CA2100:SQL クエリのセキュリティ脆弱性を確認
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|ReviewSqlQueriesForSecurityVulnerabilities|
|CheckId|CA2100|
|カテゴリ|Microsoft.Security|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 メソッドは、 <xref:System.Data.IDbCommand.CommandText%2A?displayProperty=fullName> 文字列引数から構築された文字列をメソッドに使用して、プロパティを設定します。

## <a name="rule-description"></a>ルールの説明
 この規則では、文字列引数にユーザー入力が含まれていることが想定されています。 ユーザー入力から構築された SQL コマンド文字列には、SQL 注入攻撃に対する脆弱性があります。 SQL インジェクション攻撃では、悪意のあるユーザーが、基になるデータベースへの損傷または不正アクセスを試みるために、クエリのデザインを変更する入力を提供します。 一般的な手法としては、単一引用符またはアポストロフィの挿入があります。これは、SQL リテラル文字列の区切り記号です。2つのダッシュ。 SQL コメントを意味します。セミコロンは、新しいコマンドが続くことを示します。 ユーザー入力をクエリの一部にする必要がある場合は、次のいずれかの方法を使用して、攻撃のリスクを軽減します。

- ストアド プロシージャを使用します。

- パラメーター化されたコマンド文字列を使用します。

- コマンド文字列を作成する前に、型とコンテンツの両方についてユーザー入力を検証します。

  次の [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 型は、 <xref:System.Data.IDbCommand.CommandText%2A> プロパティを実装するか、文字列引数を使用してプロパティを設定するコンストラクターを提供します。

- <xref:System.Data.Odbc.OdbcCommand?displayProperty=fullName> および <xref:System.Data.Odbc.OdbcDataAdapter?displayProperty=fullName>

- <xref:System.Data.OleDb.OleDbCommand?displayProperty=fullName> および <xref:System.Data.OleDb.OleDbDataAdapter?displayProperty=fullName>

- <xref:System.Data.OracleClient.OracleCommand?displayProperty=fullName> および <xref:System.Data.OracleClient.OracleDataAdapter?displayProperty=fullName>

- [System.data.sqlserverce. SqlCeCommand](<!-- TODO: review code entity reference <xref:assetId:///System.Data.SqlServerCe.SqlCeCommand?qualifyHint=False&amp;autoUpgrade=True>  -->) と [System.data.sqlserverce. SqlCeDataAdapter] (<!-- TODO: review code entity reference <xref:assetId:///System.Data.SqlServerCe.SqlCeDataAdapter?qualifyHint=False&amp;autoUpgrade=True>  -->)

- <xref:System.Data.SqlClient.SqlCommand?displayProperty=fullName> および <xref:System.Data.SqlClient.SqlDataAdapter?displayProperty=fullName>

  型の ToString メソッドを明示的または暗黙的に使用してクエリ文字列を構築すると、この規則に違反することに注意してください。 以下に例を示します。

```
int x = 10;
string query = "SELECT TOP " + x.ToString() + " FROM Table";
```

 悪意のあるユーザーが ToString () メソッドをオーバーライドできるため、ルールに違反します。

 ToString を暗黙的に使用した場合も、規則に違反します。

```
int x = 10;
string query = String.Format("SELECT TOP {0} FROM Table", x);
```

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、パラメーター化クエリを使用します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 コマンドテキストにユーザー入力が含まれていない場合は、この規則による警告を抑制しても安全です。

## <a name="example"></a>例
 次の例は、パラメーター化されたコマンド文字列を使用して規則を満たす、規則に違反するメソッド、およびメソッドを示して `UnsafeQuery` `SaferQuery` います。

 [!code-cpp[FxCop.Security.ReviewSqlQueries#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Security.ReviewSqlQueries/cpp/FxCop.Security.ReviewSqlQueries.cpp#1)]
 [!code-csharp[FxCop.Security.ReviewSqlQueries#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.ReviewSqlQueries/cs/FxCop.Security.ReviewSqlQueries.cs#1)]
 [!code-vb[FxCop.Security.ReviewSqlQueries#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Security.ReviewSqlQueries/vb/FxCop.Security.ReviewSqlQueries.vb#1)]

## <a name="see-also"></a>参照
 [セキュリティの概要](https://msdn.microsoft.com/library/33e09965-61d5-48cc-9e8c-3b047cc4f194)
