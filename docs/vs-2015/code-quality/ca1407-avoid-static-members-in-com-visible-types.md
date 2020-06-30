---
title: 'CA1407: COM 参照可能な型で静的メンバーを避けてください。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1407
- AvoidStaticMembersInComVisibleTypes
helpviewer_keywords:
- CA1407
- AvoidStaticMembersInComVisibleTypes
ms.assetid: bebd0776-ad04-453c-bca8-8c124c2d7840
caps.latest.revision: 25
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 436a8614c18c296c072d91116143306d898f0436
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85538854"
---
# <a name="ca1407-avoid-static-members-in-com-visible-types"></a>CA1407:Com 参照可能な型で静的メンバーを使用しません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|AvoidStaticMembersInComVisibleTypes|
|CheckId|CA1407|
|カテゴリ|Microsoft. 相互運用性|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 コンポーネントオブジェクトモデル (COM) に対して表示されるように明示的にマークされている型には、メソッドが含まれてい `public``static` ます。

## <a name="rule-description"></a>ルールの説明
 COM はメソッドをサポートしていません `static` 。

 このルールは、プロパティとイベントのアクセサー、演算子のオーバーロードメソッド、または属性または属性のいずれかを使用してマークされたメソッドを無視し <xref:System.Runtime.InteropServices.ComRegisterFunctionAttribute?displayProperty=fullName> <xref:System.Runtime.InteropServices.ComUnregisterFunctionAttribute?displayProperty=fullName> ます。

 既定では、アセンブリ、パブリック型、パブリック型のパブリックインスタンスメンバー、およびパブリック値型のすべてのメンバーに対して、COM から参照できます。

 このルールを実行するには、 <xref:System.Runtime.InteropServices.ComVisibleAttribute> `false` <xref:System.Runtime.InteropServices.ComVisibleAttribute> 次のコードに示すように、アセンブリレベルをに設定し、クラスをに設定する必要があり `true` ます。

```csharp
using System;
using System.Runtime.InteropServices;

[assembly: ComVisible(false)]
namespace Samples
{
    [ComVisible(true)]
    public class MyClass
    {
        public static void DoSomething()
        {
        }
    }
}
```

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、メソッドと同じ機能を提供するインスタンスメソッドを使用するようにデザインを変更し `static` ます。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 COM クライアントがメソッドによって提供される機能へのアクセスを必要としない場合は、この規則による警告を抑制しても安全です `static` 。

## <a name="example-violation"></a>違反の例

### <a name="description"></a>説明
 次の例は、 `static` この規則に違反するメソッドを示しています。

### <a name="code"></a>コード
 [!code-csharp[FxCop.Interoperability.ComVisibleStaticMembersViolation#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.ComVisibleStaticMembersViolation/cs/FxCop.Interoperability.ComVisibleStaticMembersViolation.cs#1)]

### <a name="comments"></a>コメント
 この例では、 **FromPages**のメソッドを COM から呼び出すことはできません。

## <a name="example-fix"></a>修正の例

### <a name="description"></a>説明
 前の例の違反を修正するには、メソッドをインスタンスメソッドに変更しますが、このインスタンスでは意味がありません。 より適切な解決策は、メソッドを明示的に適用し `ComVisible(false)` て、メソッドが COM から認識されないことを他の開発者に明確にすることです。

 次の例は、メソッドに適用され <xref:System.Runtime.InteropServices.ComRegisterFunctionAttribute> ます。

### <a name="code"></a>コード
 [!code-csharp[FxCop.Interoperability.ComVisibleStaticMembersFixed#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.ComVisibleStaticMembersFixed/cs/FxCop.Interoperability.ComVisibleStaticMembersFixed.cs#1)]

## <a name="related-rules"></a>関連規則
 [CA1017:アセンブリに ComVisibleAttribute を設定します](../code-quality/ca1017-mark-assemblies-with-comvisibleattribute.md)

 [CA1406:Visual Basic 6 クライアントに対しては Int64 引数を使用しません](../code-quality/ca1406-avoid-int64-arguments-for-visual-basic-6-clients.md)

 [CA1413:Com 参照可能な値型ではパブリックでないフィールドを使用しません](../code-quality/ca1413-avoid-non-public-fields-in-com-visible-value-types.md)

## <a name="see-also"></a>関連項目
 [アンマネージ コードとの相互運用](https://msdn.microsoft.com/library/ccb68ce7-b0e9-4ffb-839d-03b1cd2c1258)
