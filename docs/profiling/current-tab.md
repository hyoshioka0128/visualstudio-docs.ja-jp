---
title: 現在のタブ | Microsoft Docs
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
ms.openlocfilehash: f48ba44d41286f1cf5eda6ececb68d21d39abd14
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "62552789"
---
# <a name="current-tab"></a>現在のタブ
**現在**のタブをクリックすると、CPU スレッド セグメントが選択されている場合、現在の選択ポイントに最も近い呼び出し履歴 (利用できる場合) が表示されます。  その場合、選択ポイントはタイムラインの上に黒い矢印またはキャレットで表示されます。 ブロッキング セグメントが選択されているとき、実行がないため、キャレットは表示されません。 しかしながら、セグメントは強調表示され、呼び出し履歴が表示されます。

 **現在**タブには、DirectX アクティビティ セグメント、マーカー、I/O アクセスに関する情報も表示されます。  DirectX アクティビティの場合、DMA パケットがハードウェア キューにより処理される方法に関する情報が表示されます。  マーカーの場合、説明とマーカーの種類に関する情報が表示されます。  I/O アクセスの場合、ファイルと読み込まれた (または書き込まれた) バイトの数に関する情報が表示されます。

## <a name="see-also"></a>参照
- [スレッド ビュー](../profiling/threads-view-parallel-performance.md)