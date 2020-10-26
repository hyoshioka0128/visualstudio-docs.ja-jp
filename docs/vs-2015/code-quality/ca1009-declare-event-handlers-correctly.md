---
title: 'CA1009: イベントハンドラーを正しく宣言します。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1009
- DeclareEventHandlersCorrectly
helpviewer_keywords:
- CA1009
- DeclareEventHandlersCorrectly
ms.assetid: ab65c471-1449-49d2-9896-7b9af74284b4
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 6a4a4e2e6990772b50568043c4d18ff29248571d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85547889"
---
# <a name="ca1009-declare-event-handlers-correctly"></a>CA1009:イベント ハンドラーを正しく宣言します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|DeclareEventHandlersCorrectly|
|CheckId|CA1009|
|カテゴリ|Microsoft Design|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 パブリックまたは保護されたイベントを処理するデリゲートに、正しいシグネチャ、戻り値の型、またはパラメーター名がありません。

## <a name="rule-description"></a>ルールの説明
 イベント ハンドラー メソッドでは 2 つのパラメーターを使用します。 1つは型で <xref:System.Object?displayProperty=fullName> 、は ' sender ' という名前です。 これは、イベントを発生させるオブジェクトです。 2番目のパラメーターの型は <xref:System.EventArgs?displayProperty=fullName> で、' e ' という名前が付けられています。 これは、イベントに関連付けられるデータです。 たとえば、ファイルが開かれるたびにイベントが発生した場合、イベントデータには通常、ファイルの名前が含まれます。

 イベントハンドラーメソッドは値を返すことはできません。 C# プログラミング言語では、これは戻り値の型によって示され `void` ます。 イベントハンドラーは、複数のオブジェクトで複数のメソッドを呼び出すことができます。 メソッドが値を返すことが許可された場合、各イベントに対して複数の戻り値が発生し、呼び出された最後のメソッドの値のみが使用可能になります。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、デリゲートの署名、戻り値の型、またはパラメーター名を修正します。 詳細については、次の例を参照してください。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。

## <a name="example"></a>例
 次の例は、イベントの処理に適したデリゲートを示しています。 このイベントハンドラーによって呼び出すことができるメソッドは、デザインガイドラインで指定されているシグネチャに準拠しています。 `AlarmEventHandler` デリゲートの型名を指定します。 `AlarmEventArgs` イベントデータの基本クラスから派生し、 <xref:System.EventArgs> アラームイベントデータを保持します。

 [!code-cpp[FxCop.Design.EventsTwoParams#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.EventsTwoParams/cpp/FxCop.Design.EventsTwoParams.cpp#1)]
 [!code-csharp[FxCop.Design.EventsTwoParams#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.EventsTwoParams/cs/FxCop.Design.EventsTwoParams.cs#1)]
 [!code-vb[FxCop.Design.EventsTwoParams#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.EventsTwoParams/vb/FxCop.Design.EventsTwoParams.vb#1)]

## <a name="related-rules"></a>関連規則
 [CA2109:表示するイベント ハンドラーを確認します](../code-quality/ca2109-review-visible-event-handlers.md)

## <a name="see-also"></a>参照
 <xref:System.EventArgs?displayProperty=fullName> <xref:System.Object?displayProperty=fullName>
 [NIB: イベントとデリゲート](https://msdn.microsoft.com/d98fd58b-fa4f-4598-8378-addf4355a115)
