---
title: サンプリング データ値について | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- sampling profiling method
- Profiling Tools, sampling
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 289f92deaceca32a44249ed77c17187743a34fa4
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2019
ms.locfileid: "74778051"
---
# <a name="understand-sampling-data-values"></a>サンプリング データ値について

Visual Studio プロファイリング ツールの "*サンプリング*" プロファイル方式では、設定された間隔でコンピューター プロセッサに割り込み、関数の呼び出し履歴を収集します。 *呼び出し履歴*は、プロセッサ上で実行されている関数に関する情報を格納する動的な構造です。

プロファイラー分析は、プロセッサがターゲット プロセス内のコードを実行しているかどうかを判別します。 プロセッサがターゲット プロセス内のコードを実行していない場合、サンプルは破棄されます。

プロセッサがターゲット コードを実行している場合、プロファイラーは、呼び出し履歴の各関数のサンプル カウントをインクリメントします。 サンプルの取得時には、呼び出し履歴上の 1 つの関数のみがコードを実行中です。 スタック上の他の関数は、関数呼び出し階層内の親であり、子の復帰を待機しています。

プロファイラーは、サンプル イベントに対して、現在命令を実行している関数の*排他*サンプル数をインクリメントします。 排他サンプルは、関数の合計 (*包括*) サンプル数にも含まれるため、現在アクティブな関数の包括サンプル数もインクリメントされます。

 プロファイラーは、呼び出し履歴上のすべての関数の包括サンプル数をインクリメントします。

## <a name="inclusive-samples"></a>包括サンプル

対象の関数の実行中に収集されるサンプルの合計数。

これには、関数コードを直接実行しているときに収集されたサンプルと、対象の関数によって呼び出された子関数の実行中に収集されたサンプルが含まれます。

## <a name="exclusive-samples"></a>排他サンプル

対象の関数の命令を直接実行中しているときに収集されたサンプルの数。

排他サンプルには、対象の関数によって呼び出された関数の実行中に収集されたサンプルは含まれません。

## <a name="inclusive-percent"></a>包括 (%)

関数またはデータ範囲の包括サンプル数である、プロファイリング実行での包括サンプル合計数の割合。

## <a name="exclusive-percent"></a>排他 (%)

関数またはデータ範囲の排他サンプル数である、プロファイリング実行での排他サンプル合計数の割合。

## <a name="see-also"></a>関連項目

[方法: 収集方法を選択する](../profiling/how-to-choose-collection-methods.md)
[パフォーマンス ツール データの分析](../profiling/analyzing-performance-tools-data.md)
