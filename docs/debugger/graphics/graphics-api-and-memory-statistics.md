---
title: グラフィックス API 統計情報とメモリ統計情報 | Microsoft Docs
description: グラフィックス API 統計情報ツールとメモリ統計情報ツールについて説明します。これらのツールには、さまざまなリソースの Direct3D API 使用状況と GPU メモリ消費に関する情報が表示されます。
ms.custom: SEO-VS-2020
ms.date: 03/02/2017
ms.topic: conceptual
f1_keywords:
- vs.graphics.apistatistics
- vs.graphics.memorystatistics
ms.assetid: 27d2f303-e3ed-4219-9009-345a0d849506
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 08c9f518f6d56f2ec211ef494da3890a56bf1369
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99882298"
---
# <a name="graphics-api-and-memory-statistics"></a>グラフィックス API 統計情報とメモリ統計情報
<!-- VERSIONLESS -->
Visual Studio 2017 以降では、グラフィックス API 統計情報ツールとメモリ統計情報ツールがサポートされています。  これら 2 つのツールを使用して、Direct3D API の使用状況と、さまざまなリソースの GPU メモリ消費に関するさまざまな情報を表示できます。

## <a name="graphics-api-statistics"></a>グラフィックス API 統計情報
Visual Studio グラフィックス診断のグラフィックス API 統計情報を使用して、実行されたすべての Direct3D 呼び出しと各呼び出しの回数を表示できます。  ウィンドウを表示するには、 **[ビュー] > [API 統計情報]** メニュー項目を選択します。

![API 統計情報](media/gfx_diag_api_statistics.png)

このツールを使用して、行っていることに気付いていない DirectX 呼び出しや回数が多い呼び出しを簡単に見つけることができます。

ウィンドウ内を右クリックして、すべてのデータを CSV としてコピーできます。これを Excel などに貼り付けて、さらに分析することができます。

## <a name="memory-statistics"></a>メモリ統計情報
このツールでは、フレームで作成したリソースに対してグラフィック ドライバーが割り当てているメモリの量が表示されます。  このウィンドウを表示するには、 **[ビュー] > [メモリ統計情報]** メニュー項目を選択します。

![メモリ統計情報](media/gfx_diag_memory_statistics.png)

**[GPU 割り当て]** 列には、 **[イベント]** 列に表示されているイベントによって使用されるメモリの量が表示されます。  また、![ウォッチ アイコン](media/gfx_watch.png) [ウォッチ アイコン](graphics-event-list.md#resource-history) を選択して、選択したイベントのリソース履歴を表示することもできます。

API 統計情報ツールと同じように、ウィンドウ内を右クリックして、すべてのデータを CSV としてコピーできます。これを Excel などに貼り付けて、さらに分析することができます。

## <a name="see-also"></a>関連項目
- [グラフィックス診断 (DirectX グラフィックスのデバッグ)](visual-studio-graphics-diagnostics.md)
- [リソース履歴](graphics-event-list.md#resource-history)
<!-- /VERSIONLESS -->