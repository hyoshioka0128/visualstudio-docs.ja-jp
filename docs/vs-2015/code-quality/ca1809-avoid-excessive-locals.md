---
title: 'CA1809: 過度なローカルを避けてください |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1809
- AvoidExcessiveLocals
helpviewer_keywords:
- AvoidExcessiveLocals
- CA1809
ms.assetid: 5c81ea43-cb49-448f-980f-a1dd9764043c
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: d39c8d9d09cf457738df87e3c2e6e109f7bc1696
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85543859"
---
# <a name="ca1809-avoid-excessive-locals"></a>CA1809:ローカルを使用しすぎないでください
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|AvoidExcessiveLocals|
|CheckId|CA1809|
|カテゴリ|Microsoft. パフォーマンス|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 メンバーに64個を超えるローカル変数が含まれており、その一部がコンパイラによって生成される可能性があります。

## <a name="rule-description"></a>ルールの説明
 一般的なパフォーマンスの最適化では、メモリ内ではなくプロセッサレジスタに値を格納します。これは、値の *登録* と呼ばれます。 共通言語ランタイムは、enregistration 用に最大64のローカル変数を考慮します。 Enregistered ではない変数はスタックに配置され、操作の前にレジスタに移動する必要があります。 すべてのローカル変数が enregistered を取得できるようにするには、ローカル変数の数を64に制限します。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、64を超えるローカル変数を使用するように実装をリファクターします。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 パフォーマンスが問題にならない場合は、このルールからの警告を抑制するか、ルールを無効にしても安全です。

## <a name="related-rules"></a>関連規則
 [CA1804:使用されていないローカルを削除します](../code-quality/ca1804-remove-unused-locals.md)
