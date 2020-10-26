---
title: 'CA2108: 値型の宣言セキュリティを確認してください |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- ReviewDeclarativeSecurityOnValueTypes
- CA2108
helpviewer_keywords:
- ReviewDeclarativeSecurityOnValueTypes
- CA2108
ms.assetid: d62bffdd-3826-4d52-a708-1c646c5d48c2
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 03918353b66c36698b5d17b332da052b6d95c87a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85544392"
---
# <a name="ca2108-review-declarative-security-on-value-types"></a>CA2108:値型での宣言セキュリティを確認します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|ReviewDeclarativeSecurityOnValueTypes|
|CheckId|CA2108|
|カテゴリ|Microsoft.Security|
|互換性に影響する変更点|中断なし|

## <a name="cause"></a>原因
 パブリックまたは保護された値型は、 [データ、モデリング](https://msdn.microsoft.com/library/8c37635d-e2c1-4b64-a258-61d9e87405e6) 、または [リンク確認要求](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d)によって保護されます。

## <a name="rule-description"></a>ルールの説明
 値型は、他のコンストラクターが実行される前に、既定のコンストラクターによって割り当てられ、初期化されます。 値型が Demand または LinkDemand によって保護されていて、呼び出し元にセキュリティチェックを満たすアクセス許可がない場合、既定以外のコンストラクターは失敗し、セキュリティ例外がスローされます。 値型の割り当ては解除されません。既定のコンストラクターによって設定された状態のままになります。 値型のインスタンスを渡す呼び出し元が、インスタンスを作成またはアクセスするためのアクセス許可を持っていると想定しないでください。

## <a name="how-to-fix-violations"></a>違反の修正方法
 型からセキュリティチェックを削除し、代わりにメソッドレベルのセキュリティチェックを使用しない限り、この規則の違反を修正することはできません。 このように違反を修正しても、不適切な権限を持つ呼び出し元が値型のインスタンスを取得するのを防ぐことはできません。 値型のインスタンスが既定の状態であることを確認して、機密情報を公開しないようにし、有害な方法では使用できないようにする必要があります。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 すべての呼び出し元が、セキュリティに対する脅威を損なうことなく既定の状態で値の型のインスタンスを取得できる場合、この規則からの警告を抑制することができます。

## <a name="example"></a>例
 次の例は、この規則に違反する値の型を含むライブラリを示しています。 型は、 `StructureManager` 値型のインスタンスを渡す呼び出し元が、インスタンスを作成またはアクセスするためのアクセス許可を持っていることを前提としています。

 [!code-csharp[FxCop.Security.DemandOnValueType#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.DemandOnValueType/cs/FxCop.Security.DemandOnValueType.cs#1)]

## <a name="example"></a>例
 次のアプリケーションは、ライブラリの弱点を示しています。

 [!code-csharp[FxCop.Security.TestDemandOnValueType#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.TestDemandOnValueType/cs/FxCop.Security.TestDemandOnValueType.cs#1)]

 この例を実行すると、次の出力が生成されます。

 **構造体のカスタムコンストラクター: 要求が失敗しました。** 
**新しい値 SecuredTypeStructure 100 100** 
**新しい値 SecuredTypeStructure 200 200**
## <a name="see-also"></a>参照
 [リンク確認要求](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d)[のデータとモデリング](https://msdn.microsoft.com/library/8c37635d-e2c1-4b64-a258-61d9e87405e6)
