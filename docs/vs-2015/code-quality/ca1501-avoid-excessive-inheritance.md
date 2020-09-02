---
title: 'CA1501: 継承が過剰にならないようにする |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1501
- AvoidExcessiveInheritance
helpviewer_keywords:
- AvoidExcessiveInheritance
- CA1501
ms.assetid: 9e934746-1a4d-492a-91e4-085201abafa4
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: cf797ad67b7df2eb1f3ba1246e965ed6ebbd586d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85547863"
---
# <a name="ca1501-avoid-excessive-inheritance"></a>CA1501:継承を使用しすぎないでください
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|AvoidExcessiveInheritance|
|CheckId|CA1501|
|カテゴリ|Microsoft の保守容易性|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 型が、その継承階層内の 5 つ以上深いレベルにあります。

## <a name="rule-description"></a>ルールの説明
 深いレベルで入れ子にされた型の確認、理解、および保守は困難です。 このルールは、分析を同じモジュール内の階層に限定します。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、継承階層の深さが低い基本型から型を派生させるか、または中間の基本型の一部を削除します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 このルールからの警告を抑制するのは安全です。 ただし、コードの保守が困難になることがあります。 基本型の可視性によっては、この規則違反の解決によって重大な変更が発生する場合があることに注意してください。 たとえば、パブリック基本型の削除は、互換性に影響する変更です。

## <a name="example"></a>例
 次の例は、規則に違反する型を示しています。

 [!code-csharp[FxCop.Maintainability.ExcessiveInheritance#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Maintainability.ExcessiveInheritance/cs/FxCop.Maintainability.ExcessiveInheritance.cs#1)]
 [!code-vb[FxCop.Maintainability.ExcessiveInheritance#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Maintainability.ExcessiveInheritance/vb/FxCop.Maintainability.ExcessiveInheritance.vb#1)]
