---
title: 'CA2124: 脆弱性のある finally 句を外側の try | でラップします。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2124
- WrapVulnerableFinallyClausesInOuterTry
helpviewer_keywords:
- CA2124
- WrapVulnerableFinallyClausesInOuterTry
ms.assetid: 82efd224-9e60-4b88-a0f5-dfabcc49a254
caps.latest.revision: 22
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 4e191ca10456f133e1213961ca2d1ed9cb8e040b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85544301"
---
# <a name="ca2124-wrap-vulnerable-finally-clauses-in-outer-try"></a>CA2124:脆弱性のある finally 句を外側の try でラップします
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|WrapVulnerableFinallyClausesInOuterTry|
|CheckId|CA2124|
|カテゴリ|Microsoft.Security|
|互換性に影響する変更点|中断なし|

## <a name="cause"></a>原因
 のバージョン1.0 および1.1 では [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 、パブリックメソッドまたはプロテクトメソッドにブロックが含まれてい `try` / `catch` / `finally` ます。 `finally`ブロックがセキュリティ状態をリセットしているように見えますが、ブロックで囲まれていません `finally` 。

## <a name="rule-description"></a>ルールの説明
 この規則で `try` / `finally` は、 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 呼び出し履歴に存在する悪意のある例外フィルターに対して脆弱である可能性のあるのバージョン1.0 および1.1 を対象とするコード内のブロックを検索します。 偽装などの機密性の高い操作が try ブロックで発生し、例外がスローされた場合は、ブロックの前にフィルターを実行でき `finally` ます。 偽装の例では、これは、フィルターが権限を借用したユーザーとして実行されることを意味します。 現在、フィルターは Visual Basic のみで実装できます。

> [!WARNING]
> のバージョン2.0 以降では [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 、 `try` / `catch` /  `finally` 例外ブロックを含むメソッド内でリセットが直接行われた場合、ランタイムは悪意のある例外フィルターからブロックを自動的に保護します。

## <a name="how-to-fix-violations"></a>違反の修正方法
 ラップされ `try` / `finally` ていないを外側の try ブロックに配置します。 次の2番目の例を参照してください。 これにより、は、 `finally` フィルターコードの前にを強制的に実行します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。

## <a name="pseudo-code-example"></a>擬似コードの例

### <a name="description"></a>説明
 次の擬似コードでは、このルールにより検出されたパターンを示しています。

### <a name="code"></a>コード

```
try {
   // Do some work.
   Impersonator imp = new Impersonator("John Doe");
   imp.AddToCreditCardBalance(100);
}
finally {
   // Reset security state.
   imp.Revert();
}
```

## <a name="example"></a>例
 次の擬似コードは、コードを保護し、この規則を満たすために使用できるパターンを示しています。

```
try {
     try {
        // Do some work.
     }
     finally {
        // Reset security state.
     }
}
catch()
{
    throw;
}
```
