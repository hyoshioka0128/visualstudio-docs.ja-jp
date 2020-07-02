---
title: 'CA1050: 名前空間の型を宣言する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1050
- DeclareTypesInNamespaces
helpviewer_keywords:
- DeclareTypesInNamespaces
- CA1050
ms.assetid: 1002748d-ac8d-404f-85dd-7a12d1ad3e05
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: a0a4dcc53fac7dc9b7e189686a3b32e2fb4fd030
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85539595"
---
# <a name="ca1050-declare-types-in-namespaces"></a>CA1050:名前空間で型を宣言します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|アイテム|値|
|-|-|
|TypeName|DeclareTypesInNamespaces|
|CheckId|CA1050|
|カテゴリ|Microsoft Design|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 パブリック型またはプロテクト型が名前付き名前空間のスコープ外で定義されています。

## <a name="rule-description"></a>ルールの説明
 型は名前の競合を防ぐために名前空間で宣言され、オブジェクト階層内の関連する型を整理する手段として宣言されます。 名前付き名前空間の外部にある型は、コード内で参照できないグローバル名前空間にあります。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、名前空間に型を配置します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告を抑制する必要はありませんが、アセンブリが他のアセンブリと一緒に使用されない場合は、この操作を安全に行うことができます。

## <a name="example"></a>例
 次の例では、名前空間の外部で型が正しく宣言されていないライブラリと、名前空間で宣言された同じ名前の型を持つライブラリを示します。

 [!code-csharp[FxCop.Design.TypesLiveInNamespaces#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.TypesLiveInNamespaces/cs/FxCop.Design.TypesLiveInNamespaces.cs#1)]
 [!code-vb[FxCop.Design.TypesLiveInNamespaces#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.TypesLiveInNamespaces/vb/FxCop.Design.TypesLiveInNamespaces.vb#1)]

## <a name="example"></a>例
 次のアプリケーションは、以前に定義されたライブラリを使用します。 名前空間の外側で宣言された型は、名前空間で修飾されていない場合に作成されることに注意して `Test` ください。 また、の型にアクセスするには、 `Test` `Goodspace` 名前空間の名前が必要です。

 [!code-csharp[FxCop.Design.TestTypesLive#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.TestTypesLive/cs/FxCop.Design.TestTypesLive.cs#1)]
 [!code-vb[FxCop.Design.TestTypesLive#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.TestTypesLive/vb/FxCop.Design.TestTypesLive.vb#1)]
