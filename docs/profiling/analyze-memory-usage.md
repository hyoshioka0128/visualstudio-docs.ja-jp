---
title: メモリ使用量の分析
description: メモリ リークや非効率的なメモリ使用量を見つけるためのツール、すなわち、メモリ使用量ツールや .NET オブジェクト割り当てツールなどのツールについて説明します。
ms.custom: SEO-VS-2020, seodec18
ms.date: 10/12/2020
ms.topic: conceptual
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 675636b7abca10fb2f9f1898d753155235830f86
ms.sourcegitcommit: a436ba564717b992eb1984b28ea0aec801eacaec
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2021
ms.locfileid: "98205724"
---
# <a name="analyze-memory-usage"></a>メモリ使用量の分析

メモリ リークおよび非効率的なメモリ使用量を見つけるには、.NET オブジェクト割り当てツールや事後分析メモリ使用量ツールなど、パフォーマンス プロファイラーにあるデバッガー統合メモリ使用量診断ツールなどのツールを使用できます。

メモリ使用量ツールを使用すると、マネージド メモリ ヒープ、およびネイティブ メモリ ヒープの 1 つまたは複数の *スナップショット* を取得できます。 .NET アプリ、ASP.NET アプリ、C++ アプリ、または混在モード (.NET とネイティブ) アプリのスナップショットを収集できます。 **メモリ使用率** ツールは、開かれた状態の Visual Studio プロジェクトまたはインストール済みの Microsoft Store アプリで実行することができます。または、実行中のアプリまたはプロセスにアタッチすることもできます。 **メモリ使用率** ツールは、デバッグを使用して、または使用せずに実行することができます。 詳細については、「[デバッガーを使用して、または使用せずにプロファイリング ツールを実行する](../profiling/running-profiling-tools-with-or-without-the-debugger.md)」を参照してください。 デバッガーで、メモリ プロファイルをオンまたはオフにして、メモリ使用率のオブジェクトごとの内訳を確認することができます。 たとえばブレークポイントなどで、実行が一時停止したときに、メモリ使用率の結果を表示できます。

.NET 開発者は、.NET オブジェクト割り当てツールまたは[メモリ使用量](../profiling/memory-usage.md)ツールのいずれかを選択できます。

- [.NET オブジェクト割り当てツール](../profiling/dotnet-alloc-tool.md)を使用すると、.NET コード内の割り当てパターンと異常を識別したり、ガベージ コレクションの一般的な問題を識別したりすることができます。 このツールは、事後分析ツールとしてのみ実行されます。 このツールは、ローカルまたはリモートのマシンで実行できます。
- [メモリ使用量ツール](../profiling/memory-usage-without-debugging2.md)は、通常 .NET アプリでは一般的でないメモリ リークを識別するのに役立ちます。 メモリのチェック中に、コードのステップ実行など、デバッガーの機能を使用する必要がある場合は、[デバッガー統合メモリ使用量](../profiling/memory-usage.md)ツールをお勧めします。

C++ 開発者は、デバッガーに統合された、またはデバッガーなしの、メモリ使用量ツールを使用できます。

- [デバッガーを使用してメモリ使用量を分析する](../profiling/memory-usage.md)
- [デバッガーなしでメモリ使用量を分析する](../profiling/memory-usage-without-debugging2.md)

Windows 7 以降ではデバッガーなしでプロファイル ツールを使用することができます。 Windows 8 以降では、デバッガーを使用してプロファイル ツールを実行する必要があります ( **[診断ツール]** ウィンドウ)。

## <a name="blogs-and-videos"></a>ブログとビデオ

[デバッグ中に CPU とメモリを分析する](https://devblogs.microsoft.com/visualstudio/analyze-cpu-memory-while-debugging/)

[Visual C++ ブログ:Visual C++ 2015 のメモリ プロファイル](https://devblogs.microsoft.com/cppblog/memory-profiling-in-visual-c-2015/)

## <a name="see-also"></a>関連項目

- [Visual Studio のプロファイル](../profiling/index.yml)
- [プロファイル ツールの概要](../profiling/profiling-feature-tour.md)
