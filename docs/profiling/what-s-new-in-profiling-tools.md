---
title: Visual Studio 2017 でのプロファイリングの新機能 | Microsoft Docs
description: 診断ツールに、修正が必要なアプリの問題の識別に役立つ新しい視覚化が追加されたことについて学習します。
titleSuffix: ''
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- profiling
- what's new
ms.assetid: d4736cc8-8961-4089-be9e-d5190ce8353c
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
monikerRange: vs-2017
ms.openlocfilehash: 9619daea30960f72b183447839db89adbaee7eb2
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99938487"
---
# <a name="whats-new-in-profiling-tools-in-includevs_dev15"></a>[!include[vs_dev15](../misc/includes/vs_dev15_md.md)] プロファイリング ツールの新機能

診断ツールに、修正が必要なアプリの問題を識別できる新しい視覚化が追加されました。 診断ツールに ASP.NET アプリのサポートが追加されました。

詳しくは、「[[!include[vs_dev15](../misc/includes/vs_dev15_md.md)] リリース ノート](/visualstudio/releasenotes/vs2017-relnotes)」をご覧ください。

パフォーマンス分析の主な領域に重点を置くことができる、**概要** タブがツールに追加されました。 概要タブには発生したイベントの数が表示され、ヒープのスナップショットを作成して、CPU 使用率のデータ収集を直ちに有効にすることができます。 このビューには、[Application Insights](/azure/azure-monitor/app/visual-studio) または [UI Analysis](/visualstudio/releasenotes/vs2017-relnotes) のイベントが表示されます。 また、Visual Studio Enterprise では、ビューに IntelliTrace イベントも表示されます。

![[診断ツール] の [概要] タブ](../profiling/media/diag-tools-summary-tab-2.png "DiagToolsSummaryTab")

CPU 使用率ツールに[新しい視覚化](../profiling/Beginners-Guide-to-Performance-Profiling.md)が加えられ、パフォーマンスの問題の原因になっている可能性が最も高い関数を識別できます。 新しい **呼び出し元/呼び出し先** ビューによって、選択した関数に対して、または選択した関数から行われる関数呼び出しのコストを調べることができます。

![診断ツールの [呼び出し元/呼び出し先] ビュー](../profiling/media/diag-tools-caller-callee-2.png "DiagToolsCallerCallee")

## <a name="see-also"></a>関連項目

- [Visual Studio のプロファイル](../profiling/index.yml)
- [プロファイル ツールの概要](../profiling/profiling-feature-tour.md)