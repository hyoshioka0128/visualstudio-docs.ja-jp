---
title: コア ビューのタイムライン | Microsoft Docs
description: タイムラインの基本、つまり、ある時点においてどのコアでどのスレッドが実行されたのかを判断する方法と拡大縮小の方法について学習します。
custom.ms: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.cv.cores.timeline.threads
helpviewer_keywords:
- Concurrency Visualizer, Cores View Timeline
ms.assetid: 10f0c666-ac2f-4ac5-9fb5-a88f660ab840
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: de09394bfc071cbe3dd1fedad52d1e5a511b62c7
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99882896"
---
# <a name="cores-view-timeline"></a>コア ビューのタイムライン
タイムラインの各行は、プロファイリング対象システムの論理プロセッサ コアを表します。 各行の、水平軸は特定の時点で論理コアで実行されたスレッドを示します。 タイムラインで興味のある色の上にマウス ポインターを合わせると、スレッドを特定するヒントが返されます。 ウィンドウの下部の凡例で、各色の意味がわかります。スレッドの特定に役立ちます。 ズーム ツールで拡大縮小できます。クリックしたままドラッグするか、CTRL を押しながらマウス ホイールを動かします。 コア ビューとスレッド ビューを切り替えるとき、ズームの一貫性が維持されます。

## <a name="see-also"></a>関連項目
- [コア ビュー](../profiling/cores-view.md)
- [ズーム コントロール (スレッド ビュー)](../profiling/zoom-control-threads-view.md)