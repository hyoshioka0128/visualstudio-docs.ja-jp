---
title: 'CA1600: アイドル状態のプロセス優先度を使用しない |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- DoNotUseIdleProcessPriority
- CA1600
helpviewer_keywords:
- CA1600
- DoNotUseIdleProcessPriority
ms.assetid: 9b0d073b-78b6-41be-8ef3-14692a735283
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 3f6233136dcf7f1db5d622a02419d33e0eedacf5
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545679"
---
# <a name="ca1600-do-not-use-idle-process-priority"></a>CA1600:アイドル状態のプロセス優先度を使用しません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|アイテム|値|
|-|-|
|TypeName|DoNotUseIdleProcessPriority|
|CheckId|CA1600|
|カテゴリ|Microsoft モビリティ|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 このルールは、プロセスがに設定されている場合に発生し `ProcessPriorityClass.Idle` ます。

## <a name="rule-description"></a>ルールの説明
 プロセス優先順位に Idle を設定しないでください。 があるプロセスは、 `System.Diagnostics.ProcessPriorityClass.Idle` CPU がアイドル状態になると CPU を占有するため、スタンバイをブロックします。

## <a name="how-to-fix-violations"></a>違反の修正方法
 プロセスをに設定 `ProcessPriorityClass.BelowNormal` します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 このルールは、アイドル状態のプロセスの優先順位が必要で、モビリティに関する考慮事項を安全に無視できる場合にのみ抑制する必要があります。
