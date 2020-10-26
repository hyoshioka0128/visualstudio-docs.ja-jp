---
title: 'CA1408: AutoDual ClassInterfaceType | を使用しないでください。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- DoNotUseAutoDualClassInterfaceType
- CA1408
helpviewer_keywords:
- CA1408
- DoNotUseAutoDualClassInterfaceType
ms.assetid: 60ca5e02-3c51-42dd-942b-4f950eecfa0f
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: b953a97d557e28cce50f554acc03797d4be38220
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85534876"
---
# <a name="ca1408-do-not-use-autodual-classinterfacetype"></a>CA1408:AutoDual ClassInterfaceType を使用しないでください
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|DoNotUseAutoDualClassInterfaceType|
|CheckId|CA1408|
|カテゴリ|Microsoft. 相互運用性|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 コンポーネントオブジェクトモデル (COM) で参照できる型は、の値に設定された属性でマークされ <xref:System.Runtime.InteropServices.ClassInterfaceAttribute> `AutoDual` <xref:System.Runtime.InteropServices.ClassInterfaceType> ます。

## <a name="rule-description"></a>ルールの説明
 デュアル インターフェイスを使用する型を使用することで、クライアントを特定のインターフェイス レイアウトに対応付けることができます。 将来のバージョンで、この型またはその基本型のレイアウトに変更が加えられると、インターフェイスに対応付けられた COM クライアントが切り離されます。 既定では、 <xref:System.Runtime.InteropServices.ClassInterfaceAttribute> 属性が指定されていない場合、ディスパッチ専用インターフェイスが使用されます。

 特に指定されていない限り、パブリックなすべての非ジェネリック型は COM から参照できます。非パブリック型とジェネリック型はすべて、COM から見えません。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、属性の値 <xref:System.Runtime.InteropServices.ClassInterfaceAttribute> を `None` の値に変更し、インターフェイスを <xref:System.Runtime.InteropServices.ClassInterfaceType> 明示的に定義します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 型とその基本型のレイアウトが将来のバージョンで変更されないことが確実である場合を除き、この規則からの警告を抑制しないでください。

## <a name="example"></a>例
 次の例は、規則に違反するクラスと、明示的なインターフェイスを使用するクラスの再宣言を示しています。

 [!code-csharp[FxCop.Interoperability.AutoDual#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.AutoDual/cs/FxCop.Interoperability.AutoDual.cs#1)]
 [!code-vb[FxCop.Interoperability.AutoDual#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Interoperability.AutoDual/vb/FxCop.Interoperability.AutoDual.vb#1)]

## <a name="related-rules"></a>関連規則
 [CA1403:Auto 配置の型を COM 参照可能にすることはできません](../code-quality/ca1403-auto-layout-types-should-not-be-com-visible.md)

 [CA1412:ComSource インターフェイスを IDispatch として設定します](../code-quality/ca1412-mark-comsource-interfaces-as-idispatch.md)

## <a name="see-also"></a>参照
 [相互運用のための .Net 型を修飾する](https://msdn.microsoft.com/library/4b8afb52-fb8d-4e65-b47c-fd82956a3cdd)[クラスインターフェイスの概要](https://msdn.microsoft.com/733c0dd2-12e5-46e6-8de1-39d5b25df024)[アンマネージコードとの相互運用](https://msdn.microsoft.com/library/ccb68ce7-b0e9-4ffb-839d-03b1cd2c1258)
