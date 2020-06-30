---
title: 'CA2103: 強制セキュリティを確認する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2103
- ReviewImperativeSecurity
helpviewer_keywords:
- CA2103
- ReviewImperativeSecurity
ms.assetid: d24fde71-bdf6-46c0-8965-9a73dc33c1aa
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: ade0d10e203752c7412929c6f5f44d9cbfaacfa6
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85521265"
---
# <a name="ca2103-review-imperative-security"></a>CA2103:命令型のセキュリティを確認します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|ReviewImperativeSecurity|
|CheckId|CA2103|
|カテゴリ|Microsoft.Security|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 メソッドが強制セキュリティを使用しています。また、そのメソッドで、確認要求がアクティブな場合に変更できるステータス情報または戻り値を使用して、アクセス許可を構築している可能性があります。

## <a name="rule-description"></a>ルールの説明
 命令型セキュリティは、属性を使用してメタデータにアクセス許可とアクションを格納する宣言セキュリティと比較して、マネージオブジェクトを使用して、コードの実行中にアクセス許可とセキュリティアクションを指定します。 強制セキュリティは、アクセス許可オブジェクトの状態を設定し、実行時まで使用できない情報を使用してセキュリティアクションを選択できるため、非常に柔軟性があります。 その柔軟性と共に、アクションが有効になっている限り、アクセス許可の状態を判断するために使用するランタイム情報が変更されていないというリスクが伴います。

 できる限り、宣言セキュリティを使用します。 宣言型の要求は理解しやすくなります。

## <a name="how-to-fix-violations"></a>違反の修正方法
 強制セキュリティ要求を確認して、アクセス許可の状態が、アクセス許可が使用されている限り変更できる情報に依存していないことを確認します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 権限がデータの変更に依存していない場合は、このルールからの警告を抑制しても安全です。 ただし、命令型の要求を、それと等価な宣言に変更することをお勧めします。

## <a name="see-also"></a>関連項目
 [安全なコーディングのガイドライン](https://msdn.microsoft.com/library/4f882d94-262b-4494-b0a6-ba9ba1f5f177)[データとモデリング](https://msdn.microsoft.com/library/8c37635d-e2c1-4b64-a258-61d9e87405e6)
