---
title: Mobility Warnings
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.codeanalysis.MobilityRules
helpviewer_keywords:
- managed code analysis warnings, mobility warnings
- mobility warnings
- warnings, mobility
ms.assetid: 9808054c-593b-4fc3-92cc-1fc45f41569c
author: jillre
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a58bd6232d25d3151b019fc774befc99d9e46e6b
ms.sourcegitcommit: 00ba14d9c20224319a5e93dfc1e0d48d643a5fcd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2020
ms.locfileid: "77091744"
---
# <a name="mobility-warnings"></a>Mobility Warnings
モビリティの警告は、効率的な電力使用をサポートします。

## <a name="in-this-section"></a>このセクションの内容

|Rule|説明|
|----------|-----------------|
|[CA1600: アイドル状態のプロセス優先度を使用しません](../code-quality/ca1600.md)|プロセス優先順位に Idle を設定しないでください。 System.Diagnostics.ProcessPriorityClass.Idle を設定したプロセスは、CPU を占有するか、そうでない場合はアイドル状態になるため、スタンバイ状態がブロックされます。|
|[CA1601: 電源の状態の変更を妨げるタイマーを使用しません](../code-quality/ca1601.md)|定期的な動作の頻度が高くなると、CPU のビジー状態が続き、ディスプレイとハード ディスクをオフにする省電力アイドル タイマーに影響を与えます。|
