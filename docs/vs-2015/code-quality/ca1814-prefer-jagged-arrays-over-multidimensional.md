---
title: 'CA1814: ジャグ配列を多次元 | で優先します。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- PreferJaggedArraysOverMultidimensional
- CA1814
helpviewer_keywords:
- PreferJaggedArraysOverMultidimensional
- CA1814
ms.assetid: b1ccf563-2ec8-42e5-b89c-731a9de1ea1d
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: ece9105e8a0a854837924e4a2d4f4ec485a5e202
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85543937"
---
# <a name="ca1814-prefer-jagged-arrays-over-multidimensional"></a>CA1814:複数次元の配列ではなくジャグ配列を使用します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|PreferJaggedArraysOverMultidimensional|
|CheckId|CA1814|
|カテゴリ|Microsoft. パフォーマンス|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 メンバーは多次元配列として宣言されます。

## <a name="rule-description"></a>ルールの説明
 ジャグ配列とは、その要素も配列である配列です。 要素を構成する配列のサイズは異なってもよいため、データ セットによっては無駄な空間が少なくなります。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、多次元配列をジャグ配列に変更します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 多次元配列でスペースを無駄にしない場合は、この規則の警告を非表示にします。

## <a name="example"></a>例
 次の例は、ジャグ配列と多次元配列の宣言を示しています。

 [!code-csharp[FxCop.Performance.JaggedArrays#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Performance.JaggedArrays/cs/FxCop.Performance.JaggedArrays.cs#1)]
 [!code-vb[FxCop.Performance.JaggedArrays#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Performance.JaggedArrays/vb/FxCop.Performance.JaggedArrays.vb#1)]
