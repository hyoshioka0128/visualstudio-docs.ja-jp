---
title: 'CA1040: 空のインターフェイスを回避する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1040
- AvoidEmptyInterfaces
helpviewer_keywords:
- AvoidEmptyInterfaces
- CA1040
ms.assetid: 120a741b-5fd1-4836-8453-7857e0cd0380
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 0ef6dc666cbc3c26d58358c9b59264f93a7bf184
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85548253"
---
# <a name="ca1040-avoid-empty-interfaces"></a>CA1040:空のインターフェイスは使用しません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|AvoidEmptyInterfaces|
|CheckId|CA1040|
|カテゴリ|Microsoft Design|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 インターフェイスがメンバーを宣言していないか、2つ以上のインターフェイスを実装していません。

## <a name="rule-description"></a>ルールの説明
 インターフェイスには、動作や使用のコントラクトを実現するメンバーが定義されます。 インターフェイスで示される機能は、継承の階層構造内に型が存在するかどうかにかかわらず、どの型からも適用できます。 型ではインターフェイスのメンバーに実装することで、インターフェイスが実装されます。 空のインターフェイスでは、メンバーは定義されません。 そのため、実装できるコントラクトは定義されていません。

 型に実装する必要がある空のインターフェイスが設計に含まれている場合は、通常、インターフェイスをマーカーとして使用するか、型のグループを識別する方法を使用します。 この id が実行時に発生する場合は、カスタム属性を使用することをお勧めします。 対象の型を特定するには、属性の有無、または属性のプロパティを使用します。 コンパイル時に id が発生する必要がある場合は、空のインターフェイスを使用できます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 インターフェイスを削除するか、またはそのインターフェイスにメンバーを追加します。 空のインターフェイスを使用して一連の型にラベルを付ける場合は、インターフェイスをカスタム属性に置き換えます。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 コンパイル時に型のセットを識別するためにインターフェイスを使用する場合は、この規則からの警告を抑制することが安全です。

## <a name="example"></a>例
 次の例は、空のインターフェイスを示しています。

 [!code-cpp[FxCop.Design.InterfacesNotEmpty#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.InterfacesNotEmpty/cpp/FxCop.Design.InterfacesNotEmpty.cpp#1)]
 [!code-csharp[FxCop.Design.InterfacesNotEmpty#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.InterfacesNotEmpty/cs/FxCop.Design.InterfacesNotEmpty.cs#1)]
 [!code-vb[FxCop.Design.InterfacesNotEmpty#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.InterfacesNotEmpty/vb/FxCop.Design.InterfacesNotEmpty.vb#1)]
