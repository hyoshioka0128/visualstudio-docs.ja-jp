---
title: 'CA1302: ロケール固有の文字列をハードコーディングしない |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- DoNotHardcodeLocaleSpecificStrings
- CA1302
helpviewer_keywords:
- DoNotHardcodeLocaleSpecificStrings
- CA1302
ms.assetid: 05ed134a-837d-43d7-bf97-906edeac44ce
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 18da0471b1ac62f0e61b303c60b46c15cdc2e428
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85539010"
---
# <a name="ca1302-do-not-hardcode-locale-specific-strings"></a>CA1302:ロケール特有の文字列をハードコードしません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|DoNotHardcodeLocaleSpecificStrings|
|CheckId|CA1302|
|カテゴリ|Microsoft のグローバリゼーション|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 メソッドは、特定のシステムフォルダーのパスの一部を表す文字列リテラルを使用します。

## <a name="rule-description"></a>ルールの説明
 列挙には、 <xref:System.Environment.SpecialFolder?displayProperty=fullName> 特別なシステムフォルダーを参照するメンバーが含まれています。 これらのフォルダーの場所は、オペレーティングシステムごとに異なる値を持つことができ、ユーザーは一部の場所を変更することができ、場所はローカライズされます。 特別なフォルダーの例としては、システムフォルダーがあります。このフォルダーは、では "C:\WINDOWS\system32" になりますが、 [!INCLUDE[winxp](../includes/winxp-md.md)] では "C:\WINNT\system32" です [!INCLUDE[win2kfamily](../includes/win2kfamily-md.md)] 。 メソッドは、 <xref:System.Environment.GetFolderPath%2A?displayProperty=fullName> 列挙体に関連付けられた場所を返し <xref:System.Environment.SpecialFolder> ます。 によって返される場所は <xref:System.Environment.GetFolderPath%2A> ローカライズされ、現在実行中のコンピューターに適しています。

 この規則は、メソッドを使用して取得されたフォルダーパスを <xref:System.Environment.GetFolderPath%2A> 別のディレクトリレベルにトークン化します。 各文字列リテラルは、トークンと比較されます。 一致が見つかった場合は、メソッドが、トークンに関連付けられているシステムの場所を参照する文字列を構築していることを前提としています。 移植性とローカライズ性を確保するには、 <xref:System.Environment.GetFolderPath%2A> 文字列リテラルを使用する代わりに、メソッドを使用して特殊なシステムフォルダーの場所を取得します。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、メソッドを使用して場所を取得し <xref:System.Environment.GetFolderPath%2A> ます。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 列挙体に関連付けられているシステムの場所の1つを参照するために文字列リテラルが使用されていない場合は、この規則による警告を抑制しても安全です <xref:System.Environment.SpecialFolder> 。

## <a name="example"></a>例
 次の例では、common application data フォルダーのパスを構築します。これにより、このルールから3つの警告が生成されます。 次に、メソッドを使用してパスを取得し <xref:System.Environment.GetFolderPath%2A> ます。

 [!code-csharp[FxCop.Globalization.HardcodedLocaleStrings#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Globalization.HardcodedLocaleStrings/cs/FxCop.Globalization.HardcodedLocaleStrings.cs#1)]
 [!code-vb[FxCop.Globalization.HardcodedLocaleStrings#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Globalization.HardcodedLocaleStrings/vb/FxCop.Globalization.HardcodedLocaleStrings.vb#1)]

## <a name="related-rules"></a>関連規則
 [CA1303:ローカライズされるパラメーターとしてリテラルを渡さない](../code-quality/ca1303-do-not-pass-literals-as-localized-parameters.md)
