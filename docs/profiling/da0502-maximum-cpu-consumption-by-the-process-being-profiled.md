---
title: 'DA0502: プロセスによる最大 CPU 使用量をプロファイリングしています | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.performance.rules.DA0502
- vs.performance.DA0502
- vs.performance.502
ms.assetid: 1ee53df5-b0dc-4265-9d4f-527830d08725
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 5c3cb5169d078ba1242bf898ba93e31a7a488bb8
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "74779338"
---
# <a name="da0502-maximum-cpu-consumption-by-the-process-being-profiled"></a>DA0502: プロセスによる最大 CPU 使用量をプロファイリングしています

|||
|-|-|
|規則 ID|DA0502|
|カテゴリ|リソース監視|
|プロファイル方法|All|
|[メッセージ]|この規則は情報提供用です。 Process()\\% Processor Time カウンターはプロファイリングを行っているプロセスの CPU 使用量を測定します。 報告される値は、全測定期間を通じて観察された最大値です。|
|規則の種類|情報|

 サンプリング、.NET メモリ、またはリソース競合メソッドを使用してプロファイリングを行うときは、この規則を呼び出すためのサンプルを少なくとも 10 個収集する必要があります。

## <a name="rule-description"></a>規則の説明
 このメッセージにより、アプリケーションの命令の実行中にプロセッサがビジー状態になった最大時間がパーセントで報告されます。 プロファイリング中のプロセスがアクティブな状態にあるすべての測定間隔を通じて取得された値のうち、最も大きな値がこのメッセージによって報告されます。 複数のプロセッサが搭載されたコンピューターの場合、パーセントが 100% を超える可能性があります。

## <a name="how-to-use-the-rule-data"></a>規則データの使用方法
 規則の値を使用して、特定のプログラムの異なるバージョンやビルドを比較したり、さまざまなプロファイリング シナリオにおけるアプリケーションのパフォーマンスを確認したりします。
