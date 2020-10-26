---
title: 'CA1026: 既定のパラメーターを使用することはできません |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1026
- DefaultParametersShouldNotBeUsed
helpviewer_keywords:
- CA1026
- DefaultParametersShouldNotBeUsed
ms.assetid: 09643415-36ef-4d0f-9411-5721e14e2512
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: a63d6e788dd1722d0c593469b225a4f1aeb4738d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85548447"
---
# <a name="ca1026-default-parameters-should-not-be-used"></a>CA1026:既定パラメーターを使用することはできません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|DefaultParametersShouldNotBeUsed|
|CheckId|CA1026|
|カテゴリ|Microsoft Design|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 外部から参照できる型には、既定のパラメーターを使用する外部から参照できるメソッドが含まれています。

## <a name="rule-description"></a>ルールの説明
 既定のパラメーターを使用するメソッドは、共通言語仕様 (CLS) で許可されています。ただし、CLS では、これらのパラメーターに割り当てられている値をコンパイラで無視できます。 既定のパラメーター値を無視するコンパイラ用に記述されたコードでは、既定のパラメーターごとに引数を明示的に指定する必要があります。 プログラミング言語全体で必要な動作を維持するには、既定のパラメーターを使用するメソッドを、既定のパラメーターを指定するメソッドのオーバーロードに置き換える必要があります。

 コンパイラは、マネージコードにアクセスするときに C++ のマネージ拡張の既定のパラメーターの値を無視します。 Visual Basic コンパイラは、 [省略可能](https://msdn.microsoft.com/library/4571ce88-a539-4115-b230-54eb277c6aa7) なキーワードを使用する既定のパラメーターを持つメソッドをサポートしています。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、既定のパラメーターを使用するメソッドを、既定のパラメーターを指定するメソッドのオーバーロードに置き換えます。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。

## <a name="example"></a>例
 次の例は、既定のパラメーターを使用するメソッドと、同等の機能を提供するオーバーロードされたメソッドを示しています。

 [!code-vb[FxCop.Design.DefaultParameters#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.DefaultParameters/vb/FxCop.Design.DefaultParameters.vb#1)]

## <a name="related-rules"></a>関連規則
 [CA1025:反復する引数を params 配列で置き換えます](../code-quality/ca1025-replace-repetitive-arguments-with-params-array.md)

## <a name="see-also"></a>参照
 [言語への非依存性、および言語非依存コンポーネント](https://msdn.microsoft.com/library/4f0b77d0-4844-464f-af73-6e06bedeafc6)
