---
title: 'CA2114: メソッドのセキュリティは、型 | のスーパーセットである必要がありますMicrosoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- MethodSecurityShouldBeASupersetOfType
- CA2114
helpviewer_keywords:
- CA2114
- MethodSecurityShouldBeASupersetOfType
ms.assetid: 663f7aa4-8be5-4bd5-be92-4e9444f07077
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: d7879d8b2aa9eb4ece1ce07f89681b6c0b0f5f31
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85534707"
---
# <a name="ca2114-method-security-should-be-a-superset-of-type"></a>CA2114:メソッド セキュリティは型のスーパーセットでなければなりません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|アイテム|値|
|-|-|
|TypeName|MethodSecurityShouldBeASupersetOfType|
|CheckId|CA2114|
|カテゴリ|Microsoft.Security|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 型には宣言セキュリティがあり、そのメソッドの1つには同じセキュリティアクションの宣言セキュリティがあり、セキュリティアクションは[リンク](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d)確認要求または[継承要求](https://msdn.microsoft.com/28b9adbb-8f08-4f10-b856-dbf59eb932d9)ではありません。また、型によってチェックされるアクセス許可は、メソッドによってチェックされるアクセス許可のサブセットではありません。

## <a name="rule-description"></a>ルールの説明
 メソッドは、同じアクションに対して、メソッドレベルと型レベルの宣言セキュリティの両方を持つことはできません。 2つのチェックは結合されません。メソッドレベルの要求だけが適用されます。 たとえば、型がアクセス許可を要求 `X` し、そのメソッドの1つがアクセス許可を要求する場合、コードには `Y` メソッドを実行するアクセス許可が必要ありません `X` 。

## <a name="how-to-fix-violations"></a>違反の修正方法
 コードを確認して、両方のアクションが必要であることを確認します。 両方のアクションが必要な場合は、メソッドレベルのアクションに、型レベルで指定されたセキュリティが含まれていることを確認してください。 たとえば、型がアクセス許可を要求 `X` し、そのメソッドがアクセス許可を要求する必要がある場合、 `Y` メソッドはとを明示的に要求する必要があり `X` `Y` ます。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 メソッドが型によって指定されたセキュリティを必要としない場合は、この規則による警告を抑制しても安全です。 ただし、これは通常のシナリオではなく、慎重な設計レビューが必要であることを示している可能性があります。

## <a name="example"></a>例
 次の例では、環境のアクセス許可を使用して、この規則に違反する危険性を示します。 この例では、アプリケーションコードは、型に必要なアクセス許可を拒否する前に、セキュリティで保護された型のインスタンスを作成します。 実際の脅威のシナリオでは、アプリケーションでオブジェクトのインスタンスを取得する別の方法が必要になります。

 次の例では、ライブラリは、型に対する書き込みアクセス許可と、メソッドに対する読み取りアクセス許可を要求します。

 [!code-csharp[FxCop.Security.MethodLevelSecurity#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.MethodLevelSecurity/cs/FxCop.Security.MethodLevelSecurity.cs#1)]

## <a name="example"></a>例
 次のアプリケーションコードは、型レベルのセキュリティ要件を満たしていない場合でも、メソッドを呼び出すことによって、ライブラリの脆弱性を示しています。

 [!code-csharp[FxCop.Security.TestMethodLevelSecurity#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.TestMethodLevelSecurity/cs/FxCop.Security.TestMethodLevelSecurity.cs#1)]

 この例を実行すると、次の出力が生成されます。

 **[すべてのアクセス許可] 個人情報: 6/16/1964 12:00:00 AM** 
 **[書き込みアクセス許可がありません (型によって要求されます)] 個人情報: 6/16/1964 12:00:00 AM** 
 **[読み取りアクセス許可がありません (メソッドによって要求されました)] 個人情報にアクセスできませんでした。要求が失敗しました。**
## <a name="see-also"></a>関連項目
 [セキュリティで保護されたコーディングガイドライン](https://msdn.microsoft.com/library/4f882d94-262b-4494-b0a6-ba9ba1f5f177)の[継承要求](https://msdn.microsoft.com/28b9adbb-8f08-4f10-b856-dbf59eb932d9)の[リンク要求](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d)[データとモデリング](https://msdn.microsoft.com/library/8c37635d-e2c1-4b64-a258-61d9e87405e6)
