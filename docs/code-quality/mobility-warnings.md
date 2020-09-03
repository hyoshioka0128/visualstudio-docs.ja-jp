---
title: モビリティに関する警告
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.codeanalysis.MobilityRules
helpviewer_keywords:
- managed code analysis warnings, mobility warnings
- mobility warnings
- warnings, mobility
ms.assetid: 9808054c-593b-4fc3-92cc-1fc45f41569c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6061b614442d7bcb2f3465b1c40f35d583626c45
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "78167586"
---
# <a name="mobility-warnings"></a>モビリティに関する警告
モビリティの警告は、効率的な電力使用をサポートします。

## <a name="in-this-section"></a>このセクションの内容

|ルール|説明|
|----------|-----------------|
|[CA1600:アイドル状態のプロセス優先度を使用しません](../code-quality/ca1600.md)|プロセス優先順位に Idle を設定しないでください。 System.Diagnostics.ProcessPriorityClass.Idle を設定したプロセスは、CPU を占有するか、そうでない場合はアイドル状態になるため、スタンバイ状態がブロックされます。|
|[CA1601:電源の状態の変更を妨げるタイマーを使用しません](../code-quality/ca1601.md)|定期的な動作の頻度が高くなると、CPU のビジー状態が続き、ディスプレイとハード ディスクをオフにする省電力アイドル タイマーに影響を与えます。|
