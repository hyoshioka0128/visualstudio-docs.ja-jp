---
title: 'CA2137: Transparent メソッドは、検証可能な IL | を含む必要がありますMicrosoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2137
ms.assetid: cbaeb0e1-56b6-43b4-812a-596b2859c329
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 6219acde1f62c946e08325f4764dc49dde461d2f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85546576"
---
# <a name="ca2137-transparent-methods-must-contain-only-verifiable-il"></a>CA2137:透過的メソッドは、検証可能な IL のみを含まなければならない
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|TransparentMethodsMustBeVerifiable|
|CheckId|CA2137|
|カテゴリ|Microsoft.Security|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 メソッドに検証できないコードが含まれているか、メソッドから参照渡しで型が返されます。

## <a name="rule-description"></a>ルールの説明
 この規則は、透過的セキュリティ コードが、検証できない MSIL (Microsoft Intermediate Language) を実行しようとすると適用されます。 ただし、規則には完全な IL 検証ツールは含まれていないため、代わりにヒューリスティックを使用して、ほとんどの MSIL 検証違反が検出されます。

 コードに検証可能な MSIL だけが含まれていることを確認するには、アセンブリで [Peverify.exe (PEVerify Tool)](https://msdn.microsoft.com/library/f4f46f9e-8d08-4e66-a94b-0c69c9b0bbfa) を実行します。 **/Transparent**オプションを指定して PEVerify を実行します。これにより、エラーの原因となる、検証不可能な透過的なメソッドのみに出力が制限されます。 /Transparent オプションが使用されていない場合、PEVerify は検証不可能なコードを含めることが許可されている重要なメソッドも検証します。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、メソッドを <xref:System.Security.SecurityCriticalAttribute> 属性または属性でマークする <xref:System.Security.SecuritySafeCriticalAttribute> か、検証不可能なコードを削除します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。

## <a name="example"></a>例
 この例のメソッドは検証不可能なコードを使用し、属性または属性でマークする必要があり <xref:System.Security.SecurityCriticalAttribute> <xref:System.Security.SecuritySafeCriticalAttribute> ます。

 [!code-csharp[FxCop.Security.CA2137.TransparentMethodsMustBeVerifiable#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.security.ca2137.transparentmethodsmustbeverifiable/cs/ca2137 - transparentmethodsmustbeverifiable.cs#1)]
