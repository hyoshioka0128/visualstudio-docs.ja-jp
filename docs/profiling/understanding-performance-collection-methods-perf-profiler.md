---
title: プロファイラー パフォーマンス収集方法について
description: Visual Studio パフォーマンス プロファイラー内のツールで使用されるデータ収集方法について学習します。
ms.date: 4/30/2020
ms.topic: conceptual
f1_keywords: ''
helpviewer_keywords:
- Performance Profiler, profiling methods
author: mikejo5000
ms.author: mikejo
manager: jmartens
monikerRange: '>= vs-2017'
ms.workload:
- multiple
ms.openlocfilehash: f9128700f6ad54f3d92108d92e25e13b9ee4266c
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99921865"
---
# <a name="understand-profiler-performance-collection-methods"></a>プロファイラー パフォーマンス収集方法について

このドキュメントでは、Visual Studio パフォーマンス プロファイラー内のツールで使用されるデータ収集方法について説明します。 

## <a name="sampling"></a>サンプリング

プロファイリングするためのサンプリング方式では、プロファイリングの実行中にアプリケーションで実行された作業に関する統計データが収集されます。 データ収集は、アプリケーションに関する情報を一定の間隔またはサンプリング頻度 (例: ミリ秒ごと) で収集した後、このデータを分析してアプリケーションで時間が費やされた場所のモデルを作成することによって実行されます。 サンプリング方式は負荷が少なく、プロファイリングされるアプリケーションの実行にほとんど影響しません。 サンプリング方式を使用するパフォーマンス プロファイラーのツールには、[CPU 使用率](../profiling/cpu-usage.md)ツールが含まれます。

## <a name="instrumentation"></a>インストルメンテーション

インストルメンテーション プロファイリングでは、プロファイリングの実行中にアプリケーションによって実行された作業に関する詳細データが収集されます。 データ収集は、タイミング情報をキャプチャするコードをバイナリ ファイルに挿入するか、アプリケーションの実行中にコールバック フックを使用して正確なタイミングと呼び出し回数の情報を収集して出力するツールによって実行されます。 サンプリングベースのアプローチに比べて、インストルメンテーション方式ではオーバーヘッドが高くなります。 インストルメンテーションを使用するパフォーマンス プロファイラーのツールには、[.NET オブジェクト割り当て](../profiling/dotnet-alloc-tool.md)ツールが含まれます。