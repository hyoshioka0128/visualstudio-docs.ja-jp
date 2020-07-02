---
title: 'CA2207: 値型の静的フィールド inline | を初期化します。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- InitializeValueTypeStaticFieldsInline
- CA2207
helpviewer_keywords:
- CA2207
- InitializeValueTypeStaticFieldsInline
ms.assetid: d1ea9d8b-ecc2-46ca-86e2-c41dd0e76658
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 792fe18a4f472d0b8a4fd62c652f2ae34fcf6864
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546303"
---
# <a name="ca2207-initialize-value-type-static-fields-inline"></a>CA2207:値型のスタティック フィールドのインラインを初期化します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|アイテム|値|
|-|-|
|TypeName|InitializeValueTypeStaticFieldsInline|
|CheckId|CA2207|
|カテゴリ|Microsoft. 使用方法|
|互換性に影響する変更点|中断なし|

## <a name="cause"></a>原因
 値型は、明示的な静的コンストラクターを宣言します。

## <a name="rule-description"></a>ルールの説明
 値型が宣言されている場合、すべての値型フィールドがゼロに設定され、すべての参照型フィールドが (Visual Basic) に設定されている既定の初期化が行われ `null` `Nothing` ます。 明示的な静的コンストラクターは、その型のインスタンスコンストラクターまたは静的メンバーが呼び出される前にのみ実行されることが保証されます。 したがって、インスタンスコンストラクターを呼び出さずに型が作成された場合、静的コンストラクターの実行は保証されません。

 すべての静的データがインラインで初期化され、明示的な静的コンストラクターが宣言されていない場合、C# および Visual Basic コンパイラは、この `beforefieldinit` フラグを MSIL クラス定義に追加します。 コンパイラは、静的初期化コードを含むプライベートな静的コンストラクターも追加します。 このプライベート静的コンストラクターは、型の静的フィールドにアクセスする前に実行することが保証されています。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、宣言時にすべての静的データを初期化し、静的コンストラクターを削除します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。

## <a name="related-rules"></a>関連規則
 [CA1810:参照型の静的フィールドをインラインで初期化します](../code-quality/ca1810-initialize-reference-type-static-fields-inline.md)
