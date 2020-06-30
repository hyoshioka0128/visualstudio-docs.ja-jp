---
title: 'CA2004: GC の呼び出しを削除します。KeepAlive |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- RemoveCallsToGCKeepAlive
- CA2004
helpviewer_keywords:
- RemoveCallsToGCKeepAlive
- CA2004
ms.assetid: bc543b5b-23eb-4b45-abc2-9325cd254ac2
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 53fa5f61cb7c503502956831452bc3eca1a9fece
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85521200"
---
# <a name="ca2004-remove-calls-to-gckeepalive"></a>CA2004:GC.KeepAlive への呼び出しを削除します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|RemoveCallsToGCKeepAlive|
|CheckId|CA2004|
|カテゴリ|Microsoft.Reliability|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 クラス `SafeHandle` はを使用しますが、の呼び出しは引き続き含まれ `GC.KeepAlive` ます。

## <a name="rule-description"></a>ルールの説明
 使用法に変換する場合は `SafeHandle` 、(object) へのすべての呼び出しを削除 `GC.KeepAlive` します。 この場合、クラスは `GC.KeepAlive` 、ファイナライザーを持たないもの `SafeHandle` の、OS ハンドルを完了するために依存していることを前提として、を呼び出す必要はありません。  を呼び出したままにすると、パフォーマンスによって測定されるのではなく、の `GC.KeepAlive` 呼び出しが必要か、または `GC.KeepAlive` 存在しない可能性のある有効期間の問題を解決するのに十分であるという認識は、コードの保守が困難になります。

## <a name="how-to-fix-violations"></a>違反の修正方法
 の呼び出しを削除 `GC.KeepAlive` します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この警告を非表示にすることができるのは、 `SafeHandle` クラスの使用法への変換が技術的に適切でない場合のみです。
