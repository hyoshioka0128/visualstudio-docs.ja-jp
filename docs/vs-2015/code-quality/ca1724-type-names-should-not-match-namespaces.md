---
title: 'CA1724: 型名を名前空間と一致させることはできません |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- TypeNamesShouldNotMatchNamespaces
- CA1724
helpviewer_keywords:
- TypeNamesShouldNotMatchNamespaces
- CA1724
ms.assetid: 329af3b5-5600-4101-831d-531ab3eb7060
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: aa0b73b6608f0dfd5daa4b770b7d780e64704c99
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544431"
---
# <a name="ca1724-type-names-should-not-match-namespaces"></a>CA1724:型名は名前空間と同一にすることはできません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|アイテム|値|
|-|-|
|TypeName|TypeNamesShouldNotMatchNamespaces|
|CheckId|CA1724|
|カテゴリ|Microsoft.Naming|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]大文字と小文字を区別しない比較では、型名は名前空間名と一致します。

## <a name="rule-description"></a>ルールの説明
 型の名前は、[!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] クラス ライブラリで定義されている名前空間の名前と一致しないようにする必要があります。 この規則に違反すると、ライブラリが使いづらくなります。

## <a name="how-to-fix-violations"></a>違反の修正方法
 クラスライブラリの名前空間の名前と一致しない型名を選択して [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] ください。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 新しい開発では、このルールの警告を抑制する必要がある既知のシナリオはありません。 警告を抑制する前に、ライブラリのユーザーと一致する名前が混同されているかどうかを慎重に検討してください。 配布ライブラリの場合、このルールからの警告を抑制することが必要になる場合があります。
