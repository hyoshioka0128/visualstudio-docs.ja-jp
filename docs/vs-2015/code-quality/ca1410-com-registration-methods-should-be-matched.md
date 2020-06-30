---
title: 'CA1410: COM 登録メソッドは一致しなければなりません |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1410
- ComRegistrationMethodsShouldBeMatched
helpviewer_keywords:
- CA1410
- ComRegistrationMethodsShouldBeMatched
ms.assetid: f3b2e62d-fd66-4093-9f0c-dba01ad995fd
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 43767ce04b32440a5c6753f5bfcabb91487c1232
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546706"
---
# <a name="ca1410-com-registration-methods-should-be-matched"></a>CA1410:COM 登録メソッドは一致しなければなりません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|ComRegistrationMethodsShouldBeMatched|
|CheckId|CA1410|
|カテゴリ|Microsoft. 相互運用性|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 型は、属性でマークされたメソッドを宣言して <xref:System.Runtime.InteropServices.ComRegisterFunctionAttribute?displayProperty=fullName> いますが、属性でマークされたメソッドを宣言していません <xref:System.Runtime.InteropServices.ComUnregisterFunctionAttribute?displayProperty=fullName> 。また、その逆も同様です。

## <a name="rule-description"></a>ルールの説明
 コンポーネントオブジェクトモデル (COM) クライアントで型を作成するには、 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] その型を最初に登録する必要があります。 使用可能な場合は、 <xref:System.Runtime.InteropServices.ComRegisterFunctionAttribute> ユーザー指定のコードを実行するための登録プロセス中に、属性でマークされたメソッドが呼び出されます。 属性でマークされた対応するメソッド <xref:System.Runtime.InteropServices.ComUnregisterFunctionAttribute> は、登録メソッドの操作を元に戻すための登録解除プロセス中に呼び出されます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、対応する登録または登録解除の方法を追加します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。

## <a name="example"></a>例
 次の例は、規則に違反する型を示しています。 コメント化されたコードは、違反の修正を示しています。

 [!code-csharp[FxCop.Interoperability.ComRegistration#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.ComRegistration/cs/FxCop.Interoperability.ComRegistration.cs#1)]
 [!code-vb[FxCop.Interoperability.ComRegistration#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Interoperability.ComRegistration/vb/FxCop.Interoperability.ComRegistration.vb#1)]

## <a name="related-rules"></a>関連規則
 [CA1411:COM 登録メソッドは参照可能であることはできません](../code-quality/ca1411-com-registration-methods-should-not-be-visible.md)

## <a name="see-also"></a>関連項目
 <xref:System.Runtime.InteropServices.RegistrationServices?displayProperty=fullName>[COMRegasm.exe を使用したアセンブリの登録](https://msdn.microsoft.com/library/87925795-a3ae-4833-b138-125413478551) [(アセンブリ登録ツール)](https://msdn.microsoft.com/library/e190e342-36ef-4651-a0b4-0e8c2c0281cb)
