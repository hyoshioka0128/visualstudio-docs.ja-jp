---
title: 現在のタブ | Microsoft Docs
description: スレッド ビューの現在のタブを選択すると、CPU スレッド セグメントまたはブロッキング セグメントの呼び出し履歴が表示されます。 DirectX セグメントに関する情報もあります。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.reportnav.current
helpviewer_keywords:
- Concurrency Visualizer, Callstack at Selection Point
ms.assetid: 2c7b1ae5-3756-4795-bc59-f6bb113f2ba5
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 65261d6304ead5ade7c28f40495fa68afb0c2171
ms.sourcegitcommit: d13f7050c873b6284911d1f4acf07cfd29360183
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/22/2021
ms.locfileid: "98686219"
---
# <a name="current-tab"></a>現在のタブ
**現在** のタブをクリックすると、CPU スレッド セグメントが選択されている場合、現在の選択ポイントに最も近い呼び出し履歴 (利用できる場合) が表示されます。  その場合、選択ポイントはタイムラインの上に黒い矢印またはキャレットで表示されます。 ブロッキング セグメントが選択されているとき、実行がないため、キャレットは表示されません。 しかしながら、セグメントは強調表示され、呼び出し履歴が表示されます。

 **現在** タブには、DirectX アクティビティ セグメント、マーカー、I/O アクセスに関する情報も表示されます。  DirectX アクティビティの場合、DMA パケットがハードウェア キューにより処理される方法に関する情報が表示されます。  マーカーの場合、説明とマーカーの種類に関する情報が表示されます。  I/O アクセスの場合、ファイルと読み込まれた (または書き込まれた) バイトの数に関する情報が表示されます。

## <a name="see-also"></a>関連項目
- [スレッド ビュー](../profiling/threads-view-parallel-performance.md)