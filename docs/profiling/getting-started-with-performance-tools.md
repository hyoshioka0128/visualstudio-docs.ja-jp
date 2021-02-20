---
title: パフォーマンス ツールの概要 | Microsoft Docs
description: コード パフォーマンス データを収集、表示、分析するために Visual Studio で提供されているさまざまな方法について学習します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2018
ms.topic: conceptual
helpviewer_keywords:
- getting started, performance
- getting started, profiling tools
ms.assetid: 02085214-a8e4-40fd-9b26-32391a7a7082
author: mikejo5000
ms.author: mikejo
manager: jmartens
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 1eb65e3cb8273f36cd9255bc0a3a2f8e91689f39
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99907366"
---
# <a name="getting-started-with-performance-tools"></a>パフォーマンス ツールの概要

Visual Studio では、さまざまな方法でコード パフォーマンス データを収集、表示、分析できます。 ほとんどの場合、パフォーマンス ツールの使用を開始する最良の方法は、**パフォーマンス ウィザード** の既定の設定を使用することです。 このウィザードによって、コードのパフォーマンス問題を指すことができるアプリ統計が収集されます。

- 一般的なコーディング問題を通知するパフォーマンス警告が Visual Studio の **[エラー一覧]** ウィンドウに表示されます。 表示された警告から、ソース コードに移動したり、より効率的なコードを記述するのに役立つ詳細なヘルプ トピックを確認したりできます。

- パフォーマンス レポートには、アプリケーションの構造、ソース コードの行、プロセスがさまざまなレベルで表示されます。 パフォーマンス レポートには、特定の関数を呼び出した関数と呼び出された関数からアプリ全体のコール ツリーまで、アプリ実行データが表示されます。

プロジェクト、アプリ、ASP.NET Web サイトをすばやくプロファイルするには、 **[デバッグ]** 、 **[パフォーマンス プロファイラー]** の順に選択し、 **[パフォーマンス ウィザード]** を選択します。 詳しい手順については、[パフォーマンス プロファイリングのビギナーズ ガイド](../profiling/beginners-guide-to-cpu-sampling.md)と「[方法: Web サイトのパフォーマンス データを収集する](../profiling/how-to-collect-performance-data-for-a-web-site.md)」を参照してください。

パフォーマンス プロファイル セッションを手動で指定し、構成するには、 **[デバッグ]** 、 **[プロファイラー]** 、 **[パフォーマンス エクスプローラー]** の順に選択します。 **[パフォーマンス エクスプローラー]** の **[ターゲット]** フォルダーと **[プロパティ]** ページを使用してセッションを構成します。 手順については、「[方法: パフォーマンス セッションを手動で作成する](../profiling/how-to-manually-create-performance-sessions.md)」を参照してください。

**関連項目:**

- [パフォーマンス ツールの概要](../profiling/overviews-performance-tools.md)
- [パフォーマンス ツール データを分析する](../profiling/analyzing-performance-tools-data.md)
- [パフォーマンス規則を使用したデータの分析](../profiling/using-performance-rules-to-analyze-data.md)
- [パフォーマンス セッションの構成](../profiling/configuring-performance-sessions.md)
