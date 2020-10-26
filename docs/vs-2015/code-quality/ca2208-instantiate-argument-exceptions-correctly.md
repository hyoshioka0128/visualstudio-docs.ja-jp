---
title: 'CA2208: 引数の例外を正しくインスタンス化します |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2208
- InstantiateArgumentExceptionsCorrectly
helpviewer_keywords:
- InstantiateArgumentExceptionsCorrectly
- CA2208
ms.assetid: e2a48939-d9fa-478c-b2f9-3bdbce07dff7
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 6a63ebb7f3946926864c4dd882c281b5dcd7c6c5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85535838"
---
# <a name="ca2208-instantiate-argument-exceptions-correctly"></a>CA2208:引数の例外を正しくインスタンス化します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|InstantiateArgumentExceptionsCorrectly|
|CheckId|CA2208|
|カテゴリ|Microsoft. 使用方法|
|互換性に影響する変更点|中断なし|

## <a name="cause"></a>原因
 次のような状況が考えられます。

- 例外の種類の既定の (パラメーターなしの) コンストラクターが呼び出されたか、または [ArgumentException] () から派生しています。<!-- TODO: review code entity reference <xref:assetId:///System.ArgumentException?qualifyHint=True&amp;autoUpgrade=True>  -->).

- 不適切な文字列引数が、例外の種類のパラメーター化されたコンストラクターに渡されたか、または [ArgumentException から派生しています。(<!-- TODO: review code entity reference <xref:assetId:///System.ArgumentException.?qualifyHint=True&amp;autoUpgrade=True>  -->)

## <a name="rule-description"></a>ルールの説明
 既定のコンストラクターを呼び出す代わりに、より意味のある例外メッセージを提供できるコンストラクターのオーバーロードのいずれかを呼び出します。 例外メッセージは、開発者を対象とし、エラー状態と、例外を修正または回避する方法を明確に説明する必要があります。

 とその派生型の1つの文字列コンストラクターおよび2つの文字列コンストラクターのシグネチャは、 <xref:System.ArgumentException> `message` パラメーターとパラメーターに対して一貫性がありません `paramName` 。 正しい文字列引数を使用して、これらのコンストラクターが呼び出されていることを確認します。 署名は次のとおりです。

 <xref:System.ArgumentException>(文字列 `message` )

 <xref:System.ArgumentException>(string `message` , string `paramName` )

 <xref:System.ArgumentNullException>(文字列 `paramName` )

 <xref:System.ArgumentNullException>(string `paramName` , string `message` )

 <xref:System.ArgumentOutOfRangeException>(文字列 `paramName` )

 <xref:System.ArgumentOutOfRangeException>(string `paramName` , string `message` )

 <xref:System.DuplicateWaitObjectException>(文字列 `parameterName` )

 <xref:System.DuplicateWaitObjectException>(string `parameterName` , string `message` )

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、メッセージ、パラメーター名、またはその両方を受け取るコンストラクターを呼び出し、呼び出されるの型に対して引数が適切であることを確認し <xref:System.ArgumentException> ます。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 パラメーター化されたコンストラクターが正しい文字列引数で呼び出された場合にのみ、この規則からの警告を抑制することが安全です。

## <a name="example"></a>例
 次の例は、System.argumentnullexception 型のインスタンスを誤ってインスタンス化するコンストラクターを示しています。

 [!code-cpp[FxCop.Usage.InstantiateArgumentExceptionsCorrectly#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Usage.InstantiateArgumentExceptionsCorrectly/cpp/FxCop.Usage.InheritedPublic.cpp#1)]
 [!code-csharp[FxCop.Usage.InstantiateArgumentExceptionsCorrectly#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.InstantiateArgumentExceptionsCorrectly/cs/FxCop.Usage.InheritedPublic.cs#1)]
 [!code-vb[FxCop.Usage.InstantiateArgumentExceptionsCorrectly#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.InstantiateArgumentExceptionsCorrectly/vb/FxCop.Usage.InstantiateArgumentExceptionsCorrectly.vb#1)]

## <a name="example"></a>例
 次の例では、コンストラクターの引数を切り替えることによって上記の違反を修正します。

 [!code-cpp[FxCop.Usage.InstantiateArgumentExceptionsCorrectly#2](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Usage.InstantiateArgumentExceptionsCorrectly/cpp/FxCop.Usage.InheritedPublic.cpp#2)]
 [!code-csharp[FxCop.Usage.InstantiateArgumentExceptionsCorrectly#2](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.InstantiateArgumentExceptionsCorrectly/cs/FxCop.Usage.InheritedPublic.cs#2)]
 [!code-vb[FxCop.Usage.InstantiateArgumentExceptionsCorrectly#2](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.InstantiateArgumentExceptionsCorrectly/vb/FxCop.Usage.InstantiateArgumentExceptionsCorrectly.vb#2)]
