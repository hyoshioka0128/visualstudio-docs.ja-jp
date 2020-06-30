---
title: 'CA1404: P-Invoke | の直後に GetLastError を呼び出します。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CallGetLastErrorImmediatelyAfterPInvoke
- CA1404
helpviewer_keywords:
- CallGetLastErrorImmediatelyAfterPInvoke
- CA1404
ms.assetid: 52ae9eff-50f9-4b2f-8039-ca7e49fba88e
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 54ac9a4d56136d9e981ae038a0b219aa4cb4774e
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544496"
---
# <a name="ca1404-call-getlasterror-immediately-after-pinvoke"></a>CA1404: P/Invoke の直後に GetLastError を呼び出します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|CallGetLastErrorImmediatelyAfterPInvoke|
|CheckId|CA1404|
|カテゴリ|Microsoft. 相互運用性|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 メソッドまたは同等の Win32 関数への呼び出しが行われ、その直前の <xref:System.Runtime.InteropServices.Marshal.GetLastWin32Error%2A?displayProperty=fullName> `GetLastError` 呼び出しがプラットフォーム呼び出しメソッドになりません。

## <a name="rule-description"></a>ルールの説明
 プラットフォーム呼び出しメソッドはアンマネージコードにアクセスし、または属性のキーワードを使用して定義され `Declare` [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] <xref:System.Runtime.InteropServices.DllImportAttribute?displayProperty=fullName> ます。 一般に、エラーが発生した場合、アンマネージ関数は Win32 関数を呼び出して、 `SetLastError` エラーに関連付けられているエラーコードを設定します。 失敗した関数の呼び出し元は、Win32 関数を呼び出して `GetLastError` エラーコードを取得し、エラーの原因を特定します。 エラーコードはスレッド単位で管理され、の次の呼び出しによって上書きされ `SetLastError` ます。 失敗したプラットフォーム呼び出しメソッドを呼び出した後、マネージコードはメソッドを呼び出してエラーコードを取得でき <xref:System.Runtime.InteropServices.Marshal.GetLastWin32Error%2A> ます。 エラーコードは、他のマネージクラスライブラリメソッドからの内部呼び出しによって上書きされる可能性があるため、 `GetLastError` またはメソッドは、 <xref:System.Runtime.InteropServices.Marshal.GetLastWin32Error%2A> プラットフォーム呼び出しメソッドの呼び出しの直後に呼び出す必要があります。

 この規則は、プラットフォーム呼び出しメソッドの呼び出しとの呼び出しの間に、次のマネージメンバーが発生した場合に、その呼び出しを無視し <xref:System.Runtime.InteropServices.Marshal.GetLastWin32Error%2A> ます。 これらのメンバーは、エラーコードを変更せず、一部のプラットフォーム呼び出しメソッドの呼び出しが成功したかどうかを判断するのに役立ちます。

- <xref:System.IntPtr.Zero?displayProperty=fullName>

- <xref:System.IntPtr.op_Equality%2A?displayProperty=fullName>

- <xref:System.IntPtr.op_Inequality%2A?displayProperty=fullName>

- <xref:System.Runtime.InteropServices.SafeHandle.IsInvalid%2A?displayProperty=fullName>

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、プラットフォーム呼び出しメソッドの呼び出しの直後になるように、呼び出しをに移動し <xref:System.Runtime.InteropServices.Marshal.GetLastWin32Error%2A> ます。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 プラットフォーム呼び出しメソッドの呼び出しとメソッドの呼び出しの間のコードが <xref:System.Runtime.InteropServices.Marshal.GetLastWin32Error%2A> 明示的にまたは暗黙的にエラーコードを変更することができない場合は、この規則からの警告を抑制することが安全です。

## <a name="example"></a>例
 次の例は、規則に違反するメソッドと、規則を満たすメソッドを示しています。

 [!code-csharp[FxCop.Interoperability.LastErrorPInvoke#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.LastErrorPInvoke/cs/FxCop.Interoperability.LastErrorPInvoke.cs#1)]
 [!code-vb[FxCop.Interoperability.LastErrorPInvoke#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Interoperability.LastErrorPInvoke/vb/FxCop.Interoperability.LastErrorPInvoke.vb#1)]

## <a name="related-rules"></a>関連規則
 [CA1060: NativeMethods クラスへの P/Invoke の移動](../code-quality/ca1060-move-p-invokes-to-nativemethods-class.md)

 [CA1400: P/Invoke エントリポイントが存在する必要があります](../code-quality/ca1400-p-invoke-entry-points-should-exist.md)

 [CA1401: P/Invoke を表示できません](../code-quality/ca1401-p-invokes-should-not-be-visible.md)

 [CA2101: P/Invoke 文字列引数のマーシャリングを指定します。](../code-quality/ca2101-specify-marshaling-for-p-invoke-string-arguments.md)

 [CA2205:Win32 API に相当するマネージド API を使用します](../code-quality/ca2205-use-managed-equivalents-of-win32-api.md)
