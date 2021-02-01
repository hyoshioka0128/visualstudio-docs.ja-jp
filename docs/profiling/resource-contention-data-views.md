---
title: リソース競合データのビュー | Microsoft Docs
description: スレッド競合プロファイル データが格納されるプロファイラー データ ファイルのビューとレポートに関するリファレンス情報について学習します。
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- profilng tools,concurrency profiling method view
- concurrency profiling method views
ms.assetid: be79ec41-f1dd-4984-993f-5c2962355a32
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 25dc334819c4b32bf74822e46dd3251919f621bf
ms.sourcegitcommit: 18729d7c99c999865cc2defb17d3d956eb3fe35c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2021
ms.locfileid: "98720333"
---
# <a name="resource-contention-data-views"></a>リソース競合データのビュー
このセクションでは、スレッド競合プロファイル データが格納されるプロファイラー データ ファイルのビューとレポートに関するリファレンス情報を示します。

## <a name="in-this-section"></a>このセクションの内容
- [概要ビュー - プロファイラー競合データ](../profiling/resource-contention-data-views.md)

 プロファイル データのグラフィカル タイムラインを表示し、最も多くのブロック イベントに参加した関数とリソースをリストします。

- [コール ツリー ビュー](../profiling/call-tree-view-contention-data.md)

 プロファイル実行の関数の実行パスおよびリソース競合データを表す階層ツリーを表示します。

- [モジュール ビュー](../profiling/modules-view-contention-data.md)

 スレッドおよびリソースの競合データをモジュール別に整理し、ブロック イベントの発生時に実行されていた関数、ソース コードの行、および命令をリストします。

- [呼び出し元/呼び出し先ビュー - 競合データ](../profiling/caller-callee-view-contention-data.md)

 選択した関数と、選択した関数を呼び出した関数および選択した関数によって呼び出された関数のスレッドおよびリソース競合データをリストします。

- [リソースの詳細ビュー](../profiling/resource-details-view-contention-data.md)

 競合しているリソースごとにブロック イベントのグラフィカル タイムラインを表示し、ブロック イベントの呼び出し履歴をリストします。

- [スレッドの詳細ビュー](../profiling/thread-details-view-contention-data.md)

 スレッドごとにブロック イベントのグラフィカル タイムラインを表示し、ブロック イベントの呼び出し履歴をリストします。

- [関数 ビュー](../profiling/functions-view-contention-data.md)

 関数ごとにスレッドおよびリソース競合データをリストします。

- [リソースの競合ビュー](../profiling/resource-contentions-view-contention-data.md)

 ブロックされたリソースごとにリソース競合データをリストします。

- [行 ビュー](../profiling/lines-view-contention-data.md)

 リソース コード行ごとにリソース競合データをリストします。

- [命令ポインター (IP) ビュー](../profiling/instruction-pointers-ips-view-contention-data.md)

 命令ごとにリソース競合をリストします。

- [プロセス ビュー](../profiling/process-view-contention-data.md)

 プロセスとスレッドごとにリソース競合をリストします。

## <a name="reference"></a>リファレンス
- [関数の詳細ビュー](../profiling/function-details-view.md)

 選択した関数と、選択した関数を呼び出した関数および選択した関数によって呼び出された関数の関係がグラフィカルな図で表示されます。
