---
title: パフォーマンス規則リファレンス | Microsoft Docs
description: プロファイル ツールのパフォーマンス規則を使用して、アプリケーションのパフォーマンスに関する追加の警告や情報を提供する方法について学習します。
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 59fc9424-76ca-4365-ae47-bb14a736c9c2
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: ca20a6a1ad687fde432d0b748aa8b87c823a1da2
ms.sourcegitcommit: 18729d7c99c999865cc2defb17d3d956eb3fe35c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2021
ms.locfileid: "98723284"
---
# <a name="performance-rules-reference"></a>パフォーマンス規則リファレンス
プロファイリング ツールのパフォーマンス規則は、アプリケーションのパフォーマンスに関する追加の警告や情報を提供します。 パフォーマンス規則は、Windows やプロセッサのパフォーマンス カウンターなどのソースから収集されたプロファイリング実行のデータを分析します。 規則のメッセージは、[!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] 統合開発環境のエラー出力ウィンドウに表示されます。 メッセージは、次のいずれかの規則レベルとして一覧表示されます。

|カテゴリ|説明|
|-|-|
|**エラー**|パフォーマンス上の問題の多くは明白なエラーではないため、エラー メッセージが生成される規則はわずかです。 エラー メッセージは、プロファイル データの収集の失敗を示す場合もあります。|
|**警告**|警告は、パフォーマンス上の問題の原因となる可能性があるアプリケーションの領域、または最適化した方がよい可能性があるアプリケーションの領域を示します。|
|**情報**|情報メッセージは、規則の条件の分析がエラー メッセージを生成するしきい値に達しなかったこと、またはメッセージの情報が有用ではあるがパフォーマンス上の問題を表していないことを示します。|

## <a name="in-this-section"></a>このセクションの内容

[ID 別のパフォーマンス規則](../profiling/performance-rules-by-id.md)

プロファイリング ツールのパフォーマンス規則は、次の 4 つのカテゴリに分類されます。

|カテゴリ|説明|
|-|-|
|[.NET Framework の使用に関するパフォーマンス規則](../profiling/dotnet-framework-usage-performance-rules.md)|.NET Framework を効率的に使用するのに役立つ規則。|
|[メモリとページングのパフォーマンス規則](../profiling/memory-and-paging-performance-rules.md)|アプリケーションのマネージド メモリとページング動作を分析する規則。|
|[プロファイリング ツールの使用に関する規則](../profiling/profiling-tools-usage-rules.md)|プロファイリング ツールを効率的に使用するのに役立つ規則。|
|[リソース監視のパフォーマンス規則](../profiling/resource-monitoring-performance-rules.md)|プロファイリング実行のプロセッサとメモリの使用率に関する情報メッセージ。|
