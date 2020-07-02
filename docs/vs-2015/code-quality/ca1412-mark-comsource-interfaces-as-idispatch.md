---
title: 'CA1412: ComSource インターフェイスを IDispatch | としてマークします。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- MarkComSourceInterfacesAsIDispatch
- CA1412
helpviewer_keywords:
- CA1412
- MarkComSourceInterfacesAsIDispatch
ms.assetid: 131a7563-0410-443c-a8f5-52104250cfb4
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 5685ad7a760e00392b5f9684cdf399ee320d4a0c
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85540258"
---
# <a name="ca1412-mark-comsource-interfaces-as-idispatch"></a>CA1412:ComSource インターフェイスを IDispatch として設定します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|アイテム|値|
|-|-|
|TypeName|MarkComSourceInterfacesAsIDispatch|
|CheckId|CA1412|
|カテゴリ|Microsoft. 相互運用性|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 型が属性でマークされ <xref:System.Runtime.InteropServices.ComSourceInterfacesAttribute> ており、少なくとも1つの指定されたインターフェイスが、 <xref:System.Runtime.InteropServices.InterfaceTypeAttribute> 値に設定された属性でマークされていません `InterfaceIsDispatch` 。

## <a name="rule-description"></a>ルールの説明
 <xref:System.Runtime.InteropServices.ComSourceInterfacesAttribute>は、クラスがコンポーネントオブジェクトモデル (COM) クライアントに公開するイベントインターフェイスを識別するために使用されます。 `InterfaceIsIDispatch`Visual Basic 6 の COM クライアントがイベント通知を受信できるようにするには、これらのインターフェイスをとして公開する必要があります。 既定では、インターフェイスが属性でマークされていない場合 <xref:System.Runtime.InteropServices.InterfaceTypeAttribute> は、デュアルインターフェイスとして公開されます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、属性を使用して指定されている <xref:System.Runtime.InteropServices.InterfaceTypeAttribute> すべてのインターフェイスの値が cominterfacetype.interfaceisidispatch に設定されるように、属性を追加または変更し <xref:System.Runtime.InteropServices.ComSourceInterfacesAttribute> ます。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。

## <a name="example"></a>例
 次の例は、いずれかのインターフェイスが規則に違反しているクラスを示しています。

 [!code-csharp[FxCop.Interoperability.MarkIDispatch#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.MarkIDispatch/cs/FxCop.Interoperability.MarkIDispatch.cs#1)]
 [!code-vb[FxCop.Interoperability.MarkIDispatch#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Interoperability.MarkIDispatch/vb/FxCop.Interoperability.MarkIDispatch.vb#1)]

## <a name="related-rules"></a>関連規則
 [CA1408:AutoDual ClassInterfaceType を使用しないでください](../code-quality/ca1408-do-not-use-autodual-classinterfacetype.md)

## <a name="see-also"></a>関連項目
 [方法: COM シンクによって処理](https://msdn.microsoft.com/7c9944b2-e951-4c3e-a0a1-59b2ae37d7fd)されるイベントを[アンマネージコードと相互運用](https://msdn.microsoft.com/library/ccb68ce7-b0e9-4ffb-839d-03b1cd2c1258)する
