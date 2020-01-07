---
title: グラフィックス API とメモリの統計情報 |Microsoft Docs
ms.date: 03/02/2017
ms.topic: conceptual
f1_keywords:
- vs.graphics.apistatistics
- vs.graphics.memorystatistics
ms.assetid: 27d2f303-e3ed-4219-9009-345a0d849506
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: fa808e76e6655c5d57108c923b19794d0398b80c
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72735575"
---
# <a name="graphics-api-and-memory-statistics"></a>グラフィックス API とメモリの統計情報
<!-- VERSIONLESS -->
Visual Studio 2017 以降では、グラフィックス API 統計とメモリ統計ツールがサポートされています。  これら2つのツールを使用すると、さまざまなリソースの GPU メモリ消費だけでなく、Direct3D API の使用状況に関するさまざまな情報を表示できます。

## <a name="graphics-api-statistics"></a>グラフィックス API の統計情報
Visual Studio グラフィックス診断のグラフィックス API 統計を使用すると、実行されたすべての Direct3D 呼び出しと各呼び出しの数を表示できます。  ウィンドウを表示するには、 **[> API の統計情報を表示]** メニュー項目を選択します。

![API 統計情報](media/gfx_diag_api_statistics.png)

このツールを使用すると、発生している可能性がある DirectX 呼び出しを検出したり、頻繁に発生するような呼び出しを行ったりできます。

ウィンドウ内を右クリックすると、すべてのデータが CSV としてコピーされ、さらに分析するために Excel のようなものに貼り付けることができます。

## <a name="memory-statistics"></a>メモリ統計情報
このツールでは、フレームに作成したリソースに対してグラフィックスドライバーが割り当てているメモリの量が表示されます。  このウィンドウを表示するには、 **[> メモリ統計情報の表示]** メニュー項目を選択します。

![メモリ統計情報](media/gfx_diag_memory_statistics.png)

**GPU 割り当て**列には、**イベント**列に表示されるイベントによって使用されるメモリの量が表示されます。  また、[ウォッチ] アイコン ![watch アイコン ](media/gfx_watch.png) を選択して、選択したイベントの[リソース履歴](graphics-event-list.md#resource-history)を表示することもできます。

API 統計情報ツールと同様に、ウィンドウ内を右クリックしてすべてのデータを CSV としてコピーし、さらに分析するために Excel のように貼り付けることができます。

## <a name="see-also"></a>関連項目
- [グラフィックス診断 (DirectX グラフィックスのデバッグ)](visual-studio-graphics-diagnostics.md)
- [リソース履歴](graphics-event-list.md#resource-history)
<!-- /VERSIONLESS -->
