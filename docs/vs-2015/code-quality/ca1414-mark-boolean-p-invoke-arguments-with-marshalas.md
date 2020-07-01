---
title: 'CA1414: ブール型の P-Invoke 引数を MarshalAs | でマークします。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1414
- MarkBooleanPInvokeArgumentsWithMarshalAs
helpviewer_keywords:
- CA1414
- MarkBooleanPInvokeArgumentsWithMarshalAs
ms.assetid: c0c84cf5-7701-4897-9114-66fc4b895699
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 783f7fad05cad18efea2f83b6d76c4c9e644f119
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85548383"
---
# <a name="ca1414-mark-boolean-pinvoke-arguments-with-marshalas"></a>CA1414: ブール型の P/Invoke 引数を MarshalAs に設定します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|MarkBooleanPInvokeArgumentsWithMarshalAs|
|CheckId|CA1414|
|カテゴリ|Microsoft. 相互運用性|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 プラットフォーム呼び出しメソッドの宣言に <xref:System.Boolean?displayProperty=fullName> パラメーターまたは戻り値が含まれていますが、 <xref:System.Runtime.InteropServices.MarshalAsAttribute?displayProperty=fullName> パラメーターまたは戻り値に属性が適用されていません。

## <a name="rule-description"></a>ルールの説明
 プラットフォーム呼び出しメソッドはアンマネージコードにアクセスし、 `Declare` またはのキーワードを使用して定義され [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] <xref:System.Runtime.InteropServices.DllImportAttribute?displayProperty=fullName> ます。 <xref:System.Runtime.InteropServices.MarshalAsAttribute>マネージコードとアンマネージコードの間でデータ型を変換するために使用されるマーシャリング動作を指定します。 やなどの多くの単純なデータ型は、 <xref:System.Byte?displayProperty=fullName> <xref:System.Int32?displayProperty=fullName> アンマネージコードで1つの表現を持ち、マーシャリング動作の指定を必要としません。共通言語ランタイムは、自動的に正しい動作を提供します。

 <xref:System.Boolean>データ型には、アンマネージコード内の複数の表現があります。 が指定されて <xref:System.Runtime.InteropServices.MarshalAsAttribute> いない場合、データ型の既定のマーシャリング動作 <xref:System.Boolean> はに <xref:System.Runtime.InteropServices.UnmanagedType?displayProperty=fullName> なります。 これは32ビットの整数であり、すべての状況に適しているわけではありません。 アンマネージメソッドによって必要とされるブール値は、適切なに決定して照合する必要があり <xref:System.Runtime.InteropServices.UnmanagedType?displayProperty=fullName> ます。 Unmanagedtype.bool は、常に4バイトの Win32 BOOL 型です。 Unmanagedtype.bool は、C++ `bool` または他の1バイト型に使用する必要があります。 詳細については、「[ブール型の既定のマーシャリング](https://msdn.microsoft.com/d4c00537-70f7-4ca6-8197-bfc1ec037ff9)」を参照してください。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、 <xref:System.Runtime.InteropServices.MarshalAsAttribute> <xref:System.Boolean> パラメーターまたは戻り値にを適用します。 属性の値を適切なに設定し <xref:System.Runtime.InteropServices.UnmanagedType> ます。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。 既定のマーシャリング動作が適切な場合でも、動作が明示的に指定されていれば、コードをより簡単に管理できます。

## <a name="example"></a>例
 次の例は、適切な属性でマークされている2つのプラットフォーム呼び出しメソッドを示して <xref:System.Runtime.InteropServices.MarshalAsAttribute> います。

 [!code-cpp[FxCop.Interoperability.BoolMarshalAs#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.BoolMarshalAs/cpp/FxCop.Interoperability.BoolMarshalAs.cpp#1)]
 [!code-csharp[FxCop.Interoperability.BoolMarshalAs#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.BoolMarshalAs/cs/FxCop.Interoperability.BoolMarshalAs.cs#1)]
 [!code-vb[FxCop.Interoperability.BoolMarshalAs#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Interoperability.BoolMarshalAs/vb/FxCop.Interoperability.BoolMarshalAs.vb#1)]

## <a name="related-rules"></a>関連規則
 [CA1901: P/Invoke 宣言はポータブルでなければなりません](../code-quality/ca1901-p-invoke-declarations-should-be-portable.md)

 [CA2101: P/Invoke 文字列引数のマーシャリングを指定します。](../code-quality/ca2101-specify-marshaling-for-p-invoke-string-arguments.md)

## <a name="see-also"></a>関連項目
 <xref:System.Runtime.InteropServices.UnmanagedType?displayProperty=fullName>[アンマネージコードとの相互運用](https://msdn.microsoft.com/library/ccb68ce7-b0e9-4ffb-839d-03b1cd2c1258)[を行うブール型に対する既定のマーシャリング](https://msdn.microsoft.com/d4c00537-70f7-4ca6-8197-bfc1ec037ff9)
