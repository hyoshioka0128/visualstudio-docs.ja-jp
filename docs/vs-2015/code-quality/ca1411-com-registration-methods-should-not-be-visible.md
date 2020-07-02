---
title: 'CA1411: COM 登録メソッドを visible にすることはできません。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1411
- ComRegistrationMethodsShouldNotBeVisible
helpviewer_keywords:
- ComRegistrationMethodsShouldNotBeVisible
- CA1411
ms.assetid: a59f96f1-1f38-4596-b656-947df5c55311
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: f001a2bb4920ebfb3f5cff3745639bd346a0a920
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85540142"
---
# <a name="ca1411-com-registration-methods-should-not-be-visible"></a>CA1411:COM 登録メソッドは参照可能であることはできません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|アイテム|値|
|-|-|
|TypeName|ComRegistrationMethodsShouldNotBeVisible|
|CheckId|CA1411|
|カテゴリ|Microsoft. 相互運用性|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 属性または属性でマークされたメソッド <xref:System.Runtime.InteropServices.ComRegisterFunctionAttribute?displayProperty=fullName> <xref:System.Runtime.InteropServices.ComUnregisterFunctionAttribute?displayProperty=fullName> は、外部から参照できます。

## <a name="rule-description"></a>ルールの説明
 アセンブリがコンポーネントオブジェクトモデル (COM) に登録されると、アセンブリ内の COM から参照できる各型のエントリがレジストリに追加されます。 属性と属性でマークされたメソッドは、登録と登録解除の <xref:System.Runtime.InteropServices.ComRegisterFunctionAttribute> <xref:System.Runtime.InteropServices.ComUnregisterFunctionAttribute> プロセス中にそれぞれ呼び出され、これらの型の登録/登録解除に固有のユーザーコードを実行します。 このコードは、これらのプロセスの外部では呼び出さないでください。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、メソッドのアクセシビリティを `private` または (では) に変更し `internal` `Friend` [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] ます。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。

## <a name="example"></a>例
 次の例は、規則に違反する2つのメソッドを示しています。

 [!code-csharp[FxCop.Interoperability.ComRegistration2#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.ComRegistration2/cs/FxCop.Interoperability.ComRegistration2.cs#1)]
 [!code-vb[FxCop.Interoperability.ComRegistration2#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Interoperability.ComRegistration2/vb/FxCop.Interoperability.ComRegistration2.vb#1)]

## <a name="related-rules"></a>関連規則
 [CA1410:COM 登録メソッドは一致しなければなりません](../code-quality/ca1410-com-registration-methods-should-be-matched.md)

## <a name="see-also"></a>関連項目
 <xref:System.Runtime.InteropServices.RegistrationServices?displayProperty=fullName>[COMRegasm.exe を使用したアセンブリの登録](https://msdn.microsoft.com/library/87925795-a3ae-4833-b138-125413478551) [(アセンブリ登録ツール)](https://msdn.microsoft.com/library/e190e342-36ef-4651-a0b4-0e8c2c0281cb)
