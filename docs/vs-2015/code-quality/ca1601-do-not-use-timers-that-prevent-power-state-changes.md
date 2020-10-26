---
title: 'CA1601: 電源状態の変更を妨げるタイマーを使用しない |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1601
- DoNotUseTimersThatPreventPowerStateChanges
helpviewer_keywords:
- CA1601
- DoNotUseTimersThatPreventPowerStateChanges
ms.assetid: b8028c92-0696-4c54-9773-0028f29bda9a
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 7928b2fff8c12ca3f0cc3c58bee31fe5809517e5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85545640"
---
# <a name="ca1601-do-not-use-timers-that-prevent-power-state-changes"></a>CA1601:電源の状態の変更を妨げるタイマーを使用しません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|値|
|-|-|
|TypeName|DoNotUseTimersThatPreventPowerStateChanges|
|CheckId|CA1601|
|カテゴリ|Microsoft モビリティ|
|互換性に影響する変更点|あり|

## <a name="cause"></a>原因
 タイマーの間隔が1秒間に複数回発生するように設定されています。

## <a name="rule-description"></a>ルールの説明
 1秒間に複数回ポーリングしたり、1秒間に1回以上発生するタイマーを使用したりしないでください。 定期的な動作の頻度が高くなると、CPU のビジー状態が続き、ディスプレイとハード ディスクをオフにする省電力アイドル タイマーに影響を与えます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 タイマー間隔を1秒あたり1回未満に設定します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 このルールは、タイマーを1秒間に複数回実行する必要があり、モビリティに関する考慮事項を無視しても問題がない場合にのみ抑制する必要があります。
