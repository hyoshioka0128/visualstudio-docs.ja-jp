---
title: 'CA2149: Transparent メソッドはネイティブコード | を呼び出すことはできません。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2149
ms.assetid: 28951bd7-f3db-4871-99aa-bad68d1ead80
caps.latest.revision: 13
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 5c1e254ae7912efbb6773155ed834e54a1db1832
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546329"
---
# <a name="ca2149-transparent-methods-must-not-call-into-native-code"></a>CA2149:透過的メソッドは、ネイティブ コード内に呼び出しを行ってはならない
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|TransparentMethodsMustNotCallNativeCode|
|CheckId|CA2149|
|カテゴリ|Microsoft.Security|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 メソッドは、P/Invoke などのメソッドスタブを介してネイティブ関数を呼び出します。

## <a name="rule-description"></a>ルールの説明
 この規則は、P/Invoke などを使用してネイティブ コードを直接呼び出すすべての透過的メソッドに対して適用されます。 この規則を違反すると、 <xref:System.MethodAccessException> レベル2の透過性モデルのになり、レベル1の透過性モデルのに対する完全な要求が発生し <xref:System.Security.Permissions.SecurityPermissionAttribute.UnmanagedCode%2A> ます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、ネイティブコードを呼び出すメソッドを、 <xref:System.Security.SecurityCriticalAttribute> 属性または属性でマークし <xref:System.Security.SecuritySafeCriticalAttribute> ます。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。

## <a name="example"></a>例
 [!code-csharp[FxCop.Security.CA2149.TransparentMethodsMustNotCallNativeCode#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.security.ca2149.transparentmethodsmustnotcallnativecode/cs/ca2149 - transparentmethodsmustnotcallnativecode.cs#1)]
