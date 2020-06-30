---
title: 'CA2214: コンストラクター | のオーバーライド可能なメソッドを呼び出しません。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- DoNotCallOverridableMethodsInConstructors
- CA2214
helpviewer_keywords:
- CA2214
- DoNotCallOverridableMethodsInConstructors
ms.assetid: 335b57ca-a6e8-41b4-a20e-57ee172c97c3
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: ad467e880b3281a75db2627108af0e0b2f90ea99
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85534460"
---
# <a name="ca2214-do-not-call-overridable-methods-in-constructors"></a>CA2214:コンストラクターのオーバーライド可能なメソッドを呼び出しません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|DoNotCallOverridableMethodsInConstructors|
|CheckId|CA2214|
|カテゴリ|Microsoft. 使用方法|
|互換性に影響する変更点|中断なし|

## <a name="cause"></a>原因
 シールされていない型のコンストラクターは、そのクラスで定義されている仮想メソッドを呼び出します。

## <a name="rule-description"></a>ルールの説明
 仮想メソッドが呼び出されると、メソッドを実行する実際の型は、実行時まで選択されません。 コンストラクターが仮想メソッドを呼び出すと、そのメソッドを呼び出すインスタンスのコンストラクターが実行されていない可能性があります。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、型のコンストラクター内から型の仮想メソッドを呼び出さないでください。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。 仮想メソッドの呼び出しを避けるために、コンストラクターを再設計する必要があります。

## <a name="example"></a>例
 次の例は、このルールに違反した場合の影響を示しています。 テストアプリケーションは、のインスタンスを作成し `DerivedType` ます。これにより、基本クラス ( `BadlyConstructedType` ) コンストラクターが実行されます。 `BadlyConstructedType`コンストラクターが仮想メソッドを正しく呼び出すことが `DoSomething` できません。 出力に示されているように、はを実行し、 `DerivedType.DoSomething()` コンストラクターが実行される前にを実行し `DerivedType` ます。

 [!code-csharp[FxCop.Usage.CtorVirtual#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.CtorVirtual/cs/FxCop.Usage.CtorVirtual.cs#1)]
 [!code-vb[FxCop.Usage.CtorVirtual#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.CtorVirtual/vb/FxCop.Usage.CtorVirtual.vb#1)]

 この例を実行すると、次の出力が生成されます。

 **基本 .ctor を呼び出しています。** 
**派生したものが初期化されていますか?** 
 **派生した .ctor を呼び出す**ことはできません。
